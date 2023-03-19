## Run

### Pull Docker image

Pull image (available versions at this [link](https://hub.docker.com/_/postgres/)).

```bash
docker pull postgres:15.2
```

### Create volume

Create volume to store the database data:

```bash
docker volume create db_postgres
```

### Run container

Start a PostgreSQL instance:

```bash
docker run \
    --rm \
    -d \
    --name postgres-container \
    -v db_postgres:/home/postgres/data \
    -e POSTGRES_PASSWORD=mysecretpassword \
    -e PGDATA=/home/postgres/data \
    postgres
```

Explanation:

- PGDATA: tells PostgreSQL where it should store the database.

### Create table

To connect to the db we have to connect to the `postgres-container` container as the user `postgres` using `psql`.

```bash
docker exec -it postgres-container /bin/bash
psql -U postgres
```

This can be done with only one command:

```bash
docker exec -it postgres-container psql -U postgres
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

### Stop container

```bash
docker stop postgres-container
```

## Resources

Create db:

<https://phoenixnap.com/kb/deploy-postgresql-on-docker>

Work with the volume:

<https://rhiyo.github.io/post/2021-4-21-running-postgres-in-docker-container-with-mounted-volume/>

