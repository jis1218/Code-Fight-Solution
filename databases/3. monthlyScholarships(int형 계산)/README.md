For the following table scholarships

id	scholarship
1	12000
2	18000
3	24000
4	15000
5	21000
6	13000
the output should be

id	scholarship
1	1000
2	1500
3	2000
4	1250
5	1750
6	1083.3333333333333

```sql
CREATE PROCEDURE monthlyScholarships()
BEGIN
	SELECT id, (scholarship/12) AS scholarship FROM scholarships;
END
```