---
layout: post
title: Data Services Metadata Query
date: 2015-10-24 13:37
author: administrator
comments: true
categories: [SAP Data Services]
---
Data Services provides full access to the repository metadata tables and views for metadata analysis. To access this metadata either we can use SQL SELECT statements or use the metadata reporting from Management Console.
<h2>Internal Metadata</h2>
Let us first take a look into a few important internal metadata tables. This set of tables and views capture information about built-in metadata objects used by Data Services and the relationships between those objects.
<h3>1. AL_MACHINE_INFO</h3>
This table contains Data Services Server information like Server Name, Server Group Name, Machine Name, Port etc.
<h3>2. AL_VERSION</h3>
This table contains Data Services Metadata Repository information like Repository Version, Repository Type- <b>central</b>/NULL(local), Secure- ( 1/0 ) etc.
<h3>3. AL_USERS, AL_ASUSERS</h3>
These tables contains Data Services user and administrator information.
<h3>4. AL_REPOTYPE_NAMES</h3>
This static data table contains internal repository object names and their id used by Data Services to identify an object.For example:
<table class="table table-bordered table-striped table-condensed">
<thead>
<tr>
<th>REPOOBJTYPE_ID</th>
<th>REPOOBJTYPE_NAME</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>Plan*</td>
</tr>
<tr>
<td>1</td>
<td>Dataflow</td>
</tr>
<tr>
<td>3</td>
<td>Transform</td>
</tr>
<tr>
<td>4</td>
<td>File</td>
</tr>
<tr>
<td>5</td>
<td>Database Datastore</td>
</tr>
<tr>
<td>7</td>
<td>Table</td>
</tr>
<tr>
<td>8</td>
<td>Column</td>
</tr>
<tr>
<td>10</td>
<td>User</td>
</tr>
<tr>
<td>11</td>
<td>Project</td>
</tr>
<tr>
<td>13</td>
<td>Function</td>
</tr>
<tr>
<td>29</td>
<td>Domain</td>
</tr>
<tr>
<td>36</td>
<td>XML Message</td>
</tr>
<tr>
<td>45</td>
<td>Memory Table</td>
</tr>
</tbody>
</table>
* Job/Workflow
<h3>5. AL_DATATYPE_NAMES</h3>
This static data table contains data type id and names internal to Data Services as below
<table class="table table-bordered table-striped table-condensed">
<thead>
<tr>
<th>DATATYPE_ID</th>
<th>DATATYPE_NAME</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>REAL</td>
</tr>
<tr>
<td>1</td>
<td>FLOAT</td>
</tr>
<tr>
<td>2</td>
<td>DOUBLE</td>
</tr>
<tr>
<td>5</td>
<td>INTEGER</td>
</tr>
<tr>
<td>6</td>
<td>DECIMAL</td>
</tr>
<tr>
<td>9</td>
<td>FIXCSTR</td>
</tr>
<tr>
<td>11</td>
<td>VARCSTR</td>
</tr>
<tr>
<td>13</td>
<td>DATE</td>
</tr>
<tr>
<td>14</td>
<td>TIME</td>
</tr>
<tr>
<td>15</td>
<td>INTERVAL</td>
</tr>
<tr>
<td>16</td>
<td>DATETIME</td>
</tr>
<tr>
<td>21</td>
<td>LONG</td>
</tr>
<tr>
<td>23</td>
<td>TIMESTAMP</td>
</tr>
<tr>
<td>200</td>
<td>NFIXCSTR</td>
</tr>
<tr>
<td>201</td>
<td>NVARCSTR</td>
</tr>
</tbody>
</table>
<h3>6. AL_LANG</h3>
This table contains various Data Services objects information displayed in Data Services object library.( OBJECT GUID )
<table class="table table-bordered table-striped table-condensed">
<thead>
<tr>
<th>Column Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>OBJECT_KEY</td>
<td>Internal ID of the object. UNIQUE for each objects we create in Data Services.</td>
</tr>
<tr>
<td>OBJECT_TYPE</td>
<td>ID for type of object as defined in AL_REPOTYPE_NAMES.</td>
</tr>
<tr>
<td>NAME</td>
<td>Name of the object.</td>
</tr>
<tr>
<td>GUID</td>
<td>Globally Unique Identifiers or Universal Unique Identifier (UUID) of the object.</td>
</tr>
<tr>
<td>NORMNAME</td>
<td>Unique name for this object in this table.</td>
</tr>
<tr>
<td>VERSION</td>
<td>Indicates the number of times this object has been updated.</td>
</tr>
<tr>
<td>TYPE</td>
<td>Subtype of the object.*</td>
</tr>
<tr>
<td>OWNER</td>
<td>For table objects, the owner.</td>
</tr>
<tr>
<td>DATASTORE</td>
<td>For table objects, the datastore to which they belong.</td>
</tr>
</tbody>
</table>
* Integer value 1 for Workflow and 0 for all other object types.

