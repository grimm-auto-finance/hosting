# hosting

## Usage

### Docker

Place this repository in the same directory as the [frontend](https://github.com/tli-group-4-grimm/frontend) and the [backend](https://github.com/tli-group-4-grimm/backend), then copy `example.env` to `.env` and fill in the necessary credentials.

#### Development

```sh
docker-compose -f docker-compose-dev.yaml up
```

#### Production

```sh
cp Caddyfile-example Caddyfile
```

Replace `<hostname>` in `Caddyfile` with the hostname of your server, for example: `http://localhost`

```sh
docker-compose up
```

### Windows

Since file system events are not supported with Docker bind mounts on Windows, hot-reloading is not possible when running inside Docker, so it is necessary to run things manually when developing on Windows. Begin by exporting the necessary environment variables, replacing the empty strings with their respective values:

```ps1
# in ../frontend
$Env:VITE_BACKEND_BASE_URL = ""

# in ../backend
$Env:SENSO_API_KEY = ""
$Env:SENSO_API_BASE_URL = ""
```

Then run the following commands in each of the three repositories, in any order, to start the project:

```ps1
# in ../frontend
pnpm run dev

# in ../backend
gradle run

# in . (hosting)
caddy run -config .\Caddyfile-windows
```

Note that with this setup, there is hot-reloading for the frontend, but not the backend. To restart the backend after a change, cancel the current `gradle run` command with Control-C, then run:

```ps1
gradle build
gradle run
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md)
