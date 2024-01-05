---
status: ood
---

# Raspberry Pi

this procedure Installs FTS + UI + video Server onto a Raspberry Pi

## Hardware requirements
you need a RaspPi with at least 4 GB RAM

## Procedure

### Prepare an SD Card
Start with new installation of ubuntu 22.04 server for RaspPi 64.
FTS 2.1 expects [Ubuntu 22.04 (64 bit)](https://ubuntu.com/download/raspberry-pi/thank-you?version=22.04.3&architecture=server-arm64+raspi).

You will need an imager.

* [Raspberry Pi Imager](https://www.raspberrypi.com/software/) (you may also use [BalenaEtcher Imager](https://www.balena.io/etcher)

Follow the instructions to prepare an SD card with the appropriate image.

![](rpi-imager.png)

The `rpi-imager` provides a means for setting an `ssh` authorized key and default `username` and `password`. 

![](rpi-imager-ssh-settings.png)
![](rpi-imager-general-settings.png)

### Setup Hardware

 * insert the prepared SD card into the Raspberry Pi.
 * connect a keyboard
 * connect a monitor
 * connect to an ethernet network

### Update the OS

The initial setup takes ~5 minutes on a RaspPi 4
Login with `fts` / `ubuntu` (or whichever user you selected)

If the RaspPi is connected to your router,
when it boots it will display the IP grabbed from DHCP server.
Write down the IP address, we will need it later.

```bash
sudo apt update -y 
sudo apt upgrade -y
```

In some cases you need to run: 
```sudo apt full-upgrade``` or ```sudo apt-get dist-upgrade```.

It is generally easier to communicate with your server via `ssh`.
You will need the IP address (you should write the address down for later reference).
```bash
sudo apt install -y net-tools
```
```bash
ip addr
```
Here is representative fragment from an output.
```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether d8:3a:dd:5f:27:24 brd ff:ff:ff:ff:ff:ff
    inet 10.2.118.237/24 metric 100 brd 10.2.118.255 scope global dynamic eth0
       valid_lft 53818sec preferred_lft 53818sec
    inet6 fe80::da3a:ddff:fe5f:2724/64 scope link
       valid_lft forever preferred_lft forever
```
The IP address in this case is `10.2.118.237`.
This is the same address you may have captured earlier during initial boot.

Multiple `reboot` may be required to get the OS fully updated.
```bash
sudo reboot 
```

From here on it should be possible to connect via `ssh`.
Here is an example with the IP address obtained previously and `fts` user.
```bash
ssh fts@10.2.118.237
```

### Update Prerequisites

Verify the following packages are installed.
```bash
sudo apt install -y wget curl
````

Connect 
FTS 2.1 runs on Python 3.11.
```bash
sudo apt install -y python3.11-dev
sudo apt install -y python3-pip
python3 -m pip install psutil
```

### Run the Zero Touch Installer (ZTI)
Run one of the following (equivalent) commands to start the [ZeroTouch](../../Installation/Ansible/ZeroTouchInstall.md) installer.
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash
```
```bash
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | bash
```

## After installation

`ZeroTouch` will configure the system and start all the services for you. 
However, there are many corner cases which `ZeroTouch` may miss.
Many (if not all) of the choices made by `ZeroTouch` are written to stdout.
I recommend that you validate the properties in that output.

### [Verify and/or Edit the `fts-ui` configuration file](../../administration/usingConsole.md)  
```text
/usr/local/lib/python3.11/dist-packages/FreeTAKServer-UI/config.py
```
`WEBMAPIP` is 1880 for a `NodeRedFlow` install and `8000` for a compiled `webmap`.

For specific instructions on validating the configuration,
see [these notes](../Troubleshooting/fts-ui-server.md).

### [Verify and/or Edit the `fts` configuration file](../../administration/usingConsole.md) 
```text
/opt/FTSConfig.yaml
```

For specific instructions on validating the configuration,
see [these notes](../Troubleshooting/fts-server.md).

## Mange the FTS services:

If the `ZTI` had run it will have attempted to start the `fts` services.
As you make changes to their configurations you will need to restart them.
```bash
sudo systemctl stop fts-ui
sudo systemctl stop fts

sudo systemctl start fts
sudo systemctl start fts-ui
```

Your `FTS` should now be running.

See [troubleshooting](../Troubleshooting/troubleshooting_faq.md) for more information.

There are other services which `ZTI` will start.
They are also managed by `systemd`.

```bash
sudo systemctl status nodered.service
sudo systemctl status mediamtx.service
sudo systemctl status webmap.service
sudo systemctl status murmur.service
```