<b>NOTE:</b> Other important columns namely CHECKOUT_DT, CHECKOUT_REPO, CHECKIN_DT, CHECKIN_REPO, LABEL_DT, LABEL, COMMENTS, SEC_USER, SEC_USER_COUT are NULL for Local repositories but are relevant for Central repositories and they maintain the Version Control information.
<pre class="brush: sql">SELECT 
OBJECT_KEY, OBJECT_TYPE, NAME, GUID, NORMNAME,
VERSION, TYPE, OWNER, DATASTORE, STATE, LANGSIZE, 
CHECKOUT_DT, CHECKOUT_REPO, CHECKIN_DT, CHECKIN_REPO,
LABEL_DT, LABEL, COMMENTS, SEC_USER, SEC_USER_COUT
FROM AL_LANG
</pre>
Also this metadata table does not holds information for tables within Data stores. They are maintained on other views or tables like <b>ALVW_OBJ_CINOUT</b> or <b>AL_SCHEMA</b>.

Some related tables- <b>AL_LANGTEXT</b>, <b>AL_LANGXMLTEXT</b> which contains the text and XML representation of the objects.

Also check the Table <b>AL_ATTR</b>, which contains attributes of repository objects like description etc.

<b>Query 1:</b> The following query returns all the user defined <b>Jobs</b> in a data services repository.
Note: Here we are interested to get the Job name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "JOB NAME" 
FROM AL_LANG A 
WHERE A.OBJECT_TYPE = 0 AND A.TYPE = 0
AND A.VERSION = (
SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE A.NORMNAME = B.NORMNAME )
AND A.NAME NOT IN( 'CD_JOB_d0cafae2', 'di_job_al_mach_info' )
ORDER BY A.NAME
</pre>
<b>Query 2:</b> The following query returns all the user defined <b>Workflows</b> in a data services repository.
Note: Here we are interested to get the Workflow name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "WORKFLOW NAME" 
FROM AL_LANG A 
WHERE A.OBJECT_TYPE = 0 AND A.TYPE = 1
AND A.VERSION = (
SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE A.NORMNAME = B.NORMNAME )
ORDER BY A.NAME
</pre>
<b>Query 3:</b> The following query returns all the user defined <b>Dataflows</b> in a data services repository.
Note: Here we are interested to get the Dataflow name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "DATAFLOW NAME" 
FROM AL_LANG A 
WHERE A.OBJECT_TYPE = 1
AND A.VERSION = (
SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE A.NORMNAME = B.NORMNAME )
AND A.NAME NOT IN( 'CD_DF_d0cafae2', 'di_df_al_mach_info' )
ORDER BY A.NAME
</pre>
<b>Query 4:</b> The following query returns all the user defined <b>Datastores</b> in a data services repository.
Note: Here we are interested to get the Datastore name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "DATA STORE NAME" 
FROM AL_LANG A 
WHERE A.OBJECT_TYPE = 5
AND A.VERSION = (
SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE A.NORMNAME = B.NORMNAME )
AND A.NAME &lt;&gt; 'CD_DS_d0cafae2'
ORDER BY A.NAME
</pre>
<b>Query 5:</b> The following query returns all the user defined <b>flatfile formats</b> in a data services repository.
Note: Here we are interested to get the flatfile formats name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "FILE FORMAT NAME" 
FROM AL_LANG A 
WHERE A.OBJECT_TYPE = 4
AND A.VERSION = (
SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE A.NORMNAME = B.NORMNAME )
AND A.NAME NOT IN( 'Transport_Format', 'di_ff_al_mach_info' )
ORDER BY A.NAME
</pre>
<b>Query 6:</b> The following query returns all the user defined <b>XML definitions</b> in a data services repository.
Note: Here we are interested to get the XML schema name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "XML SCHEMA NAME" 
FROM AL_LANG A 
WHERE A.OBJECT_TYPE = 36
AND A.VERSION = (
SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE A.NORMNAME = B.NORMNAME )
ORDER BY A.NAME
</pre>
Using <b>AL_ATTR</b> table to get attributes of repository objects

