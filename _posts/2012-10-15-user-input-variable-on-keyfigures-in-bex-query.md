---
layout: post
title: User input variable on Keyfigures in BEx Query
date: 2012-10-15 12:32
author: administrator
comments: true
categories: [SAP BW]
---
There are scenarios you might want to create an user input variable for key figures in BEx instead of traditional variables for characteristics.Below are simple steps to achieve it.<br/><h6>1) Open BEx query designer and open the required or create new query.</h6><br/><h5>2) Drag &amp; Drop the key figure you would like to create a variable onto "Columns" pane.</h5><br/><h6>3) You may/maynot show the key figure necessarily in the query output.</h6><br/><h5>4) Activate "Conditions" using the toolbar in BEx designer.</h5><br/><h5>5) RIght-click and create new condition.</h5><br/><h5>6) Add key figure to the new condition created</h5><br/><h5>7) The bottom pane in condition window will provide you with various options to define the condition criteria.</h5><br/><h5>8) Choose the required criteria such as "Equal" or "Between" or "greater than".</h5><br/><h5>9) Then in the input box where you put the actual value, instead choose the variable icon and create/choose a variable.</h5><br/><h5>10) This will enable to popup a variable in the variable screen where users can input any value to that keyfigure.</h5><br/><h5>11) Remember that these variable are only single input values and not multiple value entry.If you choose criteria as "between", then you need to create 2 variables for "Low" and "high" values.</h5>
