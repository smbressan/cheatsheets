## Postgres Cheatsheet


#### Connect to a db: 
```
psql -h host -p 5432 -d DATABASE_NAME -U user  
```
#### Create a read only user
```
CREATE USER USER_NAME WITH ENCRYPTED PASSWORD 'xxxxx';
GRANT CONNECT ON DATABASE "DATABASE_NAME" to USER_NAME;

GRANT USAGE ON SCHEMA public to USER_NAME;
GRANT SELECT ON ALL SEQUENCES IN SCHEMA public TO USER_NAME;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO USER_NAME;
```
#### Version of the db I'm running: 
```
SELECT version();
```
#### Future clause for a given user: 
```
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO USER_NAME;
```
#### More commands

| Command  | Description  |
|----------|--------------|
|```\du```  | To list all users and their assign roles |
| ```\c dbname username``` | Switch connection to another DB |
| ```\l``` | List available DBs |
| ```\dt``` | List all tables in a DB |
| ```\d table_name``` | Describe a table |
| ```\dn``` | List available schema |
| ```\df``` | List available functions |
| ```\dv``` | List available views |
| ```\g``` | Execute the previous command |
| ```\s``` | Command history |
| ```\i filename``` | Execute commands from a file |
| ```\q``` | Quit |
