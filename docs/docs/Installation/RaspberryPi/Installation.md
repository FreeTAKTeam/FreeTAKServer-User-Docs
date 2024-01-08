---
status: current
---

# Raspberry Pi

this procedure Installs FTS + UI + video Server onto a Raspberry Pi

## Hardware requirements
you need a RaspPi with at least 4 GB RAM

## Procedure

### Prepare an SD Card
Start with new installation of ubuntu 22.04 server for RaspPi 64.
FTS 2.1 expects [ubuntu 22.04](https://ubuntu.com/download/raspberry-pi/thank-you?version=22.04.3&architecture=server-arm64+raspi).
Previous FTS versions work 
with [Ubuntu 20.04](https://cdimage.ubuntu.com/releases/20.04.4/release/ubuntu-20.04.3-preinstalled-server-arm64+raspi.img.xz).

You will need an imager.

* [BalenaEtcher Imager](https://www.balena.io/etcher)
* [Raspberry Pi Imager](https://www.raspberrypi.com/software/) preferred

follow the instructions to create a sd card with the image.

<img src="belena-etcher-flashing.png" width="200" />
<img src="rpi-imager.png" width="200" />

The `rpi-imager` provides a means for setting an `ssh` authorized key and default `username` and `password`

### Setup Hardware

 * insert the prepared sd card into the Raspberry Pi.
 * connect a keyboard
 * connect a monitor
 * connect to an ethernet network

### Update the OS
 * the initial setup takes ~5 minutes on a RaspPi 4
 * login with `ubuntu` / `ubuntu` (or whichever user you selected)
   * If the RaspPi is connected to your router,
     when it boots it will display the IP grabbed from DHCP server.
     Write down the IP address, we will need it later.
   * (optional) OS may prompt you to create a new password
   * (optional) update OS: 
```bash
sudo apt-get update
sudo apt-get upgrade
```


In some cases you need to run: ```sudo apt full-upgrade``` or ```sudo apt-get dist-upgrade```.

Reboot may be needed a couple of times to get the OS completely updated.
```bash
sudo reboot 
```

### Update Prerequisites

Verify the following packages are installed.
```bash
sudo apt install wget curl
sudo apt install net-tools
```
If you have installed `sshd` it should now be possible to connect remotely via `ssh`.
You will need the IP address.
```bash
ip addr
```

FTS 2.1 runs on Python 3.11.
```bash
sudo apt install python3.11-dev
sudo apt install python3-pip
python3 -m pip install psutil
```

### Run the ZTI
Run one of the following (equivalent) commands to start the [ZeroTouch](../../Installation/Ansible/ZeroTouchInstall.md) installer
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash
```
```bash
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | bash
```

## After installation

`ZeroTouch` should configure the system and start all the services for you. 
However, there are many corner cases which `ZeroTouch` may miss.
Many (if not all) of the choices made by `ZeroTouch` are written but it to stdout.
I recommend that you check that the properties set in the `fts` and `fts-ui` configuration files be verified.

note
: it is unlikely that your default user will have authority to edit these files, i.e. use `sudo` as needed.

[Verify and/or Edit the `fts-ui` configuration file](../../administration/usingConsole.md)  
```
/usr/local/lib/python3.11/dist-packages/FreeTAKServer-UI/config.py
```
Here is a sample fragment of that file.
```python
class Config(object):

    # this IP will be used to connect with the FTS API
    IP = '127.0.0.1'
    
    # the public IP your server is exposing
    APPIP = '0.0.0.0'

    # The IP the Web UI service will use to access the Webmap service
    WEBMAPIP = '127.0.0.1'
    
    # The TCP port the Web UI service will use to access the Webmap service
    WEBMAPPORT = 1880

```
`ZTI` sets the `IP` and `WEBMAPIP` to your externally known IP address.
If you are not on a public network this will need to be adjusted.

`WEBMAPIP` is 1880 for a `NodeRedFlow` install and `8000` for a compiled `webmap`.


[Verify and/or Edit the `fts` configuration file](../../administration/usingConsole.md)  
```
/opt/FTSConfig.yaml
```
Here is a fragment of that configuration file.
```yaml
Addresses:
  FTS_COT_PORT: 8087
  FTS_SSLCOT_PORT: 8089
  FTS_DP_ADDRESS: 127.0.0.1
  FTS_USER_ADDRESS: 127.0.0.1
  FTS_API_PORT: 19023
  FTS_FED_PORT: 9000
  FTS_API_ADDRESS: 127.0.0.1
```
* Change `FTS_DP_ADDRESS`, `FTS_USER_ADDRESS` & `FTS_API_ADDRESS` to your IP (or ZeroTier IP) address for your `RaspPi`.

## Start the FTS services:

If the `ZTI` had run it will have attempted to start the `fts` services.
If you made any changes to their configurations you will need to restart them.
```
sudo systemctl stop fts-ui
sudo systemctl stop fts

sudo systemctl start fts
sudo systemctl start fts-ui
```


