# Install

The official Docker image for FreeTAKServer.

## Usage
When using this docker container we suggested that you use the `--restart unless-stopped` flag as shown in the examples.  This will enure that the service automatically starts with the host and will restart if it encounters an error and crashes.  The port mappings in the examples are required to make the service accessable to hosts.  All environment variables are optional.  All data is stored in a single directory for ease of persistent data between container versions.

```bash
docker volume create fts_data

docker run -d -p 8080:8080/tcp -p 8087:8087/tcp -e FTS_CONNECTION_MESSAGE="Server Connection Message" -e FTS_SAVE_COT_TO_DB="True" -v fts_data:/data --name fts --restart unless-stopped freetakteam/freetakserver:1.1.2
```

### Ports
The docker image runs the ports on the same defaults as FreeTAKServer.  You can use the `-e` flag to map these ports to different ports or to run multiple FreeTAKServer's concurrently on the same host.

### Environment Variabls
```
FTS_CONNECTION_MESSAGE: Accepts a string to send to users when they connect.  Set to "None" to disable.
FTS_SAVE_COT_TO_DB: Accepts "True" or "False" setting to save CoTs to the DB.
FTS_ARGS: Arguments to pass on the command line, "-AutoStart True" is passed automatically.  
```

### Storage
All data in this container is stored in `/data`.  This directory will need to be stored to a volume if you wish to persist data between updates.

If you use a storage volume you may need to run `docker inspect fts_data` to find where it saved the data.  It will return something similar to this:
```
root@fts:/home/ubuntu# docker inspect fts_data
[
    {
        "CreatedAt": "2020-11-12T03:32:53Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/fts_data/_data",
        "Name": "fts_data",
        "Options": {},
        "Scope": "local"
    }
]
```


## Additional Architectures
Currently the container is being cross compiled for `linux/amd64`,  `linux/arm64` and `linux/arm/v7`.  If additional processor architectures are needed please open an issue and request a new one.

## Docker Hub Page
[https://hub.docker.com/r/freetakteam/freetakserver](https://hub.docker.com/r/freetakteam/freetakserver)
