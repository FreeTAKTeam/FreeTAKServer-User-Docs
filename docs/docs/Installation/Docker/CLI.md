#CLI Access
## Accessing the CLI
With the docker container isolating the running instance you also need to use docker to access the cli.
```bash
docker exec -it fts python3 -m FreeTAKServer.views.CLI
```
This will open a CLI instance attached to the process running in the container.

With the CLI open in your terminal you can view supported commands by running `help`
