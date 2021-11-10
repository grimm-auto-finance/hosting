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

Replace `<public_base_url>` in `Caddyfile` with the hostname of your server, for example: `https://example.com`

```sh
docker-compose up
```

### Ansible

Create an inventory file, then run the following command to deploy the project to all hosts, make sure you specify the inventory:

```sh
ansible-playbook -i $INVENTORY playbooks/deploy.yaml
```

The playbooks `start`, `stop`, and `restart` can also be used to perform the actions their names suggest. Note that `restart` doesn't run `docker-compose restart`, it uses `stop` and then `start` to ensure that an updated compose file will be respected.

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
