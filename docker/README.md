## Steps

Pull image (available versions at this [link](https://hub.docker.com/_/postgres/)).

```bash
docker pull postgres:15.2
```

Start a Postgres instance:

```bash
docker run \
    --rm \
    -d \
    --name postgres-container \
    -e POSTGRES_PASSWORD=mysecretpassword \
    postgres
```

Now, we:

- Connect to the `postgres-container` container name as the user `postgres`.
- Enable psql.

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

## Resources

Tutorial: <https://phoenixnap.com/kb/deploy-postgresql-on-docker>
