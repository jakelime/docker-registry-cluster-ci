ARG url_docker=docker.io
ARG PERSISTANCE_STORAGE=/datashare/docker-registry
FROM ${url_docker}/registry:2.8

ARG PERSISTANCE_STORAGE
RUN mkdir -p ${PERSISTANCE_STORAGE}

# Enable file persistance to the docker-volume
RUN ln -s ${PERSISTANCE_STORAGE} /var/lib/registry
