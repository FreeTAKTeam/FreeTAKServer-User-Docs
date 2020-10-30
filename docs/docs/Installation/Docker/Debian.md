# Debian
This is assuming a fresh installation of Debian 10.
## Install Docker
```bash
sudo apt-get install curl
curl https://releases.rancher.com/install-docker/19.03.sh | sh
```
Or follow the docker installation guide.
https://docs.docker.com/engine/install/debian/

## Run the Container
```bash
docker volume create fts_data

docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/host/system/folder --name fts --restart unless-stopped freetakteam/freetakserver:1.1.2
```