## Jsonnet helpers
JSONNET_ARGS=-J ./lib -J ./vendor -J .
JSONNET_TEST_FILES=$(wildcard ./*/tests/test.jsonnet)
JSONNET_PHONY_GOLDEN=$(patsubst %.jsonnet,%-golden.json,$(JSONNET_TEST_FILES))
JSONNET_PHONY_DIFF=$(patsubst %.jsonnet,%.diff,$(JSONNET_TEST_FILES))

TANKA_CONTAINER_CMD:=docker run --rm \
  -u="$(shell id -u):$(shell id -g)" \
  -v $$(pwd):/src/ \
  --workdir /src/ \
  grafana/tanka:latest

## Install jsonnetfile.json with jsonnet-bundler
kind/up:
	@@jb install

## Format Jsonnet files with tanka
jsonnet/fmt:
	@@if ! $(TANKA_CONTAINER_CMD) fmt . ; then \
	  exit 1;\
	fi

## Run Jsonnet tests
jsonnet/test: jsonnet/install jsonnet/fmt jsonnet/diff

## Diff Jsonnet fils against expected golden 
jsonnet/diff: jsonnet/diff-help $(JSONNET_PHONY_DIFF)

%.diff: %.jsonnet
	diff -u $(*)-golden.json <(jsonnet $(JSONNET_ARGS) $(<))

%.parse: %.jsonnet
	jsonnet $(JSONNET_ARGS) $(<) > /dev/null

%-golden.json: %.jsonnet
	jsonnet $(JSONNET_ARGS) $(<) > $(@)

## Generate expected golden files from Jsonnet
jsonnet/gen-golden: $(JSONNET_PHONY_GOLDEN)

## Help regarding Jsonnet diff
jsonnet/diff-help:
	@echo "NOTE: if the 'jsonnet/diff' target fails, review output and run:"
	@echo "      $(MAKE) jsonnet/gen-golden jsonnet/diff"
	@echo
