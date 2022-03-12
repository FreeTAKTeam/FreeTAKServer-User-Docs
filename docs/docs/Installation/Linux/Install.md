# FreeTAK Server Installation
This guide will walk you through installing FreeTAKServer 1.9 on a Linux host.
you need to prepare for the followin steps, not all of them are required:

- [Creates target machines](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/Installation/PyPi/Linux/ConfigureMachine.md) 
- Install FreeTAKServer
- Configure and Run FreeTAKServer
- Configure Web UI
- Install the [web Map](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/WebMap/Installation.md)
- Install the [Video Service](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/Video/Installation.md)
- Install [NodeRed](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/NodeRedinstallation.md) for FreeTAKHub 

## Linux Distribution

A part Ubuntu 20.04, you may use  Debian 10 or Raspberry PI OS.


## Upgrade your distro

```
sudo apt update && sudo apt upgrade
```

tap Y and Enter
this will bring Ubuntu to the last pathch level
type 

```
Python3 
```
in the console

### OPTIONAL Install Python 3
this should not be necessary if you follow the instruction until now, however if the command Python3 fails type:

```bash
sudo apt update && sudo apt install python3 && sudo apt install python3-pip
```

### Install Pip
Pip is the package manager for Python

```
sudo apt update && apt install python3-pip
```

### Install Python Libraries

```bash
sudo apt install python3-dev python3-setuptools build-essential python3-gevent python3-lxml libcairo2-dev
```

```
sudo  pip3 install wheel pycairo
```

