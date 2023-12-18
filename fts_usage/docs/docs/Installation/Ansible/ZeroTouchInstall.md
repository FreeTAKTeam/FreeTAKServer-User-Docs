# Zero Touch Installation
the ZeroTouch (ZT or ZTI) installation is the simplest way to install FTS. 
Has been tested on the [cloud](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/Cloud/0_ConfigureMachine/) and on the [RasberryPi](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/RaspberryPie/Installation/) however only on Digital Ocean cloud you will have the perfect experience, where all is installed and configured. 

## Instructions
To install, enter into the console on a Ubuntu 22.04 server:
```console
wget -qO - bit.ly/freetakhub2 | sudo bash
```
in alternative use the long form
```console
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash
```
If you are still wanting to use the previous "legacy" version, please use the following command (please note this must be done in Ubuntu 20.04)

```console
wget -qO - bit.ly/freetakhub2 | sudo INSTALL_TYPE=legacy bash
```

NOTE:
* Intel-based architecture
  * The map in the web interface may not work with non-Intel-based architecture.

### how ZT works
The command wget -qO - bit.ly/freetakhub2 | sudo bash is a combination of several commands and options used together to perform a specific task. Here's a breakdown of what each part of the command does:

wget: This is the command for a popular network downloader utility.
-q: This option tells wget to operate in quiet mode, which suppresses the usual output.
O -: as the capital letter 'o'. The -O - option tells wget to redirect the downloaded content to standard output (stdout) instead of saving it to a file. The - character is used here to denote stdout.
bit.ly/freetakhub2: This is a shortened URL using the bit.ly service. It redirects to a longer URL from which wget will download content.
|: This is a pipe. It takes the output of the command on its left (wget in this case) and uses it as the input for the command on its right.
sudo bash:
sudo: This command is used to execute the following command (bash) with superuser (root) privileges. It's required for commands that need higher permissions to run, typically for installing software or modifying system files.
bash: This is the command to invoke the Bash shell. When used without a filename, bash will read and execute commands from its standard input (which, in this case, is the output of wget).
Putting it all together, wget -qO - bit.ly/freetakhub2 | sudo bash downloads the content from the URL shortened as bit.ly/freetakhub2, then immediately executes that content as a bash script with superuser privileges.


# Zero Touch Deployment Diagram
This script will install and configure FreeTAKHub components.

1. FreeTAKServer (FTS): The core server that interfaces with TAK-enabled clients
1. FreeTAKServer User Interface (FTS-UI): A web-based user interface.
1. Video Server:  based on RTSP SImple Server. Handles video streaming.
3.  Server:  Handle integration services (see below)
4. FreeTAKHub Integration Server: Based on Node Red. Handles FTS integrations like SALUTE reports & video checking services (checks if videos are running and notifies FTS).
5. FreeTAKHub Voice Server: Uses [Murmur](https://github.com/mumble-voip/mumble) or Mumble VOIP Server for voice chatting.
6. FreeTAKHub Webmap: A mapping component on the web interface.



![FreeTAK 1 9 9 ZTI deployment](https://user-images.githubusercontent.com/60719165/207360218-a7b7a619-4cb0-4234-b7bb-9f74910019f6.png)


# Custom Deployment (Advanced)

This script prompts the user to select specific FreeTAKHub components to install:

```console
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/advanced_install.sh | sudo bash
```

Shortened URL for Custom Deployment (under construction)

```console
wget -qO rb.gy/ocghax | sudo bash
```
# Verify your installation
at the end of the ZT you will see a report that will provide credentials and a play recap
![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/47afb1a2-76db-44d0-becb-b66708f80289)
you may now proceed to  [Installation Check](../../../Installation/Troubleshooting/InstallationCheck.md)
## Services
the current name of the services installed by the Zero Touch :

* fts.service
* fts-ui.service
* mumble-server.service
* nodered.service
* rtsp-simple-server.service

use 
```
 systemctl list-units --type=service
```
to see if they are installed and active

to get the exact location/status use
```
systemctl status [SERVICENAME].service
```


this command will output the status of all the services
```
sudo systemctl status fts.service fts-ui.service mumble-server.service nodered.service rtsp-simple-server.service
```

 [how to start / stop / enable  a service?](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/Linux/Service/)


