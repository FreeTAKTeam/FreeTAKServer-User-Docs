This guide will walk you through installing FreeTAKServer 1.9 on a Linux host
you need to prepare for the followin steps
- Creates target machines
- 


## Creates target machines
in this example we will use Digital ocean.
1.,. create a DO accoutan
![image](https://user-images.githubusercontent.com/60719165/142765115-3e2a579e-a3fe-4049-beb9-c070f7966f9c.png)

2. create a 2 new droplets
![image](https://user-images.githubusercontent.com/60719165/142765256-c03f7653-fc80-40ab-845f-304399154313.png)

4. Select Ubunbt 20.04 LTS
5. plan basic
6. reccomended the 15 $ Mo plan (it would work with the 5 $ plan but very slow)
7. select the region that is the closesest to you
![image](https://user-images.githubusercontent.com/60719165/142765192-7504fcd9-790b-4c30-b7a8-c30f84488b3d.png)

7. generate a new SSH key and dowload it. It will download 2 files 1 with PEM extension and the second without extension
8.
9.  Select project (FTYS)
10.  press create droplet

## Setup you access to the VM 
- download winSCP and Putty
- open Puttygen 
SSH (Mac/Linux)
Copy .PEM file to the machine from which you are going to connect.
Make sure permissions on .PEM file are appropriate (chmod 600 file.pem)
Connect with ssh command: ssh vcloud@ipaddress –i privkey.pem
Putty (Windows)
Download Putty and puttygen from - here
Use puttygen to convert  file without extesion to .PPK file.
Start puttygen and select “Load”
Select your without extesion  file.
Putty will convert format to .PPK format. enter image description here
Select “Save Private Key” A passphrase is not required but can be used if additional security is required.
Open WinSCP and create a new site
![image](https://user-images.githubusercontent.com/60719165/142771002-3a713b87-768c-48e8-a448-323e28e345a6.png)

![image](https://user-images.githubusercontent.com/60719165/142771008-d272d5df-3e78-4f0c-8be8-a43028414c77.png)

Connect with Putty.

Launch Putty and enter the host IP address. If connecting to the 10.X private address you must first establish an SSL VPN connection.
Navigate to Connection/SSH/Auth
Click “Browse” and select the .PPK file you exported from puttygen. enter image description here
 

## Linux Distribution

It is suggested to use Ubuntu 20.04 or Debian 10 or Raspberry PI OS.

### OPTIONAL Install Python 3

```bash
sudo apt update && sudo apt install python3 && sudo apt install python3-pip
```

### Install Pip
```
sudo apt install python3-pip
```

### Install Python Libraries
OPTIONAL this should not be necessary using FTS 1.9
```bash
sudo apt install python3-dev python3-setuptools build-essential python3-gevent python3-lxml libcairo2-dev
```

### Install 'wheel' and 'pycairo'
OPTIONAL this should not be necessary using FTS 1.5
```bash
sudo apt install python3-dev python3-setuptools build-essential python3-gevent python3-lxml libcairo2-dev
sudo pip3 -m install wheel pycairo
```

![image](https://user-images.githubusercontent.com/60719165/142766382-8a6e5d05-a198-488d-86f2-67cd49cc1ca6.png)

### delete previous installation
required if you have a . Upgrade will not work.
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
you can install a past version using this command
```
sudo python3 -m pip install FreeTAKServer[ui]==[VERSIONNUMBER]
```

## Configure and Run FTS 1.9 +

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

````
enter ip [10.0.2.15]: 
10.0.2.15
````

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

enter the preferred log file path [/usr/local/lib/python3.8/dist-packages/FreeTAKServer/Logs]: 
/usr/local/lib/python3.8/dist-packages/FreeTAKServer/Logs
```

at this point a YAML file is created under the location you selected (default is /opt/FTSConfig.yaml). FTS will start all the services.
![image](https://user-images.githubusercontent.com/60719165/142766645-210f09c3-88f5-435a-8a0d-d27bc3d4f1c3.png)

your FTS is now started
![image](https://user-images.githubusercontent.com/60719165/142766636-16cb4097-73e3-4bce-8442-b6b034687dd0.png)

content of the YAML file
![image](https://user-images.githubusercontent.com/60719165/142766660-daac490a-3c0c-4089-b3b8-40c5e520c1ff.png)

If you want to modify the YAML file you need to stop FTS and modify the YAML and then restart it.
CTRL + C (2 times) in the console will stoop FTS. 

### Configure FreeTAKServer < 1.9
![image](https://user-images.githubusercontent.com/60719165/124500136-9aafa500-dd95-11eb-8aa8-67ffda7076f0.png)

Depending on the linux distro your config file for FTS will be in a python version dependant location.
you can use pip to discover the location. Type:
```
 python3 -m pip show FreeTAKServer
```

If you are running python 3.7 you would get
```
/usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

similarly, If you are running python 3.8

```
/usr/local/lib/python3.8/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

You can edit the file via nano with the following command

```
sudo nano /usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

To exit nano `ctrl+x` and then enter `y` to save and hit enter.

#### DBFilePath
OPTIONAL this should not be necessary since FTS 1.5
you need to change the `DBFilePath` value to something valid, if you are running as root, '/root' is a good choice.

Original Value
```python
    # this should be set before startup
    DBFilePath = str(r'/opt/FTSDataBase.db')
```

As roots Home Folder

```python
    # this should be set before startup
    DBFilePath = str(r'/root/FTSDataBase.db')
```
###  MySQL database
FTS supports an abstraction layer, so it's easy to use a different database like MySQL. MYSQL is still experimental support, so use at your own risk.
To switch to a MySQL database
```python
    # this should be set before startup
    DBFilePath = str('user:pass@localhost/dbname')
```

And then under
```
sudo nano /usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/DatabaseConfiguration.py
```

Change
```python
DataBaseType = str('sqlite:///')
```
To
```python
DataBaseType = str('mysql://')
```

### Configure Web UI
the Web UI is an optional component, however it's required to properly control FTS.
open a new Session and type
![image](https://user-images.githubusercontent.com/60719165/142766762-580c8faf-c7ee-4596-a966-b59c72696c20.png)


```
cd /usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI
```


![image](https://user-images.githubusercontent.com/60719165/142766782-e003c5b2-f707-4c9f-93ea-a7bef8d896c6.png)


```

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
```app.config['APIKEY'] = 'Bearer [API_TOKEN]' ```
the webSocket  key used by the UI to comunicate with FTS. must be the same value specified in the FTS config. 
 ```   app.config['WEBSOCKETKEY'] = '[Your_Web_socket_Key]' ```
 
 
OPTIONAL" Its configuration can be found under /[INSTALLATIONPATH]/FreeTAKServer-UI/config.py
```
    SQLALCHEMY_DATABASE_URI = 'sqlite:///' + '/root/FTSDataBase.db'
```
To use a MySQL database change the above line as follows
```python
SQLALCHEMY_DATABASE_URI = 'mysql://' + 'user:pass@localhost/dbname'
 
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


### Test FTS
Let's make sure your FTS server can start and run without errors.

```bash
sudo python3 -m FreeTAKServer.controllers.services.FTS
```

If you see FTS start without error you may hit `ctrl+c` twice and move onto running FTS.


your FTS is now configured
![image](https://user-images.githubusercontent.com/60719165/142767335-c8283798-877e-4fab-b264-7c70f314b3d0.png)

from the Admin console send a message hello world to the client
![image](https://user-images.githubusercontent.com/60719165/142767408-8e754ffa-7102-42ac-8254-a5ba35ff6526.png)

