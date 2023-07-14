> **Warning**
> The Docker Installation Method directs users to a Dockerhub Registry whose images haven't been updated in ~2 years and whose source code has been archived: The former Docker image for FreeTAKServer, this repo is now archived. Please use the FTS rpository to get the current Container.
> 

This will run FreeTAKServer without persistent data storage with all default settings.
```bash
docker run -d -p 8080:8080/tcp -p 8087:8087/tcp --name fts --restart unless-stopped freetakteam/freetakserver:1.1.2
```
## Persistent Data

All persistent data is stored to /data and may be volume mounted.  The host volume needs to be owned by user and group 1000.
```bash
docker volume create fts_data

docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/host/system/folder --name fts --restart unless-stopped freetakteam/freetakserver:1.1.2
```
It is also possible to use an absolute path with a blind mount on the host instead of a proper volume.  For more information about volumes [https://docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/)