<b>Query 7:</b> The following query returns all the <b>Data flow</b> names along with their dataflow <b>Description attributes</b> if any, in the repository:
<pre class="brush: sql">SELECT DISTINCT O.OBJECT_KEY, O.NAME, 
CASE WHEN A.PARENT_OBJ_TYPE = 1 THEN A.ATTR_VALUE ELSE NULL END
FROM AL_LANG O LEFT OUTER JOIN <b>AL_ATTR</b> A
ON O.OBJECT_KEY = A.PARENT_OBJID  
WHERE O.OBJECT_TYPE = 1 
AND A.ATTR_NAME = 'Description' 
AND O.VERSION = ( SELECT MAX(B.VERSION) FROM AL_LANG B 
WHERE O.NORMNAME = B.NORMNAME )
AND O.NAME NOT IN ( 'CD_DF_d0cafae2', 'di_df_al_mach_info' )
ORDER BY 2
</pre>
<h3>7. AL_SETOPTIONS</h3>
This table contains option settings for all repository objects.
<table class="table table-bordered table-striped table-condensed">
<thead>
<tr>
<th>Column Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>PARENT_OBJ_ID</td>
<td>ID of the parent object to which this option belongs.</td>
</tr>
<tr>
<td>PARENT_OBJ_TYPE</td>
<td>ID for type of object as defined in AL_REPOTYPE_NAMES.</td>
</tr>
<tr>
<td>OPTION_NAME</td>
<td>Name of the option.</td>
</tr>
<tr>
<td>OPTION_VALUE</td>
<td>Value of the option.</td>
</tr>
<tr>
<td>OVERFLOW_KEY</td>
<td>KEY value pointing to a row in the <b>AL_OVERFLOW_ATTR</b> table. When an OPTION_VALUE exceeds 255 characters, Data Services adds the remaining characters to AL_OVERFLOW_ATTR and stores the row ID as OVERFLOW_KEY in the AL_SETOPTIONS table.</td>
</tr>
</tbody>
</table>
Also check the related table <b>AL_OVERFLOW_ATTR</b>.

