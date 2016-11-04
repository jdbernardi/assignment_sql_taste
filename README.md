# assignment_sql_taste
A delicious appetizer of SQL-ey goodness

[Joe Bernardi](https://github.com/jdbernardi/assignment_sql_taste)

## Queries, Queries, Queries

--US HOUSING--

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


--BILLBOARD TOP 100--

1. All rows where Elvis Presley had a song on the top 100 charts

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE "group" LIKE '%Elvis%'

2. All rows where the artist's name contained "Tony" (not case sensitive)

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE "artist" ILIKE '%Tony%'


3. All rows where the song title contained the word "love" in any way

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE "song_name" ILIKE '%love%'

4. All rows where the artist's name begins with the letter "A"

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE "artist" LIKE 'A%'

5. The top 3 songs from each year between 1960-1969

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE year BETWEEN 1960 AND 1969
  	      AND year_rank IN (1,2,3)

6. All rows where either Elvis Presley, The Rolling Stones, or Van Halen were the artist

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE "group" ILIKE '%Rolling Stones%'
  	OR "group" ILIKE '%Van Halen%'
  	OR "group" ILIKE '%Elvis Presley%'

7. Which artist has had the most appearances on the top 100 list?
	=>Madonna & Elvis Presley

	SELECT artist,
    COUNT(year) AS year
  	FROM tutorial.billboard_top_100_year_end

  GROUP BY artist

  ORDER BY year DESC

8. Which artist has had the most #1 hits? How many? Beatles (2), Elvis(2)

	SELECT artist,
    COUNT(year) AS year
  	FROM tutorial.billboard_top_100_year_end
    WHERE year_rank = 1
  GROUP BY artist

  ORDER BY year DESC


9. All rows from 1970 where the songs were ranked 10-20th

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE year_rank BETWEEN 10 AND 20
  	  AND year = 1970

10. All rows from the 1990's where Madonna was not ranked 10-100th

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE year BETWEEN 1990 AND 1999
  	  AND year_rank >= 10
  	  AND artist != 'Madonna'

11. All rows from 1985 which do not include Madonna or Phil Collins in the group.

	SELECT *
  	FROM tutorial.billboard_top_100_year_end
  	WHERE year = 1985
  	  AND ("group" NOT ILIKE '%Madonna%'
  	  AND "group" NOT ILIKE '%phil collins%' )


12. All number 1 songs in the data set.

	SELECT year AS "Year",
	       song_name AS "Song"
  	FROM tutorial.billboard_top_100_year_end
  	WHERE year_rank = 1


13. All rows where the artist is not listed

	SELECT year AS "Year",
	       song_name AS "Song"
  	FROM tutorial.billboard_top_100_year_end
  	WHERE artist IS NULL

14. All of Madonna's top 100 hits ordered by their ranking (1 to 100)

	SELECT year AS "Year",
	       year_rank AS "Rank",
	       artist AS "Artist",
	       song_name AS "Song"
  	FROM tutorial.billboard_top_100_year_end
  	WHERE artist ILIKE 'Madonna'
  	ORDER BY year_rank


15. All of Madonna's top 100 hits ordered by their ranking within each year

	SELECT year AS "Year",
	       year_rank AS "Rank",
	       artist AS "Artist",
	       song_name AS "Song"
  	FROM tutorial.billboard_top_100_year_end
  	WHERE artist ILIKE 'Madonna'
  	ORDER BY year, year_rank


16. Every number 1 song since 1990 followed by every number 2 song since 1990 and number 3 song since 1990. (Hint: Multiple ordering)


	SELECT year AS "Year",
	       year_rank AS "Rank",
	       artist AS "Artist",
	       song_name AS "Song"
  	FROM tutorial.billboard_top_100_year_end
  	WHERE year >= 1990 AND year_rank IN (1,2,3)
  	ORDER BY year_rank, year

--OPTIONAL--

1. What is the highest position ever reached by Phil Collins?

	SELECT MAX( year_rank ) AS max_rank
		FROM tutorial.billboard_top_100_year_end
		WHERE artist = 'Phil Collins'

2. What is the average position reached by Michael Jackson?

	SELECT AVG( year_rank ) AS avg_rank
		FROM tutorial.billboard_top_100_year_end
		WHERE artist = 'Michael Jackson'

3. Madonna's average position when she actually reached the top 10

4. List the top 10 artists based on their number of appearances on this list (and what that number is) since 1985

5. The total count of top 10 hits written by either Elvis, Madonna, the Beatles, or Elton John


--aapl_historical_stock_price--

1. The count of days when Apple traded in a range that was larger than $5

	SELECT COUNT(*)
	  FROM tutorial.aapl_historical_stock_price
	  WHERE ( high - low ) > 5

2. The highest daily trading range that Apple stock achieved in 2012

	SELECT MAX(high - low)
    FROM tutorial.aapl_historical_stock_price
    WHERE year = 2012

3. The average price for all days when Apple's trading volume exceeded 10,000,000 shares.

4. The number of trading days in each month of the year 2012

	SELECT COUNT( date )
	  FROM tutorial.aapl_historical_stock_price
	  WHERE year = 2012
	GROUP BY month

5. The maximum price Apple traded at during each year of the data set

	SELECT MAX( high ),
	       year AS "Year"
	  FROM tutorial.aapl_historical_stock_price
	GROUP BY year
	ORDER BY year

6. The average price and trading volume on each calendar month across the full data set (this should return only 12 rows, one for each month!)

7. The average price for each month and year of data since 2008, ordered by years descending and months ascending.

	SELECT AVG( close ) AS "Avg Close",
       AVG( volume ) AS "Avg Vol"
  	FROM tutorial.aapl_historical_stock_price 
  	GROUP BY month

8. The average price of days with a trading volume above 25,000,000 shares (just 1 row)

9. The average price on all months with an average daily trading volume above 10,000,000 shares.
10. The lowest and highest prices that Apple stock achieved between 2005 and 2010 (inclusive).
11. The average daily trading range in months where the stock moved more than $25 (open of month to close of month)
12. All months in the second half of the year where average daily trading volume was below 10,000,000.
13. A list of all calendar months by average daily trading volume (so only 12 rows), sorted from highest to lowest.
14. Count how many unique months there are in the data set (should equal 12)
15. Count how many unique years there are in the data set
16. Count how many unique prices there are in the data set
17. Return the percentage of unique "open" prices compared to all open prices in the data set
18. A listing of all months by their average daily trading volume and a classification that puts this volume into the following categories: "Low" = below 10MM, "Medium" = 10-25 MM, "High" = above 25MM
19. A listing of average monthly price plus which quarter of the year they are in (e.g. "Q2" or "Q4").
20. This same listing filtered for only Q4 (use the new column not the months explicitly as part of this filtering).

