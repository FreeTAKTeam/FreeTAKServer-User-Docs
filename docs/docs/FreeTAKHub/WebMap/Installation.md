
the webmap is not a background app, so it needs to remain open to receive information and will not persist it.

so to test ensure that you have connected users and do no switch to other tabs

## Installation 

get the link of the last release:
```
https://github.com/FreeTAKTeam/FreeTAKHub/releases/download/v0.2.5/FTH-webmap-linux-0.2.5.zip
```
login to your server and in the console type  

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

