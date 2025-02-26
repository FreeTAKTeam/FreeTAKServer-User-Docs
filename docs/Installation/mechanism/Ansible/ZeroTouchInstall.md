
# Zero Touch Installation (ZTI) 

The ZeroTouch (ZT or ZTI) installation is the easiest way to install FTS. 
Has been tested on the [cloud](../../platform/Cloud/AWS.md) and
on the [RasberryPi](../../platform/RaspberryPi/Installation.md);
however, only on Digital Ocean cloud (by virtue of appropriate defaults) you will have the optimal experience,
where all is installed and configured. 

The `ZTI` can be run on different platforms,
make sure you have chosen the platform correctly,
or you will need to update configuration files later.

## Quick start
in most cases use this command to install FTS
```
wget -qO - bit.ly/freetakhub2 | sudo bash
```
in a cloud environment (e.g. Digital Ocean), this will have you up and running in 5 minutes. For more option continue to read

## `ZTI` Usage
The `ZTI` provides usage documentation.
This information is the most current.
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --help
```

The following instructions provide examples where
these options are demonstrated.

## Zero Touch Deployment Diagram
This `ZTI` installs and configures FreeTAKHub components on a single device.

!!! note
    The following list and diagram are not exhaustive. 

1. FreeTAKServer (FTS): The core server that interfaces with TAK-enabled clients
2. FreeTAKServer User Interface (FTS-UI): A web-based user interface.
3. Video Server:  based on RTSP Simple Server. Handles video streaming.
4. Server:  Handle integration services (see below)
5. FreeTAKHub Integration Server: Based on Node Red. Handles FTS integrations like SALUTE reports & video checking services (checks if videos are running and notifies FTS).
6. FreeTAKHub Voice Server: Uses [Murmur](https://github.com/mumble-voip/mumble) or Mumble VOIP Server for voice chatting.
7. FreeTAKHub Webmap: A mapping component on the web interface.

![FreeTAK 2.1 ZTI deployment](../../images/zero-touch-deply-default.png)

### Services Status
This command will output the status of these services
```
sudo systemctl status fts.service fts-ui.service mumble-server.service nodered.service rtsp-simple-server.service
```

Note:: `rtsp-simple-server` is also known as `mediamtx`.

 [how to start / stop / enable  a service?](../../../Troubleshooting/Service.md)


## Platform Specific Instructions

The `ZTI` only works on Linux systems.

### Cloud Server (with automatic IP address discovery)

In this mode, `ZTI` guesses your IP address using
`curl ifconfig.me/ip`.
If this does not give the appropriate IP address you will need to provide it.
Run one of the following (equivalent) commands to start the [ZeroTouch](../../mechanism/Ansible/ZeroTouchInstall.md) installer.
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash
```
??? tip "Alternate, full path."
    ```bash
    wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash
    ```

### Explicit IP Address

Implicitly, the `ZTI` guesses your IP address using `https://ifconfig.me/ip`.
When installing on the devices not on the public internet
it is unlikely that this is what you want.
There are several ways to discover a candidate IP address, here are some.

!!! warning
    The IP address should be stable; on reboot you may get a different IP address.
    You should take steps to ensure the IP address does not change without your knowledge.

Show the assigned IPv4 LAN addresses:
```bash
ip -4 addr
```
??? tip "Extract specific LAN addresses"
    Wired, ethernet, RJ45
    ```bash
    ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
    ```
    WiFi
    ```bash
    ip -4 addr show wlan0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
    ```

On the public internet:
```bash
curl ifconfig.me/ip
```

It will be helpful to create an environment parameter
to remember the IP address (MY_IPA) you have selected.
```bash
export MY_IPA=<the appropriate IP address>
```

!!! note "Here are complete examples capturing the IP address:"
    Wired, ethernet, RJ45
    ```bash
    export MY_IPA=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
    ```
    WiFi
    ```bash
    export MY_IPA=$(ip -4 addr show wlan0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
    ```

## Run the Zero Touch Installer (ZTI)

