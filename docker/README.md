## Run

### Pull Docker image

Pull image (available versions at this [link](https://hub.docker.com/_/postgres/)).

```bash
make pull-image
```

### Create volume

[Resource](https://rhiyo.github.io/post/2021-4-21-running-postgres-in-docker-container-with-mounted-volume/).

Create volume to store the database data:

```bash
make create-volume
```

### Run container

Start a PostgreSQL instance:

```bash
make run
```

### Create table

[Resource](https://phoenixnap.com/kb/deploy-postgresql-on-docker).

```bash
make connect
psql -U postgres
```

This can be done with only one command:

```bash
make connect-psql
```

To configure the db:

```bash
# Create db.
create database contacts;
# Show the current databases.
\l
# Connect to the db as the postgres user.
\c contacts
# Create a schema that helps you get a logical representation of the database structure.
create schema contacts;
# List schemas.
\dn
# Add the new schema to the search path to work with tables in this schema without specifying the schema name.
SET search_path TO contacts, public;
# Show schema search path.
SHOW search_path;
# Show current schema.
SELECT current_schema();
# Create table.
CREATE TABLE users (
	id INT PRIMARY KEY,
	name VARCHAR ( 50 ) NOT NULL,
	surname VARCHAR ( 50 ) NULL
);
# Show tables in current schema.
\dt
# Show table details.
\d+ users;
# Insert data.
INSERT INTO
    users (id, name, surname)
VALUES
    (1, 'John','Doe'),
    (2, 'Foo Name','Bar Surname')
;
# Exit the container.
\q
```

Resources:
- [Create db](https://www.postgresqltutorial.com/postgresql-administration/postgresql-create-database/).
- [Schema](https://www.postgresqltutorial.com/postgresql-administration/postgresql-schema/).

### Export and import the database

#### Export the database

Resources:

- [Option 1](https://www.postgresqltutorial.com/postgresql-administration/postgresql-copy-database/)
- [Option 2](https://www.postgresqltutorial.com/postgresql-administration/postgresql-backup-database/)

```bash
make connect
cd /home/postgres/data
# Option 1.
pg_dump -U postgres -d contacts -f contacts.sql
# Option 2.
pg_dump -U postgres -F p contacts > contacts.sql
```

The database will be exported to the volume's path.

#### Import the database

[Resource](https://www.postgresqltutorial.com/postgresql-administration/postgresql-restore-database/)

```bash
make connect
psql -U postgres
create database contactsnew;
\q
cd /home/postgres/data
# Stop in case of error.
psql -U postgres --set ON_ERROR_STOP=on -f contacts.sql contactsnew
# Add schema.
psql -U postgres
\c contactsnew
SET search_path TO contacts, public;
```

### Connect with DBeaver

DBeaver configuration:

- IP: 0.0.0.0

### Stop container

```bash
make stop
```

