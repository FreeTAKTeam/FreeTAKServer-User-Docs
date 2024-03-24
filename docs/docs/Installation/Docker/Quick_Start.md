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

### Quick Instructions
1. Copy the [`example-compose.yaml`](https://github.com/FreeTAKTeam/FreeTAKHub-Installation/blob/main/containers/example-compose.yaml)
file to your favorite directory.
2. Rename it to compose.yaml
3. Run the command

    For podman:
    ```shell
    podman-compose up
    ```
    
    For non-free runtime:
    
    ```shell
    docker-compose up
    ```

4. Then refer to other FTS documentation to do appropriate configuration using the environment variables exposed in the 
compose file.

### Additional Detail
A [sample compose file](https://github.com/FreeTAKTeam/FreeTAKHub-Installation/blob/main/containers/example-compose.yaml)
is provided to speed up your setup. T this can be placed in whatever directory you use for your container infrastructure
or a new directory that you create for this purpose. You will likely want to rename the compose file provided to 
`compose.yaml`.

If you expect to run these images as part of a larger compose file, then you can use the sample compose file as
sensible defaults and append it to your pre-existing compose file.

### Configuration
All configuration is handled by environment variables. For information on what the environment variables control, visit
the Container Overview page.

## Persistent Data
All persistent data is stored to a volume. Be careful not to purge your container runtime unless you want to lose it all.