With an appropriate IP address in hand you can run the `ZTI`.
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IPA}
```
??? tip "Alternate, full path."
    ```bash
    wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash -s -- --ip-addr ${MY_IPA}
    ```

## How `ZT` works
The command `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IPA} `
is a combination of several commands and options used together to perform a specific task.
Here's a breakdown of what each part of the command does:

wget
: This is the command for a popular network downloader utility.

-q
: This option tells wget to operate in quiet mode, which suppresses the usual output.

O -
: as the capital letter 'o'.
The -O - option tells wget to redirect the downloaded content to standard output (stdout)
instead of saving it to a file. The - character is used here to denote stdout.

bit.ly/freetakhub2
: This is a shortened URL using the bit.ly service.
It redirects to a longer URL from which wget will download content.

|
: This is a pipe.
It takes the output of the command on its left (wget in this case)
and uses it as the input for the command on its right.


sudo
: This command is used to execute the following command (bash) with superuser (root) privileges.
It's required for commands that need higher permissions to run,
typically for installing software or modifying system files.

bash
: This is the command to invoke the Bash shell. When used without a filename,
bash will read and execute commands from its standard input (which, in this case, is the output of wget).

-s
: If this option is present, or if no arguments remain after option processing,
then commands are read from the standard input.
This option allows the positional parameters to be set when invoking an interactive shell
or when reading input through a pipe.

--
: End of options.
Anything further on the command line is an argument, not an option.

--ip-addr ${MY_IPA}
: Provide an argument to configure FTS with a specific, `MY_IPA`, IP address.

??? warning "Variable Expansion"
    The command `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IPA}` presumes that the variable `MY_IPA` has been set.
    If `export MY_IPA=192.168.1.100` then, the statement expands to 
    `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr 192.168.1.100`,
    and NOT to `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr $192.168.1.100`


Putting it all together, `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IPA}`
downloads the content from the URL shortened as `bit.ly/freetakhub2`,
then immediately executes that content as a bash script with superuser privileges.
A specific IP address (stored in the variable `MY_IPA`, expanded) is provided as an argument to configure FTS.

## Atypical Optional Behavior

As mentioned previously you can see several atypical behaviors are available.
They are documented here.

### `ZTI` `--help` Argument
??? tip "show usage."
    ```bash
    wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --help
    ```

### `ZTI` `--verbose` Argument
??? tip "Verbose output."
    ```bash
    wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --verbose
    ```
    Print script debugging information.

### `ZTI` `--pypi` Argument
??? tip "Explicitly set the URL for the PYPI repository"
    ```bash
    wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --pypi https://test.pypi.org
    ```
    Generally, `pip` acquires python packages from https://pypi.org,
    this option makes it possible to use an alternate repository.

### `ZTI` Legacy Argument

If you are still wanting to use the previous "legacy" version,
use this option.

Note:: the legacy version only works with Ubuntu 20.04

```console
wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --legacy
```
??? tip "Alternate, environment variable."
    ```console
    wget -qO - bit.ly/freetakhub2 | sudo INSTALL_TYPE=legacy bash
    ```

### `ZTI` `--repo` Argument

??? tip "testing a forked repository."
    ```console
    export MY_IPA=10.2.118.126
    export MY_REPO=babeloff
    wget -qO - https://raw.githubusercontent.com/${MY_REPO}/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash -s -- --ip-addr ${MY_IPA} --repo https://github.com/${MY_REPO}/FreeTAKHub-Installation.git 
    ```

## Operation

Now that your shiny new FTS system has been installed,
it is time to make sure it is nominally working.

### FTS User Interface

* http://[use MY_IPA here]:5000/index
* username: `admin`
* password: `password`

### FTS Hub : Node-Red

* http://[use MY_IPA here]:1880
* username: `admin`
* password: `password`

!!! note
    When trying to log in for the first time, you might get a warning along the lines of `FTS Server is Not Reachable at {your IPA}`.
    [Restarting the services](../../../administration/Operation/fts-service-mgmt.md) can help.

### Node-Red issues

Currently there is a know issue regarding the Node-Red integration. The following is based on the [YouTube-Video by Cßrv0 (external)](https://www.youtube.com/watch?v=Yaa1viiC6_M&t=25m0s). If you run into troubles following the text description, please refer to this video for additional help.

This is due to a problem with nodeJS so we need to reinstall Node-Red at version 20:

```bash
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered) --node20
```

Accept the prompts following up depending on your needs.

Finally you'll need to restart Node-Red:

```bash
sudo systemctl enable nodered.service
sudo systemctl start nodered.service 
```

There still will be a known error regarding `worldmap` itself. To fix this you'll need to adjust the corresponding node within Node-Red.

Login into Node-Red again and go to the `FTH Webdmap` flow and edit the `FTS Server` TCP node (with the woarning below). Change the properties to:

```
server: ${your IPA}
port: 8087
```

Redeploy the flows. This should fix the issues.

!!! note
    Don't worry when your clients and COTs dont show up immediately. The worldmap needs some time to get up to date.

### Reconfiguration

`ZeroTouch` will have configured the system and started the services for you. 
However, there are many corner cases which `ZeroTouch` may miss.
Many (if not all) of the choices made by `ZeroTouch` are written to stdout.
I recommend that you validate the properties in that output.
You should stop the fts services prior to reconfiguration,
and you must start (restart) the fts services after reconfiguration.

* [Service Management](../../../administration/Operation/fts-service-mgmt.md)
* [Configuration](../../../administration/Operation/fts-config.md)

### Try out the TAK Clients

Now try out TAK clients after connecting them to the shiny new FTS server.

* [Try Me](../../../Usage/Connecting_ATAK.md)
