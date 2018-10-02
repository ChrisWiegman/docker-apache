NAMESPACE := ufhweb
NAME := apache
VERSION := 2.4-wp-multi-subdir

all: \
	build \
	push

build:
	docker build --no-cache  . -t $(NAMESPACE)/$(NAME):$(VERSION)
	docker build . -t gitlab.ahc.ufl.edu:4567/webservices/dev-ops/docker/$(NAME):$(VERSION)

push:
	docker push $(NAMESPACE)/$(NAME):$(VERSION)
	docker push gitlab.ahc.ufl.edu:4567/webservices/dev-ops/docker/$(NAME):$(VERSION)

.PHONY: \
	all \
	build \
	push
