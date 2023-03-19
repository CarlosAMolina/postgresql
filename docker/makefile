CONTAINER_DATA_PATHNAME=/home/postgres/data
CONTAINER_NAME=postgres-container
CONTAINER_VOLUME=db_postgres
IMAGE_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PW=mysecretpassword

create-volume:
	docker volume create $(CONTAINER_VOLUME)

run:
	docker run \
		--rm \
		-d \
		--name $(CONTAINER_NAME) \
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
