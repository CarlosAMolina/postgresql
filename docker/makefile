CONTAINER_DATA_PATHNAME=/home/postgres/data
CONTAINER_NAME=postgres-container
CONTAINER_VOLUME=db_postgres
IMAGE_NAME=postgres
IMAGE_VERSION=15.2
POSTGRES_USER=postgres
POSTGRES_PW=mysecretpassword

pull-image:
	docker pull $(CONTAINER_NAME):$(IMAGE_VERSION)

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

stop:
	docker stop $(CONTAINER_NAME)
