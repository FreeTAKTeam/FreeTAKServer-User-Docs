## About webmap
The webmap provides insights of user presence and COTS shared with everyone. Also in his NodeRed version can create certain types of CoT.
there are 2 versions of the webmap:
1.  webMap NodeRed Flow version
2.  webMap Compiled version 


# webMap NodeRed Flow version
the webmap Flow works with all systems that supports Nodered. Advanced users should use this version.

## Installation 
get the webmap.json the last release:
```
https://github.com/FreeTAKTeam/FreeTAKHub-Webmap/releases
```
import the flow into node red

![image](https://user-images.githubusercontent.com/60719165/177557386-7b928582-fc87-4141-9cf5-713f5ff11b46.png)


in the FTS UI edit the file config.py /
change the lines:
```
    # webmap IP
    WEBMAPIP = "[YOURIP]"

    # webmap port
    WEBMAPPORT = *1880*
```

manage palette

![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/2802f254-5eb3-4efe-8d93-6cccd82e0b80)

install/update the required nodes

![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/6ff491e5-949d-4194-8ebf-b69d95fbffd4)


# Compiled version
The compiled version of the webmap work only with AMD64 CPU. Can installed with the ZeroTOuch installer or manually following the instructions below.

 ## NOTICE
the webmap is not a background app, so it needs to remain open to receive information and will not persist it.
So to test ensure that you have connected users and do no switch to other tabs.


## Installation 

get the link of the last release:
```
https://github.com/FreeTAKTeam/FreeTAKHub/releases/download/v0.2.5/FTH-webmap-linux-0.2.5.zip
```
login to your server and go to the opt folder

```
cd /opt
```

the console type  


```
wget https://github.com/FreeTAKTeam/FreeTAKHub/releases/download/v0.2.5/FTH-webmap-linux-0.2.5.zip
```
to download the zip file

![image](https://user-images.githubusercontent.com/60719165/142767625-c871e45a-8d0f-49ab-95ff-ddb2f99bfe8d.png)

install Unzip
```
sudo apt install unzip
```

unzip the package
```
unzip FTH-webmap-linux-0.2.5.zip
```

make the file an executable
```
sudo chmod +x FTH-webmap-linux-0.2.5
```
edit the config file webMAP_config.json
set FTH_FTS_URL to the IP and port of your FTS

```
  "FTH_FTS_URL": "[YOUR_FTS_IP]" 
  "FTH_FTS_TCP_Port": [YOUR_FTS_PORT]
```

in the console type:
```
./[package_name] /[PATHTOCONFIGURATIONFILE]/webMAP_config.json
```

e.g. if your configuration file is under opt
```
./FTH-webmap-linux-0.2.5 /opt/webMAP_config.json
```

* navigate to your IP:8000/tak-map 
* e.g. http://10.0.2.15:8000/tak-map

![image](https://user-images.githubusercontent.com/60719165/142767854-276d1413-ece2-4487-8499-c7253fb27e8b.png)

now connect a TAK client to see if that displays
![image](https://user-images.githubusercontent.com/60719165/143260791-d909e0d5-38e4-4d78-98fe-2fb488e333bf.png)

## configure to start as a service
Systemd is the service manager used by Ubuntu, Debian and many other Linux distributions, and allows to launch rtsp-simple-server on boot.

move the executable
```
sudo mv FTH-webmap-linux-0.2.5 /usr/local/bin/
```

and configuration in the system:

```
sudo mv webMAP_config.json /usr/local/etc/
```

Create the service. copy this complete text and paste into the console:
```
sudo tee /etc/systemd/system/webMap.service >/dev/null << EOF
[Unit]
After=network.target
[Service]
ExecStart=/usr/local/bin/FTH-webmap-linux-0.2.5  /usr/local/etc/webMAP_config.json
[Install]
WantedBy=multi-user.target
EOF
```

Enable the service:
```
sudo systemctl enable webMap.service
```

start the service
```
sudo systemctl start webMap.service
```
