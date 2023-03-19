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
    (2, 'Foo Name','Bar Surname');
# Exit the container.
\q
```

### Export and import the database

#### Export the database

[Resource](https://kinsta.com/docs/import-export-postgresql-database-command-line/#import-a-postgresql-database).

```bash
make connect
pg_dump -U postgres -d contacts > contacts.sql
```

#### Import the database

[Resource](https://kinsta.com/docs/import-export-postgresql-database-command-line/#import-a-postgresql-database).

First, connect to the container:

```bash
make connect
psql -U postgres
```

If the database does not exit:

```bash
pg_dump -U postgres < contacts.sql
```

The previous command will import the data to the db postgres, not to the db contacts.

### Stop container

```bash
make stop
```

