# Warning! Old Documentation Ahead!

The documentation below is for the **OLD** FTS container implementation and is not correct.

If you are following these instructions, you will probably not get the result you want.

New documentation is in the works, and will be released ASAP.

---

This will run FreeTAKServer without persistent data storage with all default settings.
The data storage will be in memory.
```bash
docker run -d -p 8080:8080/tcp -p 8087:8087/tcp --name fts \
  --restart unless-stopped freetakteam/freetakserver:1.1.2
```


## Persistent Data

All persistent data is stored to /data and may be volume mounted.
The host volume needs to be owned by user and group 1000.

```bash
docker volume create fts_data

docker run -d -p 8080:8080/tcp -p 8087:8087/tcp \
  -e FTS_CONNECTION_MESSAGE="Server Connection Message" \
  -e FTS_COT_TO_DB="True" \
  -v fts_data:/data \
  --name fts \
  --restart unless-stopped \
  freetakteam/freetakserver:1.1.2
```

It is also possible to use an absolute path with a blind mount on the host instead of a proper volume.
For more information about volumes [https://docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/)

Alternatively, you can use the example `docker-compose.yml` [available here](https://github.com/FreeTAKTeam/FreeTAKServer-Docker/blob/main/docker-compose.yml)
by copying `docker-compose.yml` into a directory and
then doing `docker-compose up` or `docker-compose up -d` to bring the container up,
and in the background, respectively.
The `docker-compose.yml` uses a bind mount to `./data`.
