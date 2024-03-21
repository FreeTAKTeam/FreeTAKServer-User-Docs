---
status: current
---

# Zero Touch Installation (ZTI)
The ZeroTouch (ZT or ZTI) installation is the easiest way to install FTS. 
Has been tested on the [cloud](../../platform/Cloud/AWS.md) and
on the [RasberryPi](../../platform/RaspberryPi/Installation.md);
however, only on Digital Ocean cloud (by virtue of appropriate defaults) you will have the optimal experience,
where all is installed and configured. 

The `ZTI` can be run on different platforms,
make sure you have chosen the platform correctly,
or you will need to update configuration files later.

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

Note: The following list and diagram are not exhaustive. 

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
sudo systemctl status fts.service fts-ui.service mumble-server.service nodered.service mediamtx.service
```

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
Alternate, full path.
```bash
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash
```

### Custom IP Address

By default, the `ZTI` guesses your IP address using `https://ifconfig.me/ip`.
When installing on the devices not on the public internet it is unlikely that this is what you want.
There are several ways to discover a candidate IP address, here are some.

Wired, ethernet, RJ45, LAN
```bash
ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
```
WiFi, LAN
```bash
ip -4 addr show wlan0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
```
On the public internet.
```bash
curl ifconfig.me/ip
```
Here is an example capturing the wired LAN address:
```bash
export MY_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
```
With an appropriate IP address in hand you can run the `ZTI`.
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IP}
```
Alternate, full path.
```bash
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash -s -- --ip-addr ${MY_IP}
```


## How `ZT` works
The command `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IP} `
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

--ip-addr ${MY_IP}
: Provide an argument to configure FTS with a specific, `MY_IP`, IP address.


Putting it all together, `wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IP}`
downloads the content from the URL shortened as `bit.ly/freetakhub2`,
then immediately executes that content as a bash script with superuser privileges.
Providing an argument to configure FTS with a specific IP address.


## `ZTI` Legacy Argument

If you are still wanting to use the previous "legacy" version,
please use the following command (please note this must be done in Ubuntu 22.04)

```console
wget -qO - bit.ly/freetakhub2 | sudo INSTALL_TYPE=legacy bash
```
or
```console
wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --legacy
```