![image](https://user-images.githubusercontent.com/60719165/142766382-8a6e5d05-a198-488d-86f2-67cd49cc1ca6.png)

### delete previous installation
required only if:
- you have an existing installation
-  Upgrade fails.

```bash
sudo pip3 uninstall FreeTAKServer
sudo pip3 uninstall FreeTAKServer-UI
```

Delete the database 
```bash
sudo  rm /root/FTSDataBase.db
```

and the various logs folders
```bash
sudo rm -r /usr/local/lib/python3.8/dist-packages/FreeTAKServer
```

### Install FreeTAKServer
Install the FTS  and the Web UI (suggested)
```bash
sudo python3 -m pip install FreeTAKServer[ui]
```

in alternative Install the FTS only
```bash
sudo python3 -m pip install FreeTAKServer
```

check your install
```bash
pip check FreeTakServer 
```
![image](https://user-images.githubusercontent.com/60719165/142766403-b877a43b-ec9d-48ce-a13c-b216ddcfa295.png)

#### Install an old version
you can install a [past version](https://pypi.org/project/FreeTAKServer/#history) using this command
```
sudo python3 -m pip install FreeTAKServer[ui]==[VERSIONNUMBER]
```

for example if you want to install version 1.5
```
sudo python3 -m pip install FreeTAKServer[ui]==1.5.10
```

## Configure and Run FTS (1.9+) 
this works only for 1.9 or better, for see here for [manual configuration](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/Installation/PyPi/Linux/ManualConfiguration.md) 
start FTS
```
sudo python3 -m FreeTAKServer.controllers.services.FTS 
```

the first time a wizard will popup

![image](https://user-images.githubusercontent.com/60719165/142766476-f1b5bbb9-aba5-4e05-9b53-a15c075d7e96.png)

```
would you like to use a yaml config file, 
 if yes you will be prompted for further configuration options [yes]: yes

``` 
 
 press enter
 
``` 
where would you like to save the yaml config [/opt/FTSConfig.yaml]:
```

from now on, hit ENTER if you are happy with the default

the public IP will be automatically discovered (you can double check in your digital Ocena console for safety)

```
enter ip [10.0.2.15]: 
10.0.2.15
```

this is the FTS_MAIN_IP, must be you EXTERNAL IP
continue to follow the instructions:

```
**enter the preferred database path [/opt/FTSDataBase.db]: **
/opt/FTSDataBase.db
```

![image](https://user-images.githubusercontent.com/60719165/142766542-18876805-9454-4725-849b-f794036c2848.png)


next one is important, adjust the path to your Python install

![image](https://user-images.githubusercontent.com/60719165/142766601-30560314-9ac1-4fe2-8e8b-91d0057b1991.png)


```
enter the preferred main_path [/usr/local/lib/python3.8/dist-packages/FreeTAKServer]:
/usr/local/lib/python3.8/dist-packages/FreeTAKServer
```

the log can be located anywhere on your machine
```
enter the preferred log file path [/usr/local/lib/python3.8/dist-packages/FreeTAKServer/Logs]: 
/usr/local/lib/python3.8/dist-packages/FreeTAKServer/Logs
```

at this point a YAML file is created under the location you selected (default is /opt/FTSConfig.yaml). FTS will start all the services.
![image](https://user-images.githubusercontent.com/60719165/142766645-210f09c3-88f5-435a-8a0d-d27bc3d4f1c3.png)

### content of the YAML file

![image](https://user-images.githubusercontent.com/60719165/142766660-daac490a-3c0c-4089-b3b8-40c5e520c1ff.png)

If you want to modify the YAML file you need to stop FTS and modify the YAML and then restart it.
CTRL + C (2 times) in the console will stoop FTS

#### Additional FTS configuration
FTS sends a welcome message every time a client connects. This can be changed in the file MainConfig.py  

```
        ConnectionMessage = f'Welcome to FreeTAKServer {version}. The Parrot is not dead. It’s just resting'
```

### SUCCESS!!!
your FTS is now started
![image](https://user-images.githubusercontent.com/60719165/142766636-16cb4097-73e3-4bce-8442-b6b034687dd0.png)

After that you have completed the setup you may want to create a [Service](Service.md) so that FTS will run even if you close the console.


### Configure Web UI
the Web UI is an optional component, however it's required to properly control FTS.


open a new console Session and type


```
cd /usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI
```
or use WinSCP to navigate

![image](https://user-images.githubusercontent.com/60719165/142766762-580c8faf-c7ee-4596-a966-b59c72696c20.png)

edit the file called 
```
config.py
```
![image](https://user-images.githubusercontent.com/60719165/142766782-e003c5b2-f707-4c9f-93ea-a7bef8d896c6.png)


set the IP value to your external IP
```
   IP = '127.0.0.1'
```
for example only do not use it

![image](https://user-images.githubusercontent.com/60719165/142766838-f5823555-9839-4a5e-81e3-196888215dd3.png)

set the webmap IP
```
WEBMAPIP = YOURIP
```

for example only do not use it

![image](https://user-images.githubusercontent.com/60719165/142767734-4346ff2a-0df8-4fa6-81ea-9a5c5cbc313c.png)


the port the UI uses to communicate with the backend
    PORT = '19023'
 
 If you change those values in the UI you must change also the YAML file configurtation
the API key used by the UI to comunicate with FTS. generate a new system user and then set it

```
app.config['APIKEY'] = 'Bearer [API_TOKEN]' 
```

the webSocket  key used by the UI to comunicate with FTS. must be the same value specified in the FTS config. 
 ```   
 app.config['WEBSOCKETKEY'] = '[Your_Web_socket_Key]'
 ```
 
OPTIONAL 
```
    SQLALCHEMY_DATABASE_URI = 'sqlite:///' + '/root/FTSDataBase.db'
```

To use a MySQL database change the above line as follows
```python
SQLALCHEMY_DATABASE_URI = 'mysql://' + 'user:pass@localhost/dbname'
 ```
 #### Additional configuration
 additional parameters for the UI are in the __init__.py
 ```
FreeTAKServer-UI/app/__init__.py
```

this include the frequence of the update for the dashboard and the file limit for data packages

```
   app.config['USERINTERVAL'] = '180000';
    app.config['SERVERHEALTHINTERVAL'] = '180000';
    app.config['SYSSTATUSINTERVAL'] = '600000';
    app.config['DATAPACKAGESIZELIMIT'] = '15360000';
```

 #### Installation on a Separate machine
Typically the web UI  is installed on the same machine as FTS, however you can install it on a separate machine and even use it to manage several instances.
If you're installing FTS-UI on a separate server the following commands may help:

```  Bash
sudo pip install WTForms==2.3.3
sudo pip install SQLAlchemy==1.3.20
sudo pip install eventlet
```

you will need also to set in the config file

```
IP = [FTS external IP]
APPIP = [FTS-UI internal IP]
```
 
 
 ### start the UI
 in the console type navigate to the installation path 
 
 ```
 cd /usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI
 ```
 
 type 
 
 ```
 sudo python3 run.py
 ```
 
 ![image](https://user-images.githubusercontent.com/60719165/142767800-e09ef09c-d6d7-4a11-bcc4-0f4a09597bb1.png)

#### wtforms Form error
NOTE: If you have an error with 'wtforms'

type in the console
``` 
pip3 install WTForms==2.3.3 
```
and press enter

### Test FTS
Let's make sure your FTS server can start and run without errors.

```bash
sudo python3 -m FreeTAKServer.controllers.services.FTS
```

If you see FTS start without error you may hit `ctrl+c` twice and move onto running FTS.


your FTS is now configured

![image](https://user-images.githubusercontent.com/60719165/142767335-c8283798-877e-4fab-b264-7c70f314b3d0.png)

If you have setup the UI, from the Admin console send a message hello world to the client

![image](https://user-images.githubusercontent.com/60719165/142767408-8e754ffa-7102-42ac-8254-a5ba35ff6526.png)

