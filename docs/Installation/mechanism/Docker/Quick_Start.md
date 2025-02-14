
# Container Quick-Start
Please use this guide if you have never used containers before.
If you are familiar with container infrastructure then you may wish to simply view the [sample compose file](https://github.com/FreeTAKTeam/FreeTAKHub-Installation/blob/main/containers/example-compose.yaml) that we provide.


## Runtimes
A runtime is what runs the container or containers you install.

There are two main runtimes: Podman and Docker.

Docker is the original runtime and is widely supported but has some issues with security, such as running containers by default in a root-ful way.

Podman is a newer runtime that is shipped by default on RHEL/Fedora/CentOS systems. Containers in this runtime are by default run root-less, preventing many security issues.

Our containers are made and tested to be compatible with Podman, which is the more restrictive runtime. As a result these containers should function on either choice. The most important part is to choose a runtime and use the correct invocations for it.

If you are on RHEL/Fedora/CentOS and similar family of systems, then you can likely invoke podman without additional installation.

If your system does not already have a runtime, install it with your package manager.

Check which one you have installed by running
```shell
podman --version
docker --version
```
If you have both, CHOOSE ONE and STICK WITH IT for the duration of the guide.

## Host expectations
The host is the computer/server/VM inside of which your runtime actually runs.

FreeTAKServer is, as the name suggests, **server software**, and should be treated as such. Installation onto a normal desktop environment requires additional effort and configuration that is typically useful only for development purposes.

The use of Linux is highly encouraged. This is the industry standard host OS for containers.

**WE WILL NOT SUPPORT RUNNING CONTAINERS ON DOCKER DESKTOP ON YOUR WINDOWS PC.**

Your Windows computer is not a good choice for hosting a server of any kind.

## Container Repository
A container repository is a location where you can obtain pre-built containers.

Some examples are docker.io and ghcr.io.

Please find all of our container images on [the GitHub Container Repository.](https://github.com/orgs/FreeTAKTeam/packages)

You can obtain the latest images of the server and web UI by running the following commands:
```shell
podman pull ghcr.io/freetakteam/freetakserver:latest
podman pull ghcr.io/freetakteam/ui:latest

OR

docker pull ghcr.io/freetakteam/freetakserver:latest
docker pull ghcr.io/freetakteam/ui:latest
```

Please note that we use GHCR instead of the more common dockerhub.

## Setup
### Installation Directory
Create a new directory in your home folder for this guide.
```shell
mkdir container
cd container
```

### Compose
A compose file is a way to automate the operation of one or many containers. In this case we have a [sample compose file](https://github.com/FreeTAKTeam/FreeTAKHub-Installation/blob/main/containers/example-compose.yaml) file with just the server and UI.

Download this file to your working directory.
```shell
wget https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/refs/heads/main/containers/example-compose.yaml -o compose.yaml
```

Open this file in the text editor of your choice
```shell
nano compose.yaml
```

and update some select configuration items with the indicated item
```yaml
FTS_IP: YOUR EXTERNAL URL HERE
```
Your external URL is your HOST COMPUTER'S EXTERNAL IP ADDRESS unless you have a very advanced configuration.

If you are running this behind your personal all-in-one cable modem/router/accesspoint combo then you probably need to do some port forwarding, however this is out of scope for this guide.

Once the configuration in your compose.yaml is to your liking, you can then simply run your compose file.
```shell
podman-compose -f compose.yaml up -d

OR

docker compose -f compose.yaml up -d
```

You can check how your containers are doing by running
```shell
podman logs freetakserver
podman logs freetakserver-ui

OR

docker logs freetakserver
docker logs freetakserver-ui
```

When done, you can stop everything by running
```shell
podman-compose -f compose.yaml down

OR

docker compose -f compose.yaml down
```
## Persistent Data

All persistent data is stored in the [volumes](https://docs.docker.com/engine/storage/volumes/) that are explicitly created in the sample compose file.

You can access it in your runtime volume store if needed, however you should probably NOT do this while the server is running.
