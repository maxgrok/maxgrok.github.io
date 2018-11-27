---
title: "SQL Crowdfunding Lab"
date: "2017-01-01T12:46:37.121Z"
layout: post
draft: false
path: "/posts/eighth-post/"
category: "Flatiron School"
tags:
  - "SQL"
  - "Queries"
description: "This is a post about a SQL lab for the Flatiron School."
---
Happy New Year! 

In this assignment, I was tasked with building a database schema, creating the UML/ERD, inserting data, writing complex join queries, and writing complex queries for the data in SQLite3 using the command line or an SQL browser such as Base for a series of crowdfunding campaigns. 

First, I created the schema by creating the tables the database required: <br><br>

{% highlight ruby %}
CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER);
CREATE TABLE projects(id INTEGER PRIMARY KEY, title TEXT, category TEXT, funding_goal
INTEGER, start_date TEXT, end_date TEXT);
CREATE TABLE pledges (id INTEGER PRIMARY KEY, amount INTEGER, user_id INTEGER, 
project_id INTEGER);
{% endhighlight %}

Second, I made a UML/ERD (Entity-relationship Diagram) to express the table data and relationships between the data with Gliffy, which is a free diagraming cloud software. 

![My helpful screenshot]({{ site.url }}/img/screenshot2.png)	

Third, I inserted the data using INSERT INTO. I overall added 20 users, 10 projects, and 30 pledges to the database. For example: 

Inserting into the users table: <br>
``` INSERT INTO users (id, name, age) VALUES (1, 'Finnebar', 17)```<br>

Inserting into the projects table: <br>
``` INSERT INTO projects (id, title, category, funding_goal, start_date, end_date) VALUES
(1, 'Help me buy a guitar', 'music', 500.00, '2013-06-30', '2013-07-30') ```<br>

Inserting into the pledges table:<br>
```INSERT INTO pledges (id, amount, user_id, project_id) VALUES
(1, 10.00, 1, 2)```<br>

Fourth, I created the database and used the < operator to insert the schema and the seed data into the database called sql_lib.db. 

Fifth, I started on the queries, which can be found below. 

{% highlight ruby %}
def selects_the_titles_of_all_projects_and_their_pledge_amounts
"SELECT Projects.title, SUM(amount) FROM projects, pledges GROUP BY pledges.project_id, 
Projects.title HAVING Projects.id = pledges.project_id ORDER BY projects.title ASC;" 
end

def selects_the_user_name_age_and_pledge_amount_for_all_pledges
"SELECT users.name,users.age,SUM(amount) FROM users, pledges 
ON pledges.user_id = users.id 
GROUP BY pledges.user_id ORDER BY name;"
end

def selects_the_titles_and_amount_over_goal_of_all_projects_that_have_
met_their_funding_goal
"SELECT Projects.title, SUM(amount) - Projects.funding_goal FROM projects, pledges 
WHERE pledges.project_id = projects.id GROUP BY Projects.title 
HAVING projects.id = pledges.project_id ORDER BY SUM(amount), 
Projects.funding_goal > -1 DESC LIMIT 2;"
end

def selects_user_names_and_amounts_of_all_pledges_grouped_by_name_then_orders_them
_by_the_amount 
"SELECT Users.name, SUM(amount) FROM pledges INNER JOIN users 
ON pledges.user_id = users.id 
GROUP BY users.name ORDER BY SUM(amount) ASC;"
end
def selects_the_category_names_and_pledge_amounts_of_all_pledges_in_the_music_category 
"SELECT projects.category, pledges.amount FROM pledges LEFT JOIN projects 
ON pledges.project_id = projects.id WHERE projects.category = 'music';" 
end
def selects_the_category_name_and_the_sum_total_of_the_all_its_pledges_for_the
_book_category
"SELECT projects.category, SUM(amount) FROM pledges LEFT JOIN projects 
ON pledges.project_id = projects.id 
GROUP BY projects.category HAVING projects.category = 'books';" 
end
{% endhighlight %}
I found each query by placing the database in sqlite3 and testing out queries in the command line. 
To find the first query, I selected the title column from Projects table as well as the sum of the amount column from Pledges table to be grouped by the Pledges' project id and Projects' title. I specified this to be only as long as the id of Projects is equal to the Pledges project_id, ordered by the Projects' title in ascending order. This means that the query will select all the titles of the projects and their pledge amounts. 
To find the last query, I selected the category column of the Projects table as well as the sum of the amount column from Pledges table to left join the Projects table on the Pledges table where the Pledges' table's project id is to equal the Projects table's id column. I specified this to be grouped by the category column of the Projects' table that have the category of the string 'books'. In the query, I used HAVING because I used GROUP BY, which were both used because there was an aggregate SQL query in use called ```SUM(column_name)```. 
A left join is where the two tables overlapped, one column replacing the other. It returns all the rows from the left table and the matched rows from the right table. The default syntax for a ```LEFT JOIN``` is:```SELECT column_name(s) FROM first_table
LEFT JOIN second_table
ON first_table.column_name = second_table.column_name;```<br>
In this case, the query returned the sum total of all the pledges for the books category. 
TL;DR - Overall, I continued to learn and practice how to create schemas, insert seed data, draw UML/ERD diagrams, write complex join statements, and write complex query statements in SQLite3. 
All the Best,
Max

