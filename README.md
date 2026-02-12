# Example for issue #20 (HTTPS supports)

This example will override the original nginx conf with one supporting HTTPS. You will need to rewrite all the project configuration (replaces `proxy_pass` with your own value, in this example `http://registry:5000` is fine).

Generating a self signed certificate:

```bash
openssl req -newkey rsa:2048 -nodes -keyout nginx/privkey.pem -x509 -days 3650 -out nginx/fullchain.pem
```

The UI will be available here : https://localhost

## Troubleshoots

### Exec into broken containers

```bash
docker compose run --rm --entrypoint /bin/sh nginx
```

## Quickstart

```bash
# Pull an example image
docker pull alpine
# Tag the image
docker tag alpine localhost/my-alpine
# Push the image into the self-hosted instance
docker push localhost/my-alpine


docker pull hello-world
docker tag hello-world localhost/hello-world
docker push localhost/hello-world
```
