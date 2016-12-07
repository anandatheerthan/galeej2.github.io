---
layout: post
title: SQL User Defined Function to Parse a Delimited String
date: 2016-02-14 03:21
author: administrator
comments: true
categories: [SQL Server]
---
<pre class="lang:mysql decode:true">SET QUOTED_IDENTIFIER OFF 
GO
SET ANSI_NULLS OFF 
GO
create   function fn_ParseText2Table 
 (
 @p_SourceText  varchar(8000)
 ,@p_Delimeter varchar(100) = ',' --default to comma delimited.
 )
RETURNS @retTable TABLE 
 (
  Position  int identity(1,1)
 ,Int_Value int 
 ,Num_value Numeric(18,3)
 ,txt_value varchar(2000)
 )
AS
BEGIN
 DECLARE @w_Continue  int
  ,@w_StartPos  int
  ,@w_Length  int
  ,@w_Delimeter_pos int
  ,@w_tmp_int  int
  ,@w_tmp_num  numeric(18,3)
  ,@w_tmp_txt   varchar(2000)
  ,@w_Delimeter_Len tinyint
 if len(@p_SourceText) = 0
 begin
  SET  @w_Continue = 0 -- force early exit
 end 
 else
 begin
 -- parse the original @p_SourceText array into a temp table
  SET  @w_Continue = 1
  SET @w_StartPos = 1
  SET @p_SourceText = RTRIM( LTRIM( @p_SourceText))
  SET @w_Length   = DATALENGTH( RTRIM( LTRIM( @p_SourceText)))
  SET @w_Delimeter_Len = len(@p_Delimeter)
 end
 WHILE @w_Continue = 1
 BEGIN
  SET @w_Delimeter_pos = CHARINDEX( @p_Delimeter
      ,(SUBSTRING( @p_SourceText, @w_StartPos
      ,((@w_Length - @w_StartPos) + @w_Delimeter_Len)))
      )
 
  IF @w_Delimeter_pos &gt; 0  -- delimeter(s) found, get the value
  BEGIN
   SET @w_tmp_txt = LTRIM(RTRIM( SUBSTRING( @p_SourceText, @w_StartPos 
        ,(@w_Delimeter_pos - 1)) ))
   if isnumeric(@w_tmp_txt) = 1
   begin
    set @w_tmp_int = cast( cast(@w_tmp_txt as numeric) as int)
    set @w_tmp_num = cast( @w_tmp_txt as numeric(18,3))
   end
   else
   begin
    set @w_tmp_int =  null
    set @w_tmp_num =  null
   end
   SET @w_StartPos = @w_Delimeter_pos + @w_StartPos + (@w_Delimeter_Len- 1)
  END
  ELSE -- No more delimeters, get last value
  BEGIN
   SET @w_tmp_txt = LTRIM(RTRIM( SUBSTRING( @p_SourceText, @w_StartPos 
      ,((@w_Length - @w_StartPos) + @w_Delimeter_Len)) ))
   if isnumeric(@w_tmp_txt) = 1
   begin
    set @w_tmp_int = cast( cast(@w_tmp_txt as numeric) as int)
    set @w_tmp_num = cast( @w_tmp_txt as numeric(18,3))
   end
   else
   begin
    set @w_tmp_int =  null
    set @w_tmp_num =  null
   end
   SELECT @w_Continue = 0
  END
  INSERT INTO @retTable VALUES( @w_tmp_int, @w_tmp_num, @w_tmp_txt )
 END
RETURN
END
GO
SET QUOTED_IDENTIFIER OFF 
GO
SET ANSI_NULLS ON 
GO</pre>
&nbsp;
<h2>Usage Examples:</h2>
<h3>Single Character Delimiter</h3>
<pre class="lang:mysql decode:true ">select * from dbo.fn_ParseText2Table('100|120|130.56|Yes|Cobalt Blue','|')</pre>
&nbsp;
<pre class="lang:mysql decode:true ">/*
Position    Int_Value   Num_value            txt_value 
----------- ----------- -------------------- --------------
1           100         100.000              100
2           120         120.000              120
3           131         130.560              130.56
4           NULL        NULL                 Yes
5           NULL        NULL                 Cobalt Blue
*/</pre>
&nbsp;
<h3>Multi-Character Delimiter</h3>
<div id="premain72022" class="pre-action-link"><span id="prehide72022">Hide</span>   Copy Code</div>
<pre class="lang:mysql decode:true ">select * from dbo.fn_ParseText2Table('Red, White, and, Blue',', ')</pre>
<div id="premain273569" class="pre-action-link"><span id="prehide273569"> </span></div>
<pre class="lang:mysql decode:true ">/*
Position    Int_Value   Num_value            txt_value 
----------- ----------- -------------------- ----------
1           NULL        NULL                 Red
2           NULL        NULL                 White
3           NULL        NULL                 and
4           NULL        NULL                 Blue 
*/</pre>
&nbsp;
<h3>Big Multi-Character Delimiter</h3>
<div id="premain298873" class="pre-action-link"><span id="prehide298873">Hide</span>   Copy Code</div>
<pre class="lang:mysql decode:true ">select * from dbo.fn_ParseText2Table('Red&lt;Tagname&gt;White&lt;Tagname&gt;Blue','&lt;Tagname&gt;')</pre>
<div id="premain496589" class="pre-action-link"><span id="prehide496589"> </span></div>
<pre class="lang:mysql decode:true ">/* 
Position    Int_Value   Num_value            txt_value 
----------- ----------- -------------------- ----------
1           NULL        NULL                 Red
2           NULL        NULL                 White
3           NULL        NULL                 and
4           NULL        NULL                 Blue 
*/</pre>
&nbsp;

Unfortunately, the only way to use this to process multiple rows is using a cursor.

Here is an example of what the code inside the cursor block would look like to insert parsed values from a string as rows in a child table
<h3>As a table in an insert statement:</h3>
<pre class="lang:mysql decode:true ">create table #tmp_Child (parent_id int, ColorSelection varchar(30), SelOrder tinyint)
declare @parent_id int
 ,@ColorSelections varchar(255)
 ,@delim varchar(100) 
set @parent_id = 122
set @ColorSelections = 'Red, White, and, Blue'
set @delim = ', ' 


-- cursor block starts here
insert #tmp_Child (parent_id, ColorSelection, SelOrder)
select @parent_id
 ,t.txt_value
 ,t.position
from dbo.fn_ParseText2Table(@ColorSelections, @delim) as t 
-- cursor block ends here
select * from #tmp_child 
drop table #tmp_child</pre>
&nbsp;
