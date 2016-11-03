# assignment_sql_taste
A delicious appetizer of SQL-ey goodness

[Joe Bernardi](https://github.com/jdbernardi/assignment_sql_taste)

## Queries, Queries, Queries

### Example

```
SELECT *
  FROM tutorial.us_housing_units
  WHERE month = 1
```

1. 10 Results with information on all columns

	SELECT *
    FROM tutorial.us_housing_units
    LIMIT 10

2. Housing starts in the Midwest

	SELECT year,
	       month,
	       month_name,
	       midwest
	  FROM tutorial.us_housing_units

3. All housing starts in December since 1985

	SELECT *
	  FROM tutorial.us_housing_units
	  WHERE "month" = 12 AND year >= 1985

4. All housing starts in the second half of the year since 1990

	SELECT *
  	FROM tutorial.us_housing_units
  	WHERE "month" >= 6 AND year >= 1990


5. All rows where housing starts were above 30,000 in the South region

	SELECT *
  	FROM tutorial.us_housing_units
  	WHERE "south" > 30

6. The sum of housing starts across all regions for each row

	SELECT south AS "South",
       west AS "West",
       midwest AS "Midwest",
       northeast AS "northeast",
       south + west + midwest + northeast  AS "TOTAL"
  FROM tutorial.us_housing_units

7. All rows where the sum of all housing starts is above 70,000 Note: You can't use an alias in a WHERE clause.

	SELECT south AS "South",
       west AS "West",
       midwest AS "Midwest",
       northeast AS "northeast",
       south + west + midwest + northeast  AS "TOTAL"
  FROM tutorial.us_housing_units
  WHERE ( south + west + midwest + northeast ) > 70

8. All rows where the sum of all housing starts is between 50-80k

	SELECT south AS "South",
       west AS "West",
       midwest AS "Midwest",
       northeast AS "northeast",
       south + west + midwest + northeast  AS "TOTAL"
  FROM tutorial.us_housing_units
  WHERE ( south + west + midwest + northeast ) > 50 AND ( south + west + midwest + northeast ) < 80


9. The average of all housing starts across all regions for each row

	SELECT south AS "South",
       west AS "West",
       midwest AS "Midwest",
       northeast AS "Northeast",
       ( south + west + midwest + northeast ) / 4  AS "Average"
  FROM tutorial.us_housing_units


10. All rows where the housing starts in the South are above the sum of the other three regions

	SELECT south AS "South",
       west AS "West",
       midwest AS "Midwest",
       northeast AS "Northeast"
  FROM tutorial.us_housing_units
  WHERE south > ( west + midwest + northeast )

11. The percentage of housing starts that occur in each region since 1990 Note: Use an alias to title the new columns appropriately

	SELECT south/( south + west + midwest + northeast ) AS "South_pct",
       west/( south + west + midwest + northeast ) AS "West_pct",
       midwest/( south + west + midwest + northeast ) AS "Midwest_pct",
       northeast/( south + west + midwest + northeast ) AS "Northeast_pct"
  FROM tutorial.us_housing_units
  WHERE year >= 1990


tutorial.billboard_top_100_year_end

Note: Use single quotes ' instead of double quotes " for LIKE and similar queries since the Mode tool is very particular about its syntax. Double quotes are used to specify column names, so you might get a "column XYZ does not exist" error if you mess this up.

All rows where Elvis Presley had a song on the top 100 charts
All rows where the artist's name contained "Tony" (not case sensitive)
All rows where the song title contained the word "love" in any way
All rows where the artist's name begins with the letter "A"
The top 3 songs from each year between 1960-1969
All rows where either Elvis Presley, The Rolling Stones, or Van Halen were the artist
Which artist has had the most appearances on the top 100 list?
Which artist has had the most #1 hits? How many?
All rows from 1970 where the songs were ranked 10-20th
All rows from the 1990's where Madonna was not ranked 10-100th
All rows from 1985 which do not include Madonna or Phil Collins in the group.
All number 1 songs in the data set.
All rows where the artist is not listed
All of Madonna's top 100 hits ordered by their ranking (1 to 100)
All of Madonna's top 100 hits ordered by their ranking within each year
Every number 1 song since 1990 followed by every number 2 song since 1990 and number 3 song since 1990. (Hint: Multiple ordering)