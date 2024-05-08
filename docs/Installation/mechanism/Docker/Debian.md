
# Debian
This is assuming a fresh installation of Debian 10.
## Install Docker
```bash
sudo apt-get install curl
curl https://releases.rancher.com/install-docker/19.03.sh | sh
```
Or follow the docker installation guide.
<https://docs.docker.com/engine/install/debian/>

## Run the Container
```bash
docker volume create fts_data

docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/host/system/folder --name fts --restart unless-stopped freetakteam/freetakserver:1.1.2
```

Alternatively, you can use the example `docker-compose.yml` [available here](https://github.com/FreeTAKTeam/FreeTAKServer-Docker/blob/main/docker-compose.yml)
by copying `docker-compose.yml` into a directory and
then doing `docker-compose up` or `docker-compose up -d` to bring the container up,
and in the background, respectively.
The `docker-compose.yml` uses a bind mount to `./data`.