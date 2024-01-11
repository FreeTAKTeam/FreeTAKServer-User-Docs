---
status: current
---
# Container Quick-Start
## Runtimes
Compatible with Podman or docker runtimes.

## Host expectations
FreeTAKServer is **server** software, and should be treated as such. Installation onto a desktop environment will require
additional configuration that is usually only helpful if you want to do development.

The use of Linux is highly encouraged, as this is the industry standard host OS for containers.

**YOU CANNOT USE DOCKER DESKTOP ON YOUR WINDOWS PC.** Docker Desktop does not provide the ability to use bind-mounted
volumes, which are required in this iteration to allow the server operator to easily change the configuration files.



## Container Repository

Please find all of our container images on [the GitHub Container Repository.](https://github.com/orgs/FreeTAKTeam/packages)

You can obtain the latest images of the server and web UI by running the following commands.
Please note the use of GHCR instead of dockerhub, and adjust accordingly.

## Setup
### Installation Directory
A directory in which to store configuration and database files is required. Please ensure the permissions for this directory
allow container runtimes full `RWX` access recursively, and if using a selinux enabled OS, ensure the context is set for containers.
For more information on this process, visit your OS provided documentation.

### Compose

A [sample compose file](https://github.com/FreeTAKTeam/FreeTAKHub-Installation/blob/main/containers/example-compose.yaml)
is provided to speed up your setup. If you do not have any other compose files, then this can be placed in the same directory
created earlier, and renamed to `compose.yaml`. Ensure that if you do not place the compose file in the same directory that
you update the volume path to the correct directory.

If you expect to run these images as part of a larger file, then you can use the sample compose file as
sensible defaults and append to your pre-existing compose file.

Once all the directories and files are set, both components can be activated by running
```Bash
podman-compose up -d
```

Or for docker runtime users

```Bash
docker compose up -d
```

### Configuration
On first run, the appropriate configuration files will be created in the indicated directory.

From this point, you should stop the containers before editing the configuration files.

```Bash
podman-compose down
```
or
```Bash
docker compose down
```

From this point, please follow the Linux installation guide for information regarding the configuration files.

## Persistent Data

All persistent data is stored to /data and may be volume mounted.
The host volume needs to be owned by user and group 1000.