The results table contains the following columns:

name - the unique name of the team;
country - the country of the team;
scored - the number of scored goals;
missed - the number of missed goals;
wins - the total number of games the team has won.
Your task is to sort the given results table in ascending order by the number of wins.

Example

For given table results

name	country	scored	missed	wins
FC Tokyo	Japan	26	28	1
Fujian	China	24	26	0
Jesus Maria	Argentina	25	23	3
University Blues	Australia	16	25	2
the output should be

name	country	scored	missed	wins
Fujian	China	24	26	0
FC Tokyo	Japan	26	28	1
University Blues	Australia	16	25	2
Jesus Maria	Argentina	25	23	3

CREATE PROCEDURE volleyballResults()
BEGIN
    SELECT * FROM results ORDER BY WINS ASC;
END