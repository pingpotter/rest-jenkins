SHELL := /bin/bash

build:
	docker build \
		-f Dockerfile \
		-t rest-api:1.0 \
		--build-arg BUILD_DATE=`date -u +”%Y-%m-%dT%H:%M:%SZ”` \
		.

