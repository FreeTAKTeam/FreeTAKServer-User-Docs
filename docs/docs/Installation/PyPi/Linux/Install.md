This guide will walk you through installing FreeTAKServer 1.5 on a Linux host

## Linux Distribution

It is suggested to use Ubuntu 20.04 or Debian 10 or Raspberry PI OS.

### Install Python 3

```bash
sudo apt update && sudo apt install python3 && sudo apt install python3-pip
```

### Install Python Libraries
OPTIONAL this should not be necessary using FTS 1.5
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
sudo pip3 uninnstall FreeTAKServer
sudo pip3 uninstall FreeTAKServer-UI
```

Delete the database 
```bash
sudo  rm /root/FTSDataBase.db
```
and the various logs folders


### Install FreeTAKServer
Install the FTS  and the Web UI (suggested)
```bash
sudo python3 -m pip install FreeTAKServer[ui]
```

in altenative Install the FTS only
```bash
sudo python3 -m pip install FreeTAKServer
```

```bash
pip check FreeTakServer 
```

### Configure FreeTAKServer

Depending on the linux distro your config file for FTS will be in a python version dependant location.

If you are running python 3.7
```
/usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

If you are running python 3.8

```
/usr/local/lib/python3.8/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

You can edit the file via nano with the following command

```
sudo nano /usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

To exit nano `ctrl+x` and then enter `y` to save and hit enter.

#### DBFilePath
OPTIONAL this should not be necessary using FTS 1.5
you need to change the `DBFilePath` value to something valid, if you are running as root, '/root' is a good choice.

Original Value
```python
    # this should be set before startup
    DBFilePath = str(r'/home/root/FTSDataBase.db')
```

As roots Home Folder
```python
    # this should be set before startup
    DBFilePath = str(r'/root/FTSDataBase.db')
```

### Configure Web UI
UI configuration can be found under FreeTAKServer-UI/config.py
```
    SQLALCHEMY_DATABASE_URI = 'sqlite:///' + '/root/FTSDataBase.db'
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
sudo python3 -m FreeTAKServer.controllers.services.FTS -DataPackageIP 0.0.0.0 -AutoStart True
```

If you see FTS start without error you may hit `ctrl+c` twice and move onto running FTS.
