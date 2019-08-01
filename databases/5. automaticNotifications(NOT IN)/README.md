Given the users table, your task is to return the emails of all the users who should get notifications, i.e. those whose role is not equal to "admin" or "premium". Note that roles are case insensitive, so users with roles of "Admin", "pReMiUm", etc. should also be excluded.

The resulting table should contain a single email column and be sorted by emails in ascending order.

Example

For the following table users

id	username	role	email
6	fasalytch	premium	much.premium@role.com
13	luckygirl	regular	fun@meh.com
16	todayhumor	guru	today@humor.com
23	Felix	admin	felix@codesignal.com
52	admin666	AdmiN	iamtheadmin@admin.admin
87	solver100500	regular	email@notbot.com
the resulting table should be

email
email@notbot.com
fun@meh.com
today@humor.com

```sql
CREATE PROCEDURE automaticNotifications()
    SELECT email
    FROM users
    WHERE role NOT IN ("admin", "premium")

    ORDER BY email;
```