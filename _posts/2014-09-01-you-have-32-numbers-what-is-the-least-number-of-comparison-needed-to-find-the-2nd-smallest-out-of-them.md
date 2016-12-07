---
layout: post
title: You have 32 numbers. What is the least number of comparison needed to find the 2nd smallest out of them?
date: 2014-09-01 03:21
author: administrator
comments: true
categories: [Logic]
---
<p dir="ltr">Minimum number of comparisons required will be n + log(n) -2 = 32 + 5 -2 = 35<br /><b>How?</b><br />We can think of this as a tournament where 32 teams are competing against each other, to get the best team out of n teams we need (n-1) comparisons, by taking two teams at a time and then playing the game between the previous winners, Games will be played in the tree format as below</p><p dir="ltr">| | | | | | | | | | | | | | | </p><p dir="ltr">Now we need to find the second best team: We can say that second best team must have lost against the winner(as otherwise it will not be second). And Total number of games played by the winner are log(n) (height of the tree).<br />Now our task reduces to just finding the best team from log(n) teams, which we know can be done in log(n) &#8211; 1 times.</p><p dir="ltr">So total number of comparisons = n-1 + log(n) -1 = n + log(n) -2.</p><p dir="ltr">http://stackoverflow.com/questions/3628718/find-the-2nd-largest-element-in-an-array-with-minimum-of-comparisom<br /></p>
