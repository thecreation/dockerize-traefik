# Dockerize Traefik

## Prerequisites
* [Docker](https://docs.docker.com/install/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [Traefik](https://docs.traefik.io/)

## Up and Running

1. Create a directory that will serve as the home for your docker services.

```sh
mkdir /data && cd /data
```

2. Clone this repo into the newly created directory as "reverse-proxy".

```sh
git clone https://github.com/thecreation/dockerize-traefik.git && cd reverse-proxy
```

3. Create `.env` file and modify the variables to fit your needs.

```sh
cp .env-example .env
vim .env
```

Update `TRAEFIK_AUTH` with the generated credentials below:

```sh
docker run \
  --entrypoint htpasswd \
  registry:latest -nb admin password
```

Fill the server ip to `TRAEFIK_IPWHITELIST` to restrict ip access.

4. Create "acme.json" and update file permissions.

```sh
touch letsencrypt/acme.json && chmod 600 letsencrypt/acme.json
```

5. Create the docker network.

```sh
docker network create reverse_proxy
```

6. Spin up the service.

```sh
docker-compose up -d
```

done!

## Web dashboard and ping

Access the links below in the browser

- https://proxy.localhost/dashboard
- https://proxy.localhost/ping

## Troubleshooting and logging

Run the following command:

```sh
tail -f logs/accessLog.txt
tail -v logs/traefik.log
```