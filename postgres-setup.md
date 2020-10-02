# Postgres setup

## 1. Create database and main role

Connect to database with psql client

```
sudo su - postgres
psql
```

Create Database and set password for the default (jhlab) user/role:

```sql
CREATE DATABASE jhlab;
ALTER ROLE jhlab WITH CREATEROLE PASSWORD 'jhlabpwd';
GRANT CREATE ON DATABASE jhlab TO jhlab WITH GRANT OPTION;
```

** Now logout and login to postgres as jhlab user. **

## 2. Create role for gateway service

```sql
CREATE ROLE gateway with LOGIN ENCRYPTED PASSWORD 'gatewaypwd';
GRANT gateway TO jhlab;
CREATE SCHEMA IF NOT EXISTS AUTHORIZATION gateway;

GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO gateway;
```


## 3. Create role for geodata service

```sql
CREATE ROLE geodata with LOGIN ENCRYPTED PASSWORD 'geodatapwd';
GRANT geodata TO jhlab;
CREATE SCHEMA IF NOT EXISTS AUTHORIZATION geodata;

GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO geodata;
```

