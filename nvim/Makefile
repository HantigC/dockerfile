IMAGE_NAME ?= hsc:nvim
CONTAINER_NAME ?= hsc-nvim
BASE_IMAGE ?= ubuntu:20.04
FROM_VOLUME ?= $(HOME)
TO_VOLUME ?= /data

.PHONY: all build run unall unbuild unrun

all: build run

build:
	docker image build \
		--build-arg BASE_IMAGE=$(BASE_IMAGE) \
		-t $(IMAGE_NAME) \
		-f Dockerfile \
		.


run:
	docker container run \
		--privileged \
		-it \
		-v $(FROM_VOLUME):$(TO_VOLUME) \
		-p 4568:8888 \
		--name $(CONTAINER_NAME) \
		$(IMAGE_NAME)

unrun:
	docker container rm $(CONTAINER_NAME)

unbuild:
	docker image rm $(IMAGE_NAME)

unall: unrun unbuild
