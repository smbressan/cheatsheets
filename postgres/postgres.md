## Postgres Cheatsheet


#### Connect to a db: 
```
psql -h host -p 5432 -d DATABASE_NAME -U user  
```
#### Create a read only user
```
CREATE USER psql_readonly WITH ENCRYPTED PASSWORD 'xxxxx';
GRANT CONNECT ON DATABASE "promotions-api" to temaki_data_user;

GRANT USAGE ON SCHEMA public to temaki_data_user;
GRANT SELECT ON ALL SEQUENCES IN SCHEMA public TO temaki_data_user;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO temaki_data_user;
```
#### Version of the db I'm running: 
```
SELECT version();
```
#### Future clause for a given user: 
```
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO readaccess;
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
