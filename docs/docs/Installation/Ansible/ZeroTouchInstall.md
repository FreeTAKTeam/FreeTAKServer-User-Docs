# Zero TOuch Installation

To install, enter into the console:

```console
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash
```

This approach assumes that:

* You have a clean, freshly installed Ubuntu 20.04. Currently FreeTAKServer and FreeTAKHub components have been successfully tested on Ubuntu 20.04. 
Other Linux distributions or OS may work, but they have not been tested.
 
The script will install and configure all FreeTAKHub components.

* FTS: hosts the core of FTS
* FTS Web UI: uses the API service 1935 to interacts with FTS
* FTH webMap :  this connects to FTS using the TCP COT service and port 8087
* Video Service: streams video.
* FTH server: runs other integrations such as the Video Service Checker and SALUTE report. The video Service checker has a strategy to verify if streams are running there and notifies FTS.
* FTH Voice: install a murmur server based on [Mumble](https://github.com/mumble-voip/mumble) for ow-latency, high quality voice chat software.

This repository is a set of Ansible/Terraform scripts that allow you to:

- Create the target nodes.
- Install FTS and all the additional modules.
- Configure FTS.

![image](https://user-images.githubusercontent.com/60719165/159137165-59164055-ce6d-4396-9a9b-f7503d20b3f6.png)

# Zero Touch Deployment Advanced  (Options)

This installation will give you the ability to select which components you need

```console
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/advanced_install.sh | sudo bash
```

Shorter URL (under construction)

```console
wget -qO rb.gy/ocghax | sudo bash
```