<b>Query 8</b>: The following query returns all the user defined <b>Jobs</b> with their execution properties/options in a data services repository.
Note: Here we are interested to get the Job name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "JOB NAME",B.OPTION_NAME, 
B.OPTION_VALUE, B.OVERFLOW_KEY 
FROM AL_LANG A, AL_SETOPTIONS B
WHERE A.OBJECT_KEY = B.PARENT_OBJID
AND B.PARENT_OBJTYPE = 0 AND A.TYPE = 0
AND A.VERSION = (
SELECT MAX(C.VERSION) FROM AL_LANG C 
WHERE A.NORMNAME = C.NORMNAME )
AND A.NAME NOT IN( 'CD_JOB_d0cafae2', 'di_job_al_mach_info' )
ORDER BY A.NAME, B.OPTION_NAME
</pre>
<b>Query 9:</b> The following query returns all the user defined <b>Workflows</b> with their properties/options in a data services repository.
Note: Here we are interested to get the Workflow name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "WORKFLOW NAME",B.OPTION_NAME, 
B.OPTION_VALUE, B.OVERFLOW_KEY 
FROM AL_LANG A, AL_SETOPTIONS B
WHERE A.OBJECT_KEY = B.PARENT_OBJID
AND B.PARENT_OBJTYPE = 0 AND A.TYPE = 1
AND A.VERSION = (
SELECT MAX(C.VERSION) FROM AL_LANG C 
WHERE A.NORMNAME = C.NORMNAME )
ORDER BY A.NAME, B.OPTION_NAME
</pre>
<b>Query 10:</b> The following query returns all the user defined <b>Dataflows</b> with their properties/options in a data services repository.
Note: Here we are interested to get the Dataflow name for the latest version. Query works in central repository to fetch the latest version of the object.
<pre class="brush: sql">SELECT A.NAME AS "DATAFLOW NAME",B.OPTION_NAME, 
B.OPTION_VALUE, B.OVERFLOW_KEY 
FROM AL_LANG A, AL_SETOPTIONS B
WHERE A.OBJECT_KEY = B.PARENT_OBJID
AND B.PARENT_OBJTYPE = 1 
AND A.VERSION = (
SELECT MAX(C.VERSION) FROM AL_LANG C 
WHERE A.NORMNAME = C.NORMNAME )
AND A.NAME NOT IN( 'CD_DF_d0cafae2', 'di_df_al_mach_info' )
ORDER BY A.NAME, B.OPTION_NAME
</pre>
Similarly, modify the above query, PARENT_OBJTYPE value to 4 or 5 or 36 to get the property informations for File Formats, Data Stores and XML Schemas correspondingly.
<h3>8. AL_USAGE</h3>
This table contains information about objects (parents) that contain (or call) other objects (children). This table is identical to view <b>ALVW_PARENT_CHILD</b> except it captures the entire call hierarchy. For example, if a table is used in a dataflow which is called from a workflow, then rows appear in this table that associate the workflow (parent) to the table (descendant). The Depth column is unique to this table which indicates the number of levels between objects in a parent/descendant relationship.

<b>Note:</b> We need to populate this table explicitly by using the <b>Calculate Usage Dependencies</b> command. From Data Services Designer go to Tools &gt; Options &gt; Designer &gt; General and enable the 'Automatically calculate column mappings' option while saving Dataflow. Else from Management Console go to Impact and Lineage Analysis -&gt; Settings -&gt; Refresh Usage Data -&gt; Calculate Column Mapping.

Alternatively, from Local Object Library, select the dataflow right-click and select Repository -&gt; Calculate Usage Dependencies and Calculate Column Mappings.

<b>ALVW_PARENT_CHILD</b> view contains information about objects (parents) that contain (or call) other objects (children).
<table class="table table-bordered table-striped table-condensed">
<thead>
<tr>
<td>Column Name</td>
<td>Description</td>
</tr>
</thead>
<tbody>
<tr>
<td>PARENT_OBJ</td>
<td>Name of the calling object.</td>
</tr>
<tr>
<td>PARENT_OBJ_TYPE</td>
<td>Type of the object (Job or dataflow etc.).</td>
</tr>
<tr>
<td>PARENT_OBJ_DESC</td>
<td>The description associated with this object.</td>
</tr>
<tr>
<td>PARENT_OBJ_KEY</td>
<td>Key in the <b>AL_LANG</b> table of the parent object.</td>
</tr>
<tr>
<td>DESCEN_OBJ</td>
<td>Name of the descendant object. For transforms, the name of the output schema of the transform call (if the name of the transform is unique). If it is not unique, Data Services generates a unique numeric suffix and appends that to the given name.</td>
</tr>
<tr>
<td>DESCEN_OBJ_TYPE</td>
<td>Type of the called object (Dataflow, table, function, file etc.).</td>
</tr>
<tr>
<td>DESCEN_OBJ_DESC</td>
<td>Description associated with the called object.</td>
</tr>
<tr>
<td>DESCEN_OBJ_KEY</td>
<td>Key in <b>AL_LANG</b> of the descendant object.</td>
</tr>
<tr>
<td>DESCEN_OBJ_USAGE</td>
<td>This identifies how the child is used- Source, Target, Lookup table.</td>
</tr>
<tr>
<td>DESCEN_OBJ_DS</td>
<td>This is applicable only to tables and files to identify the datastore of the child object.</td>
</tr>
<tr>
<td>DESCEN_OBJ_OWNER</td>
<td>Owner of the child table.</td>
</tr>
<tr>
<td>DEPTH</td>
<td>Indicates the number of levels between objects in a parent/descendant relationship as integer value.</td>
</tr>
</tbody>
</table>
<b>Query 11:</b> The following query returns all the user defined <b>Jobs</b> with their corresponding <b>Target tables</b>they populate in a data services repository.
<pre class="brush: sql">SELECT 
AL_USAGE.PARENT_OBJ,
AL_USAGE.PARENT_OBJ_DESC,
AL_USAGE.PARENT_OBJ_TYPE,
AL_USAGE.DESCEN_OBJ,
AL_USAGE.DESCEN_OBJ_DESC,
AL_USAGE.DESCEN_OBJ_TYPE,
AL_USAGE.DESCEN_OBJ_USAGE,
AL_USAGE.DESCEN_OBJ_DS,
AL_USAGE.DESCEN_OBJ_OWNER,
AL_USAGE.DEPTH
FROM AL_USAGE
WHERE AL_USAGE.PARENT_OBJ_TYPE = 'Job'
AND AL_USAGE.DESCEN_OBJ_TYPE = 'Table'
AND AL_USAGE.DESCEN_OBJ_USAGE = 'Target'
</pre>
<b>IMPORTANT NOTES</b>

