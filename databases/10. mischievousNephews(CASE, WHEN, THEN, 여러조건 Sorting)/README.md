The resulting table should contain four columns, weekday, mischief_date, author, and title, where weekday is the weekday of mischief_date (0 for Monday, 1 for Tuesday, and so on, with 6 for Sunday). The table should be sorted by the weekday column, and for each weekday Huey's mischief should go first, Dewey's should go next, and Louie's should go last. In case of a tie, mischief_date should be a tie-breaker. If there's still a tie, the record with the lexicographically smallest title should go first.

It is guaranteed that all entries of mischief are unique.

Example

For the following table mischief

mischief_date	author	title
2016-12-01	Dewey	Cook the golden fish in a bucket
2016-12-01	Dewey	Paint the walls pink
2016-12-01	Huey	Eat all the candies
2016-12-01	Louie	Wrap the cat in toilet paper
2016-12-08	Louie	Play hockey on linoleum
2017-01-01	Huey	Smash a window
2017-02-06	Dewey	Create a rink on the porch
the output should be

weekday	mischief_date	author	title
0	2017-02-06	Dewey	Create a rink on the porch
3	2016-12-01	Huey	Eat all the candies
3	2016-12-01	Dewey	Cook the golden fish in a bucket
3	2016-12-01	Dewey	Paint the walls pink
3	2016-12-01	Louie	Wrap the cat in toilet paper
3	2016-12-08	Louie	Play hockey on linoleum
6	2017-01-01

```sql
CREATE PROCEDURE mischievousNephews()
BEGIN
    SELECT DAYOFWEEK((mischief_date- INTERVAL 2 DAY))%7 AS weekday, mischief_date, author, title FROM mischief ORDER BY weekday, 
    CASE author 
    WHEN 'Huey' THEN 0 
    WHEN 'Dewey' THEN 1 
    WHEN 'Louie' THEN 2
    ELSE 3
    END,
    mischief_date, title;
END
```