# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT * FROM matches WHERE season = 2017;


```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';


```

3) What are the names of the Scottish divisions included?

```sql
SELECT DISTINCT name FROM divisions WHERE country = 'Scotland';


```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT * FROM matches
WHERE (hometeam = 'Freiburg' OR awayteam = 'Freiburg') AND division_code = (SELECT code FROM divisions WHERE name = 'Bundesliga');


```

5) Find the teams which include the word "City" in their name. 

```sql
SELECT DISTINCT hometeam FROM matches WHERE LOWER(hometeam) LIKE LOWER('%City%'); 


```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT DISTINCT hometeam FROM matches 
WHERE division_code IN (SELECT DISTINCT code FROM divisions WHERE country = 'France');

```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT hometeam, awayteam, season FROM matches
WHERE (hometeam = 'Huddersfield' AND awayteam = 'Swansea') OR (hometeam = 'Swansea' AND awayteam = 'Huddersfield');


```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
SELECT COUNT(ftr) FROM matches
WHERE ftr = 'D' AND (season BETWEEN 2010 AND 2015) AND division_code IN (SELECT code FROM divisions WHERE name = 'Eredivisie');


```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
SELECT *  FROM matches
WHERE division_code IN (SELECT code FROM divisions WHERE name = 'Premier League') ORDER BY((fthg + ftag), fthg)DESC;



```

10) In which division and which season were the most goals scored?

```sql
SELECT division_code, season, SUM(fthg + ftag)
FROM matches 
GROUP BY (division_code, season)
ORDER BY SUM(fthg + ftag)DESC LIMIT 10;
SELECT * FROM divisions WHERE code = 'EC';


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)