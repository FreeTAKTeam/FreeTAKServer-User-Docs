# Warning! Old Documentation Ahead!

The documentation below is for the **OLD** FTS container implementation and is not correct.

If you are following these instructions, you will probably not get the result you want.

New documentation is in the works, and will be released ASAP.

---

# Upgrading Existing Container
To upgrade the container to a new version you simply
stop the container running the version you wish to upgrade from,
and start a container running the version you want to upgrade to.
To have data transferred between versions you need to have used a volume during the initial set up.

```bash
docker stop fts
docker rm fts
docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/data --name fts --restart unless-stopped freetakteam/freetakserver:{New FTS version}
```

If using the `docker-compose.yml` file, perform the following:

```bash
docker-compose pull
docker-compose down
docker-compose up
# alternatively, use docker-compose up -d to run in the background
```