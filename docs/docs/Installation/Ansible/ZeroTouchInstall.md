# Zero Touch Installation

To install, enter into the console:

```console
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash
```

The optimal configuration to run the script is:

* Ubuntu 20.04
  * Other operating systems may work, but are untested.
* Intel-based architecture
  * The map in the web interface may not work with non-Intel-based architecture.

This script will install and configure FreeTAKHub components.

1. FreeTAKServer (FTS): The core server that interfaces with TAK-enabled clients
1. FreeTAKServer User Interface (FTS-UI): A web-based user interface.
1. FreeTAKHub Webmap: A mapping component on the web interface.
1. Video Server:  Handles video streaming.
1. FreeTAKHub Server: Handles FTS integrations like SALUTE reports & video checking services (checks if videos are running and notifies FTS).
1. FreeTAKHub Voice Server: Uses [Murmur](https://github.com/mumble-voip/mumble) or Mumble VOIP Server for voice chatting.

# Zero Touch Deployment Diagram

![image](https://user-images.githubusercontent.com/60719165/159137165-59164055-ce6d-4396-9a9b-f7503d20b3f6.png)

# Custom Deployment (Advanced)

This script prompts the user to select specific FreeTAKHub components to install:

```console
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/advanced_install.sh | sudo bash
```

Shortened URL for Custom Deployment (under construction)

```console
wget -qO rb.gy/ocghax | sudo bash
```