In order to check for the Job name that populates a particular Target table, use additional filter clause as AL_USAGE.DESCEN_OBJ = '[Target Table Name]'. Alternatively if we want to check the Target tables being loaded by a particular Job use filter clause as AL_USAGE.PARENT_OBJ = '[Job Name]'.

Similarly, to find out the Tables being used as Source or Lookups or in Table Comparison in a Job, modify the AL_USAGE.DESCEN_OBJ_USAGE to <b>'Source'</b> or <b>'Lookup_ext()'</b> or <b>'Comparison'</b> accordingly.

Again in order to identify the tables being used in Key_Generation transform in a Job, modify the AL_USAGE.DESCEN_OBJ_USAGE to <b>'Key Generation'</b>. So all the above cases are valid when the descendant object type is datastores or files.
( AL_USAGE.DESCEN_OBJ_TYPE = 'Datastore' or 'Table' or 'File Datastore' or 'XML Datastore' or'File' )

<b>Query 12:</b> The following query returns all the user defined <b>Dataflows</b> with their corresponding <b>Target tables</b> they populate in a data services repository.
<pre class="brush: sql">SELECT 
AL_USAGE.PARENT_OBJ,
AL_USAGE.PARENT_OBJ_DESC,
AL_USAGE.PARENT_OBJ_TYPE,
AL_USAGE.DESCEN_OBJ,
AL_USAGE.DESCEN_OBJ_DESC,
AL_USAGE.DESCEN_OBJ_TYPE,
AL_USAGE.DESCEN_OBJ_USAGE,
AL_USAGE.DESCEN_OBJ_DS,
AL_USAGE.DESCEN_OBJ_OWNER,
AL_USAGE.DEPTH
FROM AL_USAGE
WHERE AL_USAGE.PARENT_OBJ_TYPE = 'Dataflow'
AND AL_USAGE.DESCEN_OBJ_TYPE = 'Table'
AND AL_USAGE.DESCEN_OBJ_USAGE = 'Target'
</pre>
<b>IMPORTANT NOTES</b>

In order to check for the Dataflow name that populates a particular Target table, use additional filter clause as AL_USAGE.DESCEN_OBJ = '[Target Table Name]'. Alternatively if we want to check the Target tables being associated with a particular Dataflow use filter clause as AL_USAGE.PARENT_OBJ = '[Dataflow Name]'.

Similarly, to find out the Tables being used as Source or Lookups or in Table Comparison in a Dataflow, modify the AL_USAGE.DESCEN_OBJ_USAGE to <b>'Source'</b> or <b>'Lookup_ext()'</b> or <b>'Comparison'</b> accordingly.

Again in order to identify the tables being used in Key_Generation transform in a Dataflow, modify the AL_USAGE.DESCEN_OBJ_USAGE to <b>'Key Generation'</b>. So all the above cases are valid when the descendant object type is datastores or files.
( AL_USAGE.DESCEN_OBJ_TYPE = 'Datastore' or 'Table' or 'File Datastore' or 'XML Datastore' or'File' )

