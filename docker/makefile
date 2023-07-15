CONTAINER_DATA_PATHNAME=/home/postgres/data
CONTAINER_DB_DUMP_FILE_PATHNAME=$(CONTAINER_DATA_PATHNAME)/db-export.sql
CONTAINER_NAME=postgres-container
CONTAINER_VOLUME=db_postgres
IMAGE_NAME=postgres
IMAGE_VERSION=15.2
POSTGRES_USER=postgres
POSTGRES_PW=pw

pull-image:
	docker pull $(IMAGE_NAME):$(IMAGE_VERSION)

create-volume:
	docker volume create $(CONTAINER_VOLUME)

run:
	# PGDATA: tells PostgreSQL where it should store the database.
	docker run \
		--rm \
		-d \
		--name $(CONTAINER_NAME) \
		-p5432:5432 \
		-v $(CONTAINER_VOLUME):$(CONTAINER_DATA_PATHNAME) \
		-e POSTGRES_PASSWORD=$(POSTGRES_PW) \
		-e PGDATA=$(CONTAINER_DATA_PATHNAME) \
		$(IMAGE_NAME)

connect:
	docker exec -it $(CONTAINER_NAME) /bin/bash

connect-psql:
	docker exec -it $(CONTAINER_NAME) psql -U $(POSTGRES_USER)

export-db:
	echo "[DEBUG] Init dump database"
	docker exec $(CONTAINER_NAME) \
		pg_dump -U postgres -d contacts -f $(CONTAINER_DB_DUMP_FILE_PATHNAME)
	echo "[DEBUG] Init export dumped database"
	docker cp $(CONTAINER_NAME):$(CONTAINER_DB_DUMP_FILE_PATHNAME) /tmp

stop:
	docker stop $(CONTAINER_NAME)

