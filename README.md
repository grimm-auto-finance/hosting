# hosting

## Usage

Place this repository in the same directory as the [frontend](https://github.com/tli-group-4-grimm/frontend) and the [backend](https://github.com/tli-group-4-grimm/backend), then copy `example.env` to `.env` and fill in the necessary credentials.

### Development

```sh
docker-compose -f docker-compose-dev.yaml up
```

### Production

```sh
cp Caddyfile-example Caddyfile
```

Replace `<hostname>` in `Caddyfile` with the hostname of your server, for example: `http://localhost`

```sh
docker-compose up
```
