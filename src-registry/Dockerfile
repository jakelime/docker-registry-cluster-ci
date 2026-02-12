ARG url_docker=docker.io
ARG REGISTRY_STORAGE_DIR=/var/lib/registry
FROM ${url_docker}/registry:2.8

RUN mkdir -p /datashare/docker-registry
RUN ln -s /datashare/docker-registry ${REGISTRY_STORAGE_DIR}
