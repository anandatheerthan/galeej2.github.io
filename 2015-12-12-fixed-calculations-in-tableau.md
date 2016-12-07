---
layout: post
title: Fixed Calculations in Tableau
date: 2015-12-12 10:10
author: administrator
comments: true
categories: [Reporting]
---
Tableau makes it really easy to switch from showing absolute figures to a percent of total figure by using the Quick Table Calculation option. However, if you want to filter out one or more of your dimensions, the percent of total figure changes because the ‘total’ which is used in the computation changes too to reflect the loss of the dimension members. In some cases, you will want to maintain the original percentage (of the whole underlying data) whilst just displaying the dimension members you are interested in. This post examines 4 different ways to accomplish this.

Filter using table calculations
<pre class="lang:r decode:true ">LOOKUP( MIN( [Region] ), 0)</pre>
Duplicate Data

You can achieve this by duplicating data source and using data blending. Simple use the measure you want unchanged from the duplicated data source.

Using SQL

You can use RAWSQL functions to send query directly to database and get the values. However this will not work with extracts.

Fixed Function

Tableau 9 introduced Fixed function by which you can get fixed values after aggregation based on certain dimensions that are not affected by filters.
