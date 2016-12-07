---
layout: post
title: How to calculate rank in MySQL
date: 2014-10-29 10:13
author: administrator
comments: true
categories: [MySql]
---
Many a time you need to calculate rank in MySQL. You can <a href="http://www.w3schools.com/sql/sql_orderby.asp">order by a number or text</a> but can’t calculate rank in MySQL easily. Here’s a query you can use. Just replace the table name <em><strong>scores</strong></em> and column names <em><strong>id, score.</strong></em><span id="more-829"></span>

<a href="http://blog.ubiq.co/wp-content/uploads/2013/12/ranking.jpg"><img class="aligncenter size-full wp-image-865" src="http://blog.ubiq.co/wp-content/uploads/2013/12/ranking.jpg" alt="calculate rank in mysql" width="500" height="300" /></a>
<h2>Calculate rank in MySQL based on increasing value</h2>
<strong>Example:</strong>
<pre>CREATE TABLE score (id int, score int);
INSERT INTO scores VALUES (1, 35),(2, 10),(3,30),(4,22),(5,20),(6,18),(7,36);
Scores:
+----+------+
| id | score|
+----+------+
| 1  |   35 |
| 2  |   10 |
| 3  |   30 |
| 4  |   22 |
| 5  |   20 |
| 6  |   18 |
| 7  |   36 |
+----+------+</pre>
We use a ranking variable, such as the following:
<pre>SELECT    id,score,
          @curRank := @curRank + 1 AS rank
FROM      scores p, (SELECT @curRank := 0) r
ORDER BY  score;</pre>
The
<pre>(SELECT @curRank := 0)</pre>
part allows the variable initialization without requiring a separate SET command.
<pre>Result:
+----+------+------+
| id | score| rank |
+----+------+------+
| 2  |   10 |    1 |
| 6  |   18 |    2 |
| 5  |   20 |    3 |
| 4  |   22 |    4 |
| 3  |   30 |    5 |
| 1  |   35 |    6 |
| 7  |   36 |    7 |
+----+------+------+
7 rows in set (0.02 sec)</pre>
<h2>Calculate rank in MySQL based on decreasing value</h2>
If you want to calculate rank in MySQL based on decreasing order of scores just add the keyword DESC in query.
<pre>SELECT    id,score,
          @curRank := @curRank + 1 AS rank
FROM      scores p, (SELECT @curRank := 0) r
ORDER BY  score DESC;</pre>
Result:
<pre>+----+------+------+
| id | score| rank |
+----+------+------+
| 7  |   36 |    1 |
| 1  |   35 |    2 |
| 3  |   30 |    3 |
| 4  |   22 |    4 |
| 5  |   20 |    5 |
| 6  |   18 |    6 |
| 2  |   10 |    7 |
+----+------+------+
7 rows in set (0.02 sec)</pre>
