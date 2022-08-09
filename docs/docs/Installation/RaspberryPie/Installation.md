
this procedure Installs FTS + UI + video Server of a Rasberry Pi

need to start with new install of ubuntu 20.04 server for pi 64 from: 
https://cdimage.ubuntu.com/releases/20.04.4/release/ubuntu-20.04.3-preinstalled-server-arm64+raspi.img.xz

download an imager
```
https://www.balena.io/etcher
```
follow the instructions to create a card with the image

 * insert the card into the PI
 * login with ubuntu / ubuntu
 * . If the RPi is connected to your router, when it boots it will display the IP grabbed from DHCP server. Write it down
 * . OS should prompt you to create a new password
 * . If desired, update OS – Run: 
```
sudo apt-get update; sudo reboot -n; sudo apt-get upgrade
```
 * In some cases you need to run: sudo apt full-upgrade or sudo apt-get dist-upgrade
 *   reboot be needed a couple times to get the OS completely updated
```sudo reboot -n might```

 * install wget
```
sudo apt install wget
```
 * 

type or copy this string to start the ZeroTouch installer
```
wget -qO - bit.ly/ftszerotouch | sudo bash
```
in alternative use

```
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | bash
```
> 1.9.9.5 version of Zero Touch DOES NOT install the compiled webmap. You will need to install the [flow version](https://freetakteam.github.io/FreeTAKServer-User-Docs/FreeTAKHub/WebMap/Installation/)

## After installtion
 * ZeroTouch should configure the system and start all the services for you. In case the configuration need to be changed manually 
 *  Edit the file using [VIM](https://freetakteam.github.io/FreeTAKServer-User-Docs/administration/usingConsole/) 
 ```/usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI/config.py``` 
 * Use  sudo vim /usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI/config.py
 * Or browse to that location with WinSCP and double-click on ‘config.py’
 * Change FTS IP (if necessary) = Your EXTERNAL IP (or ZeroTier IP) address for your RPi
 * Leave APPIP = 0.0.0.0 
 *  Change WEBMAPIP (if necessary) = Your IP (or ZeroTier IP) address for your RPi
 *   Change WEBMAPPORT = 1880 for a NodeRedFlow install and 8000 for a compiled webmap
 * Edit this file: /opt/FTSConfig.yaml
 *  Use command: sudo vim /opt/FTSConfig.yaml
*  Or browse to that location with WinSCP and double-click on ‘FTSConfig.yaml’
* Change FTS_DP_ADDRESS, FTS_USER_ADDRESS & FTS_API_ADDRESS = Your IP (or ZeroTier IP) address for your RPi
* Start the FTS service:
```sudo systemctl start fts ```
* Start the FTS-UI service
```sudo systemctl start fts-ui```
