---
status: warning
---


# Install

The official Docker image for FreeTAKServer.

## Usage
When using this docker container we suggest
that you use the `--restart unless-stopped` flag as shown in the examples. 
This will ensure that the service automatically starts with the host
and will restart if it encounters an error and crashes.
The port mappings in the examples are required to make the service accessible to hosts.
All environment variables are optional.
All data is stored in a single directory for ease of persistent data between container versions.

{!Installation/Docker/Quick_Start.md!}

### Ports
The docker image runs the ports on the same defaults as FreeTAKServer.
You can use the `-e` flag to map these ports to different ports
or to run multiple FreeTAKServer's concurrently on the same host.

### Environment Variables
All environment variables will apply to FTS.
However, these are some additional ones specific to this docker image.

| Variable Name           | Definition                                                                                |
|-------------------------|-------------------------------------------------------------------------------------------|
| FTS_CONNECTION_MESSAGE  | The text of the message sent upon connection                                              |
| FTS_COT_TO_DB           | A boolean indicating ?                                                                    |
| APPPORT                 | Allows hosting FTS UI from a different port                                               |
| APIIP                   | Allows the FTS UI to specify a different API port. Defaults the `IP` environment variable |
| APIPORT                 | Allows the FTS UI to specify a different API port                                         |
| APIPROTOCOL             | Allows the FTS UI to specify a different API protocol                                     |
| WEBMAPIP                | Allows the FTS UI to specify a different webmap IP                                        |
| WEBMAPPORT              | Allows the FTS UI to specify a different webmap port                                      |
| WEBMAPPROTOCOL          | Allows the FTS UI to specify a different webmap protocol                                  |

### Storage
All data in this container is stored in `/data`.
This directory will need to be stored to a volume if you wish to persist data between updates.

If you use a storage volume you may need to inspect the docker volume to find where it saved the data.  
```bash
docker inspect fts_data
````
It will return something similar to this:
```json
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

The `docker-compose.yml` example utilizes a bind mount to `./data` in the same directory.

## Additional Architectures
Currently, the container is being cross compiled for `linux/amd64`, `linux/arm64` and `linux/arm/v7`.
If additional processor architectures are needed please open an issue and request a new one.

## Docker Hub Page
[https://hub.docker.com/r/freetakteam/freetakserver](https://hub.docker.com/r/freetakteam/freetakserver)
