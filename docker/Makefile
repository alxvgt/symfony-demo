IMAGE_NAME 					= qa-tracker
CONTAINER_NAME				= c_${IMAGE_NAME}

DOCKER 					= sudo docker
CONTAINERS_LIST 		= $(DOCKER) ps -a -q
IMAGES_LIST 			= $(DOCKER) images -q
UNTAGGED_IMAGES_LIST 	= $(DOCKER) images -f "dangling=true" -q

##
## Project
## -------

.DEFAULT_GOAL := help
help: ## Show this help message
help:
	@grep -E '(^[a-zA-Z_-]+:.*?##.*$$)|(^##)' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[32m%-20s\033[0m %s\n", $$1, $$2}' | sed -e 's/\[32m##/[33m/'
.PHONY: help

##
## Tools
## -----

build: ## Build image
build:
	$(DOCKER) build . -t ${IMAGE_NAME}

run: ## Run image
run: build
	$(DOCKER) run --rm --detach --name ${CONTAINER_NAME} ${IMAGE_NAME}

connect: ## Connect to the container
connect:
	$(DOCKER) exec -ti ${CONTAINER_NAME} /bin/bash

rm: ## Stop and remove the conainer
rm:
	$(DOCKER) rm -f ${CONTAINER_NAME}

rmi: ## Stop and remove the conainer
rmi:
	$(DOCKER) rmi -f ${IMAGE_NAME}

containers-list: ## List all containers
containers-list:
	$(DOCKER) ps -a

images-list: ## List all images
images-list:
	$(DOCKER) images -a

##