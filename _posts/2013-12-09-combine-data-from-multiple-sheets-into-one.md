---
layout: post
title: Combine data from multiple sheets into One
date: 2013-12-09 09:03
author: administrator
comments: true
categories: [EXCEL]
---
Sub MergeSheets()<br/><br/>' Appends data from all the selected worksheets onto the end of the<br/>' active worksheet.<br/><br/>Const NHR = 1 'Number of header rows to not copy from each MWS<br/><br/>Dim MWS As Worksheet 'Worksheet to be merged (appended)<br/>Dim AWS As Worksheet 'Worksheet to which the data are transferred<br/>Dim FAR As Long 'First available row on AWS<br/>Dim LR As Long 'Last row on the MWS sheets<br/><br/>Set AWS = ActiveSheet<br/><br/>For Each MWS In ActiveWindow.SelectedSheets<br/>If Not MWS Is AWS Then<br/>FAR = AWS.UsedRange.Cells(AWS.UsedRange.Cells.Count).Row + 1<br/>LR = MWS.UsedRange.Cells(MWS.UsedRange.Cells.Count).Row<br/>MWS.Range(MWS.Rows(NHR + 1), MWS.Rows(LR)).Copy AWS.Rows(FAR)<br/>End If<br/>Next MWS<br/><br/>End Sub<br/><br/>To install this macro, go to the VBE (keyboard Alt-TMM), insert a new macro module (Alt-IM), and paste the above code into the Code pane. Before running the macro select all the sheets you want to merge (Ctrl-click on tab). The active worksheet will be the one that was active before selecting the others.<br/><br/>&nbsp;<br/><br/>Reference: http://www.mrexcel.com/forum/excel-questions/62296-combine-data-multiple-sheets-into-just-one.html
