---
title: "SQL Library -- First Technical Post"
date: "2016-12-29T12:46:37.121Z"
layout: post
draft: false
path: "/posts/seventh-post/"
category: "Flatiron School"
tags:
  - "SQL"
  - "Queries"
description: "This is a post about a SQL lab for the Flatiron School."
---

In this assignment, I was tasked with building a database schema, creating the UML/ERD, inserting data, updating data, and writing complex queries for the data in SQLite3 using the command line or an SQL browser such as Base. 

First, I created the schema by creating the tables the database required: <br><br>
``` CREATE TABLE series (id INTEGER PRIMARY KEY, title TEXT, author_id INTEGER, subgenre_id INTEGER);```<br>
```CREATE TABLE subgenres (id INTEGER PRIMARY KEY, name TEXT);```<br>
```CREATE TABLE authors (id INTEGER PRIMARY KEY, name TEXT);```<br>
```CREATE TABLE books (id INTEGER PRIMARY KEY, title TEXT, year INTEGER, series_id INTEGER);```<br>
```CREATE TABLE characters (id INTEGER PRIMARY KEY, name TEXT, motto TEXT, species TEXT, author_id INTEGER, series_id INTEGER);```<br>
``` CREATE TABLE character_books (id INTEGER PRIMARY KEY, book_id INTEGER, character_id INTEGER); ```<br>

Second, I made a UML/ERD (Entity-relationship Diagram) to express the table data and relationships between the data with Gliffy, which is a free diagraming cloud software. 

![My helpful screenshot]({{ site.url }}/img/screenshot.png)	

Third, I inserted the data using INSERT INTO. I overall added two series, two subgenres, two authors, six books, eight characters, and data for character_books. For example: 

``` INSERT INTO series (id, title, author_id, subgenre_id) VALUES (1, "A Song of Ice and Fire", 1, 1), (2, "A Series of Unfortunate Events", 2, 2); ```

Fourth, I created the database and used the < operator to insert the schema and the seed data into the database called sql_lib.db. 

Fifth, I updated the last entry in the characters species row to be "Martian". I used this: 

```UPDATE characters SET species = "Martian" WHERE species = "cylon" AND id = 8;```

Sixth, I started on the queries, which can be found below. 

```
def select_books_titles_and_years_in_first_series_order_by_year
	"SELECT books.title, books.year FROM books WHERE series_id =1 ORDER BY year ASC;"
end

def select_name_and_motto_of_char_with_longest_motto
	"SELECT characters.name, characters.motto FROM characters WHERE LENGTH(motto) > 25;"
end

def select_value_and_count_of_most_prolific_species
	"SELECT characters.species, COUNT(characters.id) FROM characters WHERE species= 'human';"
end

def select_name_and_series_subgenres_of_authors
	"SELECT authors.name, subgenres.name FROM authors LEFT JOIN subgenres ON authors.id 
	= subgenres.id;"
end

def select_series_title_with_most_human_characters
	"SELECT series.title FROM characters, series WHERE characters.species 
	LIKE 'human' AND characters.series_id = 1 AND series.id = 1 LIMIT 1;"
end

def select_character_names_and_number_of_books_they_are_in
	"SELECT DISTINCT characters.name, COUNT(character_books.character_id) FROM characters,
	 character_books WHERE character_books.character_id = characters.id 
	 GROUP BY character_books.character_id ORDER BY COUNT(character_books.character_id) 
	 DESC, characters.name ASC;"
end
```

I found each query by placing the database in sqlite3 and testing out queries in the command line. 

To find the first query, I selected the books table title column and books table and year column from the books table where the series id for the book was 1 (which is the id for the first series) and ordered it by ascending year. 

To find the last query, I discovered the DISTINCT feature for SQL. My problem was that I was able to get the tables in place, however they would display the inappropriate name for the book_id or character_id. To fix this problem, I used DISTINCT, which selects only unique values and limited the names of the characters to the eight that were already listed, instead of listing each name multiple times. 

TL;DR - Overall, I learned how to create schemas, insert seed data, draw UML/ERD diagrams, update data, write complex join statements, and write complex query statements in SQLite3. 

All the Best,

Max
