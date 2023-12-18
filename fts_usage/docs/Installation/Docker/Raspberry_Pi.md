# Warning! Old Documentation Ahead!

The documentation below is for the **OLD** FTS container implementation and is not correct.

If you are following these instructions, you will probably not get the result you want.

New documentation is in the works, and will be released ASAP.

---

# Raspberry Pi 4/Raspberry Pi 3
It is recommended to use a Raspberry Pi 4 with 4GB or 8GB of ram.

This guide assumes that you have a clean install of Raspberry Pi OS or Raspbian.
You may also use the 64 bit Ubuntu 20.04 server prepared for the Raspberry Pi 4.

#### Install Docker
```bash
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install curl 
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```
#### Run the Container
```bash
docker volume create fts_data

docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/host/system/folder --name fts --restart unless-stopped freetakteam/freetakserver:1.1.2
```

Alternatively, you can use the example `docker-compose.yml` [available here](https://github.com/FreeTAKTeam/FreeTAKServer-Docker/blob/main/docker-compose.yml) by copying `docker-compose.yml` into a directory and then doing `docker-compose up` or `docker-compose up -d` to bring the container up, and in the background, respectively. The `docker-compose.yml` uses a bind mount to `./data`.

# Older Pi's
Raspberry Pi's prior to the Pi3 have not been tested, and would not be recommended for use.
