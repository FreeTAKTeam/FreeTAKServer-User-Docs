# Warning! Old Documentation Ahead!

The documentation below is for the **OLD** FTS container implementation and is not correct.

If you are following these instructions, you will probably not get the result you want.

New documentation is in the works, and will be released ASAP.

---

# CLI Access

## Accessing the CLI
With the docker container isolating the running instance you also need to use docker to access the cli.
```bash
docker exec -it fts python3 -m FreeTAKServer.views.CLI
```
This will open a CLI instance attached to the process running in the container.

With the CLI open in your terminal you can view supported commands by running `help`
