# Docker Registry - Self hosted solution

This solution is forked from example `#issue20` from
[jotix/docker-registry-ui](https://github.com/Joxit/docker-registry-ui).

## Example for issue #20 (HTTPS supports)

This example will override the original nginx conf with one supporting HTTPS. You will need to rewrite all the project configuration (replaces `proxy_pass` with your own value, in this example `http://registry:5000` is fine).

Generating a self signed certificate:

```bash
openssl req -newkey rsa:2048 -nodes -keyout nginx/privkey.pem -x509 -days 3650 -out nginx/fullchain.pem
```

The UI will be available here : `https://localhost`

## Quickstart

```bash
docker compose up

# UI will be available here : https://localhost

# By default, we use a custom port
docker pull hello-world # pull from docker.io official registry
docker tag hello-world localhost:10500/hello-world # tagging your local image pulled
docker push localhost:10500/hello-world # push to the self-hosted docker registry

docker pull busybox # pull from docker.io official registry
docker tag busybox localhost:10500/busybox # tagging your local image pulled
docker push localhost:10500/busybox # push to the self-hosted docker registry

# If you want to default to 443, you may change to `DOCKER_REGISTRY_PORT=443`
## If you running a single server on single host, this is nice
docker pull alpine
docker tag alpine localhost/my-alpine
docker push localhost/my-alpine
```

## Generating secrets

```bash

# HTTP_SECRET
python3 -c 'import secrets; print(secrets.token_hex(32))'

# Generates a secured secret key for use as password of 1+21 char in length
# The first char is always a letter, no dash and underscore for easy copypaste and url-safe.
## 22 chars password
python -c "import secrets, string; alph = string.ascii_letters + string.digits; print(secrets.choice(string.ascii_letters) + ''.join(secrets.choice(alph) for _ in range(21)))"
## 32 chars password
python -c "import secrets, string; alph = string.ascii_letters + string.digit

```

## Troubleshooting guides

### Exec into broken containers

```bash
docker compose run --rm --entrypoint /bin/sh nginx
```

### Garbage collection for Deleted images

```bash
container_name=${PROJECT_NAME:-dkcl}_dk_registry
docker exec $container_name registry garbage-collect /etc/docker/registry/config.yml
```

## Todo

- deleting images
  - did not manage to fix the delete images and cleanup. ohwells, leave it as it is then.
