# Upgrading Existing Container
To upgrade the container to a new version you simply stop the container running the version you wish to upgrade from, and start a container running the version you want to upgrade to.  To have data transfered between versions you need to have used a volume during the initial set up.

```bash
docker stop fts
docker rm fts
docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/data --name fts --restart unless-stopped freetakteam/freetakserver:{New FTS version}
```
