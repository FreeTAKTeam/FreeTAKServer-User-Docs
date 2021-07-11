This guide will walk you through installing FreeTAKServer 1.9 on a Linux host

## Linux Distribution

It is suggested to use Ubuntu 20.04 or Debian 10 or Raspberry PI OS.

### Install Python 3

```bash
sudo apt update && sudo apt install python3 && sudo apt install python3-pip
```

### Install Python Libraries
OPTIONAL this should not be necessary using FTS 1.9
```bash
sudo apt install python3-dev python3-setuptools build-essential python3-gevent python3-lxml libcairo2-dev
```

### Install 'wheel' and 'pycairo'
OPTIONAL this should not be necessary using FTS 1.5
```bash
sudo pip3 install wheel pycairo
```
### delete previous installation
required. Upgrade will not work.
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

```bash
pip check FreeTakServer 
```

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
```
would you like to use a yaml config file, 
 if yes you will be prompted for further configuration options [yes]: yes
 ```
 type yes
``` 
where would you like to save the yaml config [/opt/FTSConfig.yaml]:
```
from now on, hit ENTER if you are happy with the default
```
enter ip [10.0.2.15]: 
10.0.2.15
```
this is the FTS_MAIN_IP, must be you EXTERNAL IP
continue to follow the instructions:
```
enter the preferred database path [/opt/FTSDataBase.db]: 
/opt/FTSDataBase.db
enter the preferred main_path [/usr/local/lib/python3.8/dist-packages/FreeTAKServer]: 
/usr/local/lib/python3.8/dist-packages/FreeTAKServer
enter the preferred log file path [/usr/local/lib/python3.8/dist-packages/FreeTAKServer/Logs]: 
/usr/local/lib/python3.8/dist-packages/FreeTAKServer/Logs
```
at this point a YAML file is created under the location you selected (default is /opt/FTSConfig.yaml). FTS will start all the services.

### Configure FreeTAKServer > 1.9
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
Its configuration can be found under /[INSTALLATIONPATH]/FreeTAKServer-UI/config.py
```
    SQLALCHEMY_DATABASE_URI = 'sqlite:///' + '/root/FTSDataBase.db'
```
To use a MySQL database change the above line as follows
```python
SQLALCHEMY_DATABASE_URI = 'mysql://' + 'user:pass@localhost/dbname'
```

set the IP to your external IP
```
   IP = '127.0.0.1'
```
the port the UI uses to communicate with the backend
    PORT = '19023'
 
the API key used by the UI to comunicate with FTS. generate a new system user and then set it
```app.config['APIKEY'] = 'Bearer [API_TOKEN]' ```
the webSocket  key used by the UI to comunicate with FTS. must be the same value specified in the FTS config. 
 ```   app.config['WEBSOCKETKEY'] = '[Your_Web_socket_Key]' ```

### Test FTS
Let's make sure your FTS server can start and run without errors.

```bash
sudo python3 -m FreeTAKServer.controllers.services.FTS
```

If you see FTS start without error you may hit `ctrl+c` twice and move onto running FTS.
