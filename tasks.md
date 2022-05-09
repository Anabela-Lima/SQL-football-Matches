# Football Matches - Tasks


1) Find all the matches from 2017.

```sql
SELECT * FROM matches WHERE season = '2017'


```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM matches WHERE hometeam LIKE 'Barcelona' OR awayteam LIKE 'Barcelona';


```

3) What are the names of the Scottish divisions included?

```sql

SELECT name FROM divisions where name LIKE '%Scottish%';


```

4) Find the division code for the Bundesliga. Use that code to find out how many matches Freiburg have played in the Bundesliga since the data started being collected.

```sql

 SELECT * FROM divisions WHERE name LIKE 'Bundesliga';

-- [ Code is D1 ]

-- count (id) -> we are counting all games played in the Bundesliga where hometeam or awayteam has been ‘Freiburg' 
 
 SELECT COUNT(id)  FROM matches WHERE division_code = 'D1' AND (hometeam LIKE 'Freiburg' OR  awayteam LIKE 'Freiburg');

```

5) Find the unique names of the teams which include the word "City" in their name (as entered in the database)

```sql

SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%';  


```

6) How many different teams have played in matches recorded in a French division?

```sql

-- Get the division number for country France:
SELECT * FROM  divisions WHERE country = 'France';

-- Get all matches with F1 or F2:	
SELECT Count(DISTINCT hometeam) FROM matches WHERE division_code = 'F1' OR division_code = 'F2';



```

7) Have Huddersfield played Swansea in the period covered?

```sql

SELECT* From matches WHERE (hometeam Like 'Huddersfield' AND awayteam LIKE 'Swansea') OR (hometeam Like 'Swansea' AND awayteam Like 'Huddersfield');

 


```

8) How many draws were there in the Eredivisie between 2010 and 2015?

```sql
-- Get code for Eredivisie = N1

SELECT * From divisions WHERE name Like 'Eredivisie';

-- from matches count ftr (results coulumn)  where division code is N1 (i.e. Eredisie played), and season is between 2010 and 2015, and result was a draw

SELECT Count(ftr) From matches WHERE division_code = 'N1' AND (season BETWEEN 2010 AND 2015) AND (ftr ='D')
	



```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. Where there is a tie the match with more home goals should come first.

```sql

--       Get premier league code: E0 

SELECT * FROM divisions WHERE name LIKE 'Premier League';

--	ORDER by sum  (this by default is lowest to highest so convert)

SELECT  * From matches WHERE division_code = 'E0' ORDER BY (fthg + ftag);

--	Covert to DESC order
SELECT  * From matches WHERE division_code = 'E0' ORDER BY (fthg + ftag)DESC; 

--	Again order by hometeam goals in same  descending order

SELECT  * From matches WHERE division_code = 'E0' ORDER BY (fthg + ftag)DESC, fthg DESC




```

10) In which division and which season were the most goals scored?

```sql

-- 	Show:  division_code column, and season column, and a column that sums fthg and ftag

SELECT division_code, season, total (fthg+ ftag) From matches  

--	Group everything by division code, then by season:

SELECT division_code, season, SUM (fthg + ftag) FROM matches GROUP BY division_code, season

--	ORDER by DESC order (high to low) and limit to 1

SELECT division_code, season, SUM (fthg + ftag) FROM matches GROUP BY division_code, season ORDER BY sum DESC LIMIT 1;


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)
