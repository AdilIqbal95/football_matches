# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT * FROM  matches WHERE season = 2017;
--7810 matches

```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM  matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';
-- 608 matches

```

3) What are the names of the Scottish divisions included?

```sql
SELECT name FROM divisions WHERE country = 'Scotland';
--Scottish Premiership
--Scottish Championship
--Scottish League One

```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT * FROM divisions WHERE name = 'Bundesliga'; -- D1
SELECT COUNT(*) FROM matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');

```

5)  Find the teams which include the word "City" in their name. HINT: Not every team has been entered into the database with their full name, eg. `Norwich City` are listed as `Norwich`. If your query is correct it should return four teams.

```sql
SELECT DISTINCT hometeam FROM matches WHERE hometeam LIKE '%City%';
--Bath City
--Bristol City
--Edinburgh City
--Man City

```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT * FROM divisions WHERE country = 'France'; -- F1 or F2
SELECT COUNT(*) FROM matches WHERE division_code = 'F1' or division_code = 'F2';
--11959

```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT * FROM matches WHERE (hometeam = 'Huddersfield' AND awayteam = 'Swansea') OR (hometeam = 'Swansea' AND awayteam = 'Huddersfield');
-- 12 times

```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
SELECT * FROM divisions WHERE name = 'Eredivisie';  -- N1
SELECT COUNT(*) FROM matches WHERE division_code = 'N1' AND ftr = 'D' AND (season >= 2010 AND season <= 2015); 
-- 431 draws

```

9) Select the matches played in the Premier League in order of total goals scored (`fthg` + `ftag`) from highest to lowest. When two matches have the same total the match with more home goals (`fthg`) should come first. 

```sql
SELECT * FROM divisions WHERE name = 'Premier League'; -- E0
SELECT *, (fthg + ftag) as total_goals  FROM matches WHERE division_code = 'E0' ORDER BY total_goals DESC;

```

10) Find the name of the division in which the most goals were scored in a single season and the year in which it happened.

```sql
SELECT division_code,season, SUM(fthg) as total_fthg, SUM(ftag) as total_ftag, (SUM(fthg) + SUM(ftag)) as grand_total FROM matches GROUP BY season, division_code ORDER BY grand_total DESC;
-- National League (EC) in 2013 with a total of 1592 goals

```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)