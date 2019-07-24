For the following table projectLog

id	name	description	timestamp
1	James Smith	add new logo	2015-11-10 15:24:32
2	John Johnson	update license	2015-11-10 15:50:01
3	John Johnson	fix typos	2015-11-10 15:55:01
4	James Smith	update logo	2015-11-10 17:53:04
5	James Smith	delete old logo	2015-11-10 17:54:04
6	Michael Williams	fix the build	2015-11-12 13:37:00
7	Mary Troppins	add new feature	2015-11-08 17:54:04
8	James Smith	fix fonts	2015-11-14 13:54:04
9	Richard Young	remove unneeded files	2015-11-14 00:00:00
10	Michael Williams	add tests	2015-11-09 11:53:00

the output should be

name
James Smith
John Johnson
Mary Troppins
Michael Williams
Richard Young

```sql
CREATE PROCEDURE projectsTeam()
BEGIN
	SELECT name FROM projectLog GROUP BY name ORDER BY name;
END
```