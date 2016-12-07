---
layout: post
title: Convert filename to Uppercase
date: 2015-09-11 04:17
author: administrator
comments: true
categories: [Tools]
---
Type everything between the lines into notepad:

----------------------------------------------------------------------------
set fso = createobject("scripting.filesystemobject")
Function GetPath
path = WScript.ScriptFullName
GetPath = Left(path, InstrRev(path, "\"))
End Function
path2 = GetPath
folder = Left(path2, (Len(path2)-1))
set folder = fso.GetFolder(folder)
set files = folder.Files
s = ""
vCount = 0
for each file in files
vCount = vCount + 1
ReDim Preserve arFiles(vCount)
Set arFiles(vCount) = file
tempfilename = UCase(arFiles(vCount).name)
file.name = "temp" &amp; vCount
file.name = tempfilename
next
-----------------------------------------------------------------------------

Save as UpperCaps.vbs

Put the vbs file into the same folder as the files.
Double-click to run the vbs file.
You may have to refresh the folder view to see the changes.
