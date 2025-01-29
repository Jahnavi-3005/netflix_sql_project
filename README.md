# Netflix Dataset Analysis Using SQL

![netflix_logo](https://github.com/Jahnavi-3005/netflix_sql_project/blob/main/logo.png)


## Overview

This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.

## Objectives

- Analyze the distribution of content types (movies vs TV shows).
- Identify the most common ratings for movies and TV shows.
- List and analyze content based on release years, countries, and durations.
- Explore and categorize content based on specific criteria and keywords.
  
## Dataset

The data for this project is sourced from the Kaggle dataset:

- Dataset Link: [Movies Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)

## Schema

```sql
create table Netflix
(
   show_id	varchar(10),
   type	 varchar(20),
   title varchar(150),	
   director	varchar(250),
   casts	varchar(1000),
   country varchar(150),
   date_added varchar(50),
   release_year	int,
   rating	varchar(20),
   duration	varchar(25),
   listed_in varchar(250),
   description varchar(300)
);
```

select * from netflix

## Business Problems and Solutions


