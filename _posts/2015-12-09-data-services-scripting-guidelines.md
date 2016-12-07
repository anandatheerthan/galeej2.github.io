---
layout: post
title: Data Services Scripting Guidelines
date: 2015-12-09 06:23
author: administrator
comments: true
categories: [SAP Data Services]
---
<h3>Scripting Guidelines</h3>
<ul>
	<li>Statements in a script object or custom function must end with a semicolon (;)</li>
	<li>Comment lines must start with a # character.</li>
	<li>Use single quotes for string constants.</li>
	<li>Uses the backslash (\) as the escape character.
<pre>E.g. 
single quote (') -&gt; ' WHERE NAME LIKE \'SAURAV\' '
backslash (\) -&gt; 'C:\\DS'
</pre>
Also strings including curly braces or square brackets cause a processing error. We can avoid the error by preceding the braces or brackets with a backslash (\).</li>
	<li>Data Services does not strip trailing blanks from strings that are used in scripts or custom functions. To remove trailing blanks, we can use the rtrim or rtrim_blank function.</li>
	<li>Variable Names must be preceded by a dollar sign ($).</li>
	<li>Global Variables used in a script or expression must be defined at the Job level using the <b>Variables and Parameters</b> window.</li>
	<li>Local Variables used in a script or expression must be defined in the Job or Workflow context that calls the script, using the <b>Variables and Parameters</b> window; Local variables used in a Custom Function must be defined using the Smart Editor.</li>
	<li>The square brackets ([]) indicate that the value of the expression should be substituted.</li>
	<li>The curly braces ({}) indicate that the value of the expression should be quoted with single quotation marks.</li>
</ul>
<h3>Sample Examples</h3>
<ol>
	<li>
<pre>#Drop Table if it exists in Database
sql( 'DataStore_Name', 'IF EXISTS(SELECT NAME FROM DBO.SYSOBJECTS 
 WHERE NAME = \'Table_Name\' AND XTYPE = \'U\') DROP TABLE Table_Name');

#Create Table in Database
sql( 'DataStore_Name', 'CREATE TABLE Table_Name( Col1 VARCHAR(10), 
 Col2 INT )' );
print( 'Table Created' );
</pre>
</li>
	<li>
<pre>#Print Total Records in a Database Table
$LV_Count = total_rows(DataStore_Name.Owner_Name.Table_Name);
print( 'Total Records in Table: ' || $LV_Count );

#Alternatively
print( 'Total Records in Table: 
 [total_rows(DataStore_Name.Owner_Name.Table_Name)]' );
</pre>
</li>
	<li>
<pre>#Delete Data from table

$LV_Load_Date = sql('DataStore_Name','SELECT MAX(load_date) 
 FROM Batch_Control_Tbl');

sql( 'DataStore_Name', 'DELETE FROM TABLE_NAME WHERE load_date =
 {$LV_Load_Date}');
</pre>
</li>
	<li>
<pre>#  Various ways to define select
sql( 'DataStore_Name', 'SELECT sal FROM emp WHERE EMPNO ='
 || $LV_EMPNO );
sql( 'DataStore_Name', 'SELECT sal FROM emp WHERE ENAME LIKE
 {$LV_EMPNO}' );
sql( 'DataStore_Name', 'SELECT sal FROM emp WHERE ENAME LIKE 
 \'' || $LV_EMPNO || '\'' ); 
</pre>
</li>
	<li>
<pre>#Copy Contents of two files into a single file (Windows)
print(exec('cmd', 'copy "C:\\POC\\Header.txt"+"C:\\POC\\Detail.txt" 
 "C:\\POC\\ConvertedFile.txt"', 8));
</pre>
</li>
</ol>
<h3>Other useful custom scripts</h3>
<ol>
	<li>Drop a database table after determining the database type:
<pre># $G_Table_Name is the global variable to hold table name say STG_COMPLAIN
# DS_SRC_REPO is the Data Store name
# $V_String is a local variable

#1 For Microsoft_SQL_Server
if (upper( db_type( 'DS_SRC_REPO')) = 'MICROSOFT_SQL_SERVER')
begin
$V_String = 'SELECT NAME FROM sys.objects WHERE NAME = {$G_Table_Name}';
end
#2 For Oracle
if (upper( db_type( 'DS_SRC_REPO')) = 'ORACLE')
begin
$V_String = 'SELECT TABLE_NAME FROM USER_TABLES WHERE TABLE_NAME = {$G_Table_Name}';
end

# If table exists, then drop
if ( sql( 'DS_SRC_REPO',$V_String) IS not null )
begin
sql( 'DS_SRC_REPO','DROP TABLE '||$G_Table_Name);
sql( 'DS_SRC_REPO','CREATE TABLE [$G_Table_Name] ( COMPLAIN_ID int ) ');
end
</pre>
</li>
	<li>Set repository password same as username else defined via Global variable during Job Execution
<pre># If the repository password is not same as the repository user name then 
we need to set the the global variable $G_Repo_Password 

$G_Repo_Password = nvl($G_Repo_Password,datastore_field_value('DS_SRC_REPO','user'));
</pre>
</li>
	<li>Test repository connection at run-time
<pre># $G_Repo_Server is the global variable for Repository Server name 
# $G_Repo_Username is the global variable for Repository User name;
# $G_Repo_Password is the global variable for Repository Password;
# $G_Repo_Name is the global variable for Local Repository name;

#1 For Microsoft_SQL_Server with SQL server Authentication
IF(db_type('DS_SRC_REPO') = 'Microsoft_SQL_Server' 
and datastore_field_value('DS_SRC_REPO','mssql_windows_authentication') &lt;&gt; 'yes')
begin
$G_Repo_Server = nvl($G_Repo_Server,datastore_field_value('DS_SRC_REPO','sql_server_dataserver')); 
$G_Repo_Username = nvl($G_Repo_Username,datastore_field_value('DS_SRC_REPO','user'));
$G_Repo_Password = nvl($G_Repo_Password,datastore_field_value('DS_SRC_REPO','user'));
$G_Repo_Name = nvl($G_Repo_Name,datastore_field_value('DS_SRC_REPO','sql_server_database'));
$G_Repo_Info_for_al_engine ='-U[$G_Repo_Username] -P[$G_Repo_Password] 
-S[$G_Repo_Server] -NMicrosoft_SQL_Server -Q[$G_Repo_Name]';

print('INFO - The database type of the repository is: Microsoft_SQL_Server with SQL server Authentication');
end 

# Test repository connection 
# Successful message: Connected successfully to the repository. (BODI-300098)
# Unsuccessful message: Could not connect to the repository. (BODI-300099)
$V_Test_Repo = exec('al_engine.exe',' '||$G_Repo_Info_for_al_engine||' -test_repo',0);
print('INFO - Test repository connection: '||$V_Test_Repo);
If(index( $V_Test_Repo ,'BODI-300098',1) is null )
begin
print('ERROR - Could not connect to the repository &lt;[$G_Repo_Name]&gt;'
||',please check the value of the variables $G_Repo_Server,$G_Repo_Name,$G_Repo_Username and $G_Repo_Password.');
raise_exception('ERROR - Could not connect to the repository &lt;[$G_Repo_Name]&gt;'
||',please check the value of the variables $G_Repo_Server,$G_Repo_Name,$G_Repo_Username and $G_Repo_Password.');
end 
</pre>
</li>
	<li>Import database table at run-time
<pre>#IMPORT DATABASE TABLES INTO DATASTORE
print( 'Info - Importing table &lt;'|| $G_Table_Name || '&gt;');	

$L_Message = exec( 'al_engine.exe',' '|| $G_Repo_Info_for_al_engine
||' -I' || 'DS_SRC_REPO.DBO.' || $G_Table_Name, 0);

If( $L_Message is null)
begin
print('Info - The table &lt;'|| $G_Table_Name || '&gt; is imported successfully');
end
else
begin
print( $L_Message );
end
</pre>
</li>
	<li>Copy the error file to custom error directory at Catch block (Windows)
<pre>print( 'Exception Handling' );
print( error_number( ) );
print( error_context( ) );
print( error_message( ) );
$LOC = get_error_filename( );
$LOC = replace_substr( $LOC , '/', '\\' );

$FILE_NAME = 'C:\\TEMP\\Err_Customer_' || to_char( sysdate( ), 'YYYYMMDD' ) || '.txt';

print( exec( 'cmd', 'copy "' || $LOC || '" ' || $FILE_NAME, 8 ));
</pre>
</li>
	<li>Terminate a Job when the rows are rejected during loading
<pre>if ( get_file_attribute( 'C:\\TEMP Services\\bin\\STG_CUSTOMER_REJECT.txt', 'size' ) &gt; 0 )
begin
raise_exception_ext( 'Job Terminated Due to Bad Records',1);
end
</pre>
</li>
	<li>Delete a file if exists
<pre>$FileName= 'C:\\LANDING_DIR\\Customer_' || to_char( sysdate( ), 'YYYYMMDD' ) ||  '.csv';
print ( $FileName );

IF ( file_exists ( $FileName ) = 1 )
begin
exec( 'cmd', 'DEL E:\\DWBIC_Files\\FilesProcessed.txt', 8 );
end
else
begin
print( 'File does not exist' );
end
</pre>
</li>
	<li>Wait for a file
<pre>$FileName= 'C:\\LANDING_DIR\\Sales_UK_' || to_char( sysdate( ), 'YYYYMMDD' ) ||  '.csv';
print ( $FileName );

While ( file_exists ( $FileName ) = 0 )
Begin
print( 'Waiting for File' );
Sleep(10000);
End
print ( 'File Received Successfully' );
print ( 'File Processing Started' );
</pre>
</li>
	<li>Print the contents of a file in the Execution log ( Windows )
<pre>print( 'Files Processed: ' );
print( exec( 'cmd', 'TYPE C:\\LANDING_DIR\\FilesProcessed.txt' ) );
</pre>
</li>
	<li>List the XML files and count in a directory
<pre class="">wait_for_file('C:\\LANDING_DIR\\*.xml', 1, 1, -1, $file_name_list, $list_size, ','  );

#PRINT THE FILE NAMES
print( $file_name_list );

#PRINT THE NUMBER OF FILES
print( $list_size );</pre>
</li>
</ol>
