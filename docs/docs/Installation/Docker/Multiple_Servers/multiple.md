# Warning! Old Documentation Ahead!

The documentation below is for the **OLD** FTS container implementation and is not correct.

If you are following these instructions, you will probably not get the result you want.

New documentation is in the works, and will be released ASAP.

---

# Multiple Servers on Single Host

It is possible to run FreeTakServer multiple times on a single host by changing the port numbers.

If you follow an installation guide for your target platform and have a container running named `fts` using the default ports, this will explain how to run a second server on non default ports.

## Limitations
Currently due to a bug in the ATAK client you will need to share packages across all FTS servers on the same host.  The additional servers will use the first server, using the default port of 8080 for data packages.

## Running an aditional container

```bash
docker volume create fts_data2

docker run -d -p 8088:8087/tcp -e FTS_CONNECTION_MESSAGE="Server 2" -e FTS_SAVE_COT_TO_DB="True" -v fts_data2:/host/system/folder --name fts2 --restart unless-stopped freetakteam/freetakserver:1.1.2
```

We can use this command as a template to run as many FTS server instances as we would like on a single host by changing the name of the container and the ports FTS is running on.
So long as we avoid collisions on ports and names, if we have the resources we can run multiple servers with ease.
