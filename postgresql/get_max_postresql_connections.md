# Get Maximum Active Connections to PostgreSQL database

To get the maximum amount of active connections that a PostgreSQL database will accept, run the following command:
```sql
SHOW max_connections;
```

To modify this value, the command is:
```sql
ALTER SYSTEM SET max_connections = 250;
```

From the CLI the command to modify the value is:
```bash
postgres -c 'max_connections=250'
```

And this is how to update the docker-compose file if we're using it to run our database instance:
```yaml
services:
  database:
    image: postgres:latest
    command: postgres -c 'max_connections=250'
```
