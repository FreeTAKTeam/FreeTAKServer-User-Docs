This guide will walk you through installing FreeTAKServer on a linux host

## Linux Distribution

It is suggested to use Ubuntu 20.04 or Debian 10 or Raspberry PI OS.

### Install Python 3

```bash
sudo apt update && sudo apt install python3 && sudo apt install python3-pip
```

### Install Python Libraries
```bash
sudo apt install python3-dev python3-setuptools build-essential python3-gevent python3-lxml libcairo2-dev
```

### Install FreeTAKServer

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
No you need to change the `DBFilePath` value to something valid, if you are running as root, '/root' is a good choice.

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

### Test FTS
Let's make sure your FTS server can start and run without errors.

```bash
sudo python3 -m FreeTAKServer.controllers.services.FTS -DataPackageIP 0.0.0.0 -AutoStart True
```

If you see FTS start without error you may hit `ctrl+c` twice and move onto running FTS.
