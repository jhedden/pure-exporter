IMAGE_NAMESPACE ?= genegatpure
IMAGE_NAME ?= pure-helper
IMAGE_TAG ?= 1.0

RUN_PORT = 9000:9000

default: build

.PHONY: all
all: build test

.PHONY: build
build: Dockerfile requirements.txt .dockerignore $(wildcard *.py)
	docker build . -f Dockerfile -t $(IMAGE_NAMESPACE)/$(IMAGE_NAME):$(IMAGE_TAG)

.PHONY: test
test:
	docker run --rm -p $(RUN_PORT) $(IMAGE_NAMESPACE)/$(IMAGE_NAME):$(IMAGE_TAG)

.PHONY: release
release:
	@[ "$(VERSION)" ] || ( echo "$@ needs VERSION variable"; exit 1 )

	git tag "v$(VERSION)"
	git tag "$(IMAGE_TAG)" --force
	git push --force --tags
