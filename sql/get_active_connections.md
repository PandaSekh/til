# Get Active Connections to PostgreSQL database

Today I had issues with failing tests because PostgreSQL was rejecting connections due to having too many of them opened.

I needed to know the number of active connections at any given time to pinpoint the issue. Luckily Postgres has a table with stats, including active connections.

To list them:
```sql
SELECT * FROM pg_stat_activity;
```

After that, I noticed that all connections opened by my application had `application_name` valorized as `PostgreSQL JDBC Driver` (it's a Spring Boot app using HikariCP to manage connections, it's probably standard naming). 

So we can get all connections opened by the app with this query:
```sql
SELECT * FROM pg_stat_activity where application_name = 'PostgreSQL JDBC Driver';
```
