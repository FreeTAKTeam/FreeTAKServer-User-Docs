---
status: current
---

# FreeTAK Server Installation
This guide will walk you through installing FreeTAKServer 2.1 on an Ubuntu virtual machine.
These instructions are on preparing an Ubuntu VM suitable for using the FTS Zero Touch Installer.

Obviously, the ZTI can be installed in a clean native Ubuntu environment.
However, cleanly setting up such an environment can consume time.
So, while running FTS on dedicated hardware may be a more performant choice 
in a production environment it is more convenient with a virtual machine.

## Setting up the Virtual Machine

Thankfully, Canonical has provided tooling to make setting up an Ubuntu VM easy.

[Multipass Tutorials](https://multipass.run/docs/tutorials)

* [Multipass Windows](https://multipass.run/docs/windows-tutorial)
* [Multipass Linux](https://multipass.run/docs/get-started-with-multipass-linux)
* [Multipass MacOS](https://multipass.run/docs/mac-tutorial)

Any of these are suitable for testing.

We will want to specify a specific Ubuntu version.
```shell
multipass find
```
Of the choices available we want `v22.04`.
```shell
multipass launch 22.04 --name fts-test --memory 4G --disk 10G --cpus 2
```
We can verify the image.
```shell
multipass exec fts-test -- lsb_release -a
```

#### Custom IP Address
By default, the `ZTI` guesses your IP address by using `https://ifconfig.me/ip`.
If this is not the appropriate IP address you will need to supply it to ZTI.
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

## Run the Zero Touch Installer (ZTI)

With an appropriate IP address in hand you can run the `ZTI`.
```bash
wget -qO - bit.ly/freetakhub2 | sudo bash -s -- --ip-addr ${MY_IP}
```
Alternate, full path.
```bash
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | sudo bash -s -- --ip-addr ${MY_IP}
```
The [complete ZTI instructions are here](../../mechanism/Ansible/ZeroTouchInstall.md).

## Operation

`ZeroTouch` will have configured the system and started the services for you. 
However, there are many corner cases which `ZeroTouch` may miss.
Many (if not all) of the choices made by `ZeroTouch` are written to stdout.
I recommend that you validate the properties in that output.
I recommend that you stop the fts services prior to reconfiguration.

* [Service Management](../../../administration/Operation/fts-config.md)
* [Configuration](../../../administration/Operation/fts-config.md)

