--> Cleaning and transformation using Python Pandas
Got an overview of data.
Changed data types .
Removed errors
Removed null values in some columns

--> SQL analysis
Questions
Q. 1) For 'The Perfect Date', what is the Show Id and Who is the Director of this show ?
Q. 2) In which year the highest number of the TV Shows & Movies were released ? Show with Bar Graph.
Q. 3) How many Movies & TV Shows are in the dataset ? Show with Bar Graph.
Q. 4) Show all the Movies that were released in year 2000.
Q. 5) Show only the Titles of all TV Shows that were released in India only.
Q. 6) Show Top 10 Directors, who gave the highest number of TV Shows & Movies to Netflix ?
Q. 7) In how many movies/shows, Tom Cruise was cast ?
Q. 8) What are the different Ratings defined by Netflix ?
Q. 9) How many Movies got the 'TV-14' rating, in Canada ?
Q. 10) How many TV Shows got the 'R' rating, after year 2018 ?
Q. 11) Which individual country has the Highest No. of TV Shows ?
Q. 12) How can we sort the dataset by Year ?
Q. 13) Find all the instances where: Category is 'Movie' and Type is 'Dramas' or Category is 'TV Show' & Type is 'Kids' TV

Queries
1) SELECT title, show_id, director
FROM netflix
WHERE title = 'The Perfect Date'

2) SELECT release_year, type, COUNT(title)
FROM netflix
GROUP BY type, release_year
ORDER BY release_year DESC
LIMIT 2

3)SELECT  type, COUNT(title)
FROM netflix
GROUP BY type

4) SELECT  type, title, release_year
FROM netflix
WHERE release_year = 2020 AND type = 'Movie'
ORDER BY release_year DESC

5) SELECT title
FROM netflix
WHERE country = 'India' AND type = 'TV Show'

6) SELECT COUNT(type) as total_number_of_type, director
FROM netflix
WHERE director is not null
GROUP BY director
ORDER BY total_number_of_type DESC
LIMIT 10

7) SELECT netflix.cast, title
FROM netflix
WHERE netflix.cast LIKE '%Tom Cruise%'

8)SELECT COUNT(rating) AS total_no,rating
FROM netflix
WHERE rating NOT LIKE '%min%' AND rating IS NOT null
GROUP BY rating
ORDER BY total_no DESC

9) SELECT COUNT(type)
FROM netflix 
WHERE type = 'Movie' AND country = 'Canada' AND rating = 'TV-14' = 13

10) SELECT COUNT(title) as No_of_tv_shows
FROM netflix
WHERE type = 'TV Show' AND rating = 'R' AND release_year > 2018

11) SELECT COUNT(title) as No_of_tv_shows, country
FROM netflix
WHERE type = 'TV Show' AND country IS NOT null
GROUP BY country
ORDER BY No_of_tv_shows DESC
LIMIT 1

12) SELECT *
FROM netflix
ORDER BY release_year DESC

13) SELECT show_id, type, title, director, listed_in, description, country, date_added, rating
FROM netflix
WHERE (type = 'Movie' AND listed_in LIKE '%Dramas%')
OR (type = 'TV Show' AND listed_in LIKE ('%Kids%'))

--> Power Bi
Created dashbaord on netflix data with analysis from SQL.

Measures 
1) Movies = CALCULATE(COUNTROWS('netflix_titles'), netflix_titles[type]= "Movie" )
2) TV shows = CALCULATE(COUNTROWS('netflix_titles'), 'netflix_titles'[type] = "TV show" )

Pages Titles
1) Summary
   Overall summary

2) Rating
   Rating analysis with respect to TV Shows and Movies

3) Country
   TV Shows and Movies analysis with respect to countries worldwide

4) Table
   Table with filters for country, type, year and rating to find selected content

5) Map 
   Showing a mapped distribution of content worldwide
