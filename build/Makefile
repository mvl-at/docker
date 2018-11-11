GIT = git
DOCKER = docker
CP = cp
DOCKER_TAG = mvlat
IMAGES = assets calendar rest web


fetch:
	$(GIT) submodule update --recursive --remote

build:
	for image in $(IMAGES); do \
		cd $$image; \
	  version=$$($(GIT) rev-parse --short HEAD); \
		tag1=$(DOCKER_TAG)/$$image:$$version; \
		tag2=$(DOCKER_TAG)/$$image:latest; \
		if [[ "$$($(DOCKER) images -q $$tag1)" == "" ]]; then \
			echo "building " $$tag1; \
			$(DOCKER) build -t $$tag1 -t $$tag2 .; \
		fi; \
		cd ..; \
	done

push:
	for image in $(IMAGES); do \
		$(DOCKER) push $(DOCKER_TAG)/$$image; \
	done

publish: fetch build push
