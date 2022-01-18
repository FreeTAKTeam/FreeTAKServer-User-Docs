
this procedure Installs FTS + UI + video Server of a Rasberry Pi

need to start with new install of ubuntu 20.04 server for pi 64 from: 
https://cdimage.ubuntu.com/releases/20.04.3/release/ubuntu-20.04.3-preinstalled-server-arm64+raspi.img.xz

download an imager
```
https://www.balena.io/etcher
```
follow the instructions to create a card with the image

insert the card into the PI
login with ubuntu / ubuntu

install wget
```
sudo apt install wget
```

type or copy this string
```
wget -qO - https://raw.githubusercontent.com/FreeTAKTeam/FreeTAKHub-Installation/main/scripts/easy_install.sh | bash
```
