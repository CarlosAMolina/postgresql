## Steps

Pull image (available versions at this [link](https://hub.docker.com/_/postgres/)).

```bash
docker pull postgres:15.2
```

Start a Postgres instance:

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

## Resources

Tutorial: <https://www.docker.com/blog/how-to-use-the-postgres-docker-official-image/>
