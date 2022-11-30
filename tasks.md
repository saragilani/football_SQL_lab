# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT * FROM public.matches WHERE season = 2017;
```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM public.matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona'; 
```

3) What are the names of the Scottish divisions included?

*[Scottish Premiership |
Scottish Championship |
Scottish League One]*
```sql
SELECT name FROM public.divisions WHERE country ='Scotland';
```

4) Find the division code for the Bundesliga. Use that code to find out how many matches Freiburg have played in the Bundesliga since the data started being collected.

```sql
SELECT code FROM public.divisions WHERE name ='Bundesliga'; -- to find division code D1 for Bundesliga

SELECT * FROM public.matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');
```

5) Find the unique names of the teams which include the word "City" in their name (as entered in the database)

```sql
SELECT DISTINCT awayteam FROM public.matches WHERE LOWER(awayteam) LIKE '%city%';
```

6) How many different teams have played in matches recorded in a French division?

*[61]*

```sql
SELECT code FROM public.divisions WHERE country ='France'; -- F1, F2 division_codes

SELECT COUNT(DISTINCT hometeam) FROM public.matches WHERE division_code ='F1' OR division_code = 'F2';
```

7) Have Huddersfield played Swansea in the period covered?

*[Yeah they have. The two queries show all matches they've played against each other.]*

```sql
<SELECT * FROM public.matches WHERE hometeam ='Huddersfield' AND awayteam = 'Swansea';

SELECT * FROM public.matches WHERE awayteam ='Huddersfield' AND hometeam = 'Swansea';

```

8) How many draws were there in the Eredivisie between 2010 and 2015?

*[1114]*

```sql
SELECT * FROM public.divisions WHERE name = 'Eredivisie'; -- division_code = N1
SELECT COUNT(*) FROM public.matches WHERE division_code = 'N1' AND ftr = 'D';
```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. Where there is a tie the match with more home goals should come first.

```sql
SELECT * FROM public.divisions WHERE name = 'Premier League'; -- E0 code.

SELECT *, ftag + fthg AS totalgoal  FROM public.matches WHERE division_code ='E0' ORDER BY totalgoal desc, fthg >ftag DESC;
```

10) In which division and which season were the most goals scored?

```sql
SELECT *, ftag + fthg AS totalgoal  FROM public.matches WHERE division_code ='E0' ORDER BY totalgoal desc, fthg >ftag DESC;

```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)