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


select * from netflix

## Business Problems & Solutions

## 1. Count the number of Movies vs TV Shows

select 
     type,count(type) as no_of_movies_and_tv_shows
from netflix
group by type;

## 2. Find all TV Shows produced in the United States

select * 
from netflix 
where type = TV Show and country = United States;

## 3. Count how many titles were released each year

select count(title) as total_titles, release_year
from netflix
group by release_year
order by 2 desc;

## 4. Find the top 5 countries with the most content on Netflix

select 
unnest(string_to_array(country,',')) as new_country, count(show_id) 
from netflix 
group by new_country
order by count(show_id) desc
limit 5;

## 5. Identify how many titles each director has worked on

SELECT director, COUNT(*) AS total_titles 
FROM netflix 
WHERE director IS NOT NULL 
GROUP BY director 
ORDER BY total_titles DESC;


## 6. Find content added in the last 5 years

select * from netflix 
where to_date(date_added, 'Month DD,YYYY') >= current_date - interval '5 years';

## 7. Find all the movies/TV shows by director 'Rajiv Chilaka'!

select * from netflix 
where director like '%Rajiv Chilaka%';

## 8. List all TV shows with more than 5 seasons

select * from netflix 
where type = 'TV Show' and split_part(duration,' ',1):: numeric > 5 ;

## 9. Count the number of content items in each genre

select unnest(string_to_array(listed_in,',')) as genre, count(show_id)
from netflix
group by genre;

## 10. List all movies that are documentaries

select * from netflix
where listed_in Ilike '%documentaries%' ;

## 11.Find each year and the average numbers of content release in India on netflix.

select extract(year from to_date(date_added,'Month DD,YYYY')) as year, count(*) as yearly_content,
round(count(*)::numeric / (select count(*) from netflix where country = 'India')::numeric*100,2)as avg_content_per_year
from netflix
where country = 'India'
group by 1;

## 12. Find all content without a director

select * from netflix 
where director is null;