Let us create a table with possible list of values for <b>PARENT_OBJ_TYPE</b>, <b>DESCEN_OBJ_TYPE</b> and<b>DESCEN_OBJ_USAGE</b> for quick reference.
<table class="table table-bordered table-striped table-condensed">
<thead>
<tr>
<td>PARENT_OBJ_TYPE</td>
<td>DESCEN_OBJ_TYPE</td>
<td>DESCEN_OBJ_USAGE</td>
</tr>
</thead>
<tbody>
<tr>
<td>Job</td>
<td>WorkFlow</td>
<td>Source</td>
</tr>
<tr>
<td>WorkFlow</td>
<td>DataFlow</td>
<td>Target</td>
</tr>
<tr>
<td>DataFlow</td>
<td>Datastore</td>
<td>Lookup_ext()</td>
</tr>
<tr>
<td>SDK Transform</td>
<td>File Datastore</td>
<td>Comparison</td>
</tr>
<tr>
<td></td>
<td>XML Datastore</td>
<td>Key Generation</td>
</tr>
<tr>
<td></td>
<td>File</td>
<td>NULL</td>
</tr>
<tr>
<td></td>
<td>Transform</td>
<td>Transform</td>
</tr>
<tr>
<td></td>
<td>SDK Transform</td>
<td>SDK Transform</td>
</tr>
</tbody>
</table>
<b>Query 13:</b> The following query returns all the objects (Job/Worflow/Dataflow) that would be affected if we drop a Target table or to find <b>Object Dependencies</b>. This is used to produce a <b>WHERE USED</b> report for an object.
<pre class="brush: sql">SELECT 
AL_USAGE.PARENT_OBJ,
AL_USAGE.PARENT_OBJ_DESC,
AL_USAGE.PARENT_OBJ_TYPE,
AL_USAGE.DESCEN_OBJ,
AL_USAGE.DESCEN_OBJ_DESC,
AL_USAGE.DESCEN_OBJ_TYPE,
AL_USAGE.DESCEN_OBJ_USAGE,
AL_USAGE.DESCEN_OBJ_DS,
AL_USAGE.DESCEN_OBJ_OWNER,
AL_USAGE.DEPTH
FROM AL_USAGE
WHERE AL_USAGE.DESCEN_OBJ_TYPE = 'Table'
AND AL_USAGE.DESCEN_OBJ = '[Target Table Name]'
</pre>
Related Table <b>AL_PARENT_CHILD</b> or View <b>ALVW_PARENT_CHILD</b> contains information about objects (parents) that contain (or call) other objects (children).

<b>Query 14:</b> The following query returns the user defined <b>Dataflows</b> that populates a particular <b>Target table</b>.
<pre class="brush: sql">SELECT 
PARENT_OBJ,
PARENT_OBJ_DESC,
PARENT_OBJ_TYPE,
DESCEN_OBJ,
DESCEN_OBJ_DESC,
DESCEN_OBJ_TYPE,
DESCEN_OBJ_USAGE,
DESCEN_OBJ_DS,
DESCEN_OBJ_OWNER 
FROM AL_PARENT_CHILD 
WHERE DESCEN_OBJ_TYPE = 'Table' 
AND DESCEN_OBJ = '[Target Table Name]' 
AND DESCEN_OBJ_USAGE = 'Target'
</pre>
Alternatively, we can use the same query with View <b>ALVW_PARENT_CHILD</b>.

<b>Query 15:</b> The following query returns the user defined <b>Dataflows</b> associated with a particular <b>Job</b>.
<pre class="brush: sql">SELECT 
PARENT_OBJ,
PARENT_OBJ_DESC,
PARENT_OBJ_TYPE,
DESCEN_OBJ,
DESCEN_OBJ_DESC,
DESCEN_OBJ_TYPE,
DESCEN_OBJ_USAGE,
DESCEN_OBJ_DS,
DESCEN_OBJ_OWNER 
FROM AL_PARENT_CHILD 
WHERE PARENT_OBJ_TYPE = 'Job' 
AND PARENT_OBJ = '[Job Name]' 
AND DESCEN_OBJ_TYPE = 'Dataflow'
</pre>
Alternatively, we can use the same query with View <b>ALVW_PARENT_CHILD</b>.
