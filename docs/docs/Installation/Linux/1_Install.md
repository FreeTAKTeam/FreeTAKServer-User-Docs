# FreeTAK Server Installation
This guide will walk you through installing FreeTAKServer 2.0

## 0. Document Goals

- Prepare host OS
- Install FreeTAKServer
- Configure and Run FreeTAKServer
- Configure Web UI
- Install [NodeRed](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/NodeRedinstallation.md) for FreeTAKHub 
- Install the [Web Map](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/WebMap/Installation.md)
- Install the [Video Service](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/FreeTAKHub/Video/Installation.md)

---
## Note: Linux Distributions

The main supported OS is Ubuntu 20.04. Due to cross-compatibility, Debian 10 and the latest Raspbian also work.

Centos/RHEL/Fedora installation instructions are provided on a best-effort volunteer basis.

---
## 1. Update OS Packages

**Ubuntu**

```bash
sudo apt update && sudo apt upgrade
```

**RHEL**

```bash
sudo dnf update
```

---
## 2. Pre-requisite Software

**Ubuntu**

Install packages from the distro repo

```bash
sudo apt update && sudo apt install python3 && sudo apt install python3-pip
sudo apt install python3-dev python3-setuptools build-essential python3-gevent python3-lxml libcairo2-dev
```

**RHEL**

Install distro repo packages

```bash
sudo dnf group install "C Development Tools and Libraries" "Development Tools"
sudo dnf install python3 python3-pip cairo cairo-devel python3-cairo python3-cairo-devel python3-gevent python3-lxml python3-virtualenv
```

Create and activate a virtualenv for the next steps

```bash
virtualenv venv
source venv/bin/activate
```


---
## 3. Install Python Libraries

**Ubuntu**

```bash
sudo pip3 install wheel pycairo
```

Note, use of pip with sudo is not recommended and you will be warned about this!


**RHEL**


```bash
pip install wheel pycairo
```


![image](https://user-images.githubusercontent.com/60719165/142766382-8a6e5d05-a198-488d-86f2-67cd49cc1ca6.png)

---
## 4. Remove Old Installation
**YOU MUST DO THIS IF:**

-  Free TAK Server has been installed before
-  An upgrade fails
-  A previous installation was not completed

**Ubuntu**

```bash
sudo pip3 uninstall FreeTAKServer
sudo pip3 uninstall FreeTAKServer-UI
```

**RHEL**

```bash
pip uninstall FreeTAKServer FreeTAKServer-UI
```

Delete the database and log folders

```bash
sudo rm /root/FTSDataBase.db
sudo rm -r /usr/local/lib/<your-python-version>/<dist or site>-packages/FreeTAKServer
```

---
## 5. Install FreeTAKServer
Install the FreeTAKServer  and the associated Web UI

**Ubuntu**

```bash
sudo python3 -m pip install FreeTAKServer[ui]
```

**RHEL**

```bash
pip install FreeTAKServer[ui]
```

The FreeTAKServer can be installed without the UI, however this makes the
server much more difficult to use and is probably not what you want. This can be done using the `FreeTAKServer` pip package.

### Advanced Installations: Install a specific version
To install a special version of a FreeTAKServer pip package by appending `==version-number` to the installation command.

```bash
python3 -m pip install FreeTAKServer[ui]==version-number
```

For example, if you want to install version Alpha of the requests package, you can run the following command:

```bash
python3 -m pip install FreeTAKServer[ui]==0.2.0.13
```

Old installations can be installed in the same way, if desired.

This will download and install version 0.2.0.13 of FreeTAKServer. If no version number is specified, then the latest normal release will be installed.

---
## 6. Check Installation

The pip utility allows the user to check the installation status of a package.

**Ubuntu/RHEL**

```bash
pip check FreeTakServer 
```
![image](https://user-images.githubusercontent.com/60719165/142766403-b877a43b-ec9d-48ce-a13c-b216ddcfa295.png)

---
## 7. Configure and Run FreeTAKServer
this works only for 1.9 or better, for see here for [manual configuration](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/Installation/PyPi/Linux/ManualConfiguration.md) 

Start the FreeTAKServer
**Ubuntu**

```bash
sudo python3 -m FreeTAKServer.controllers.services.FTS 
```

**RHEL**

```bash
python -m FreeTAKServer.controllers.services.FTS 
```

On the first run, a configuration wizard will help set up the config file.

![image](https://user-images.githubusercontent.com/60719165/142766476-f1b5bbb9-aba5-4e05-9b53-a15c075d7e96.png)

**If the wizard does not show up, see [troubleshooting](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/Troubleshooting/troubleshooting/).**

The default configuration option is presented in [brackets].
If the default is acceptable you can simply press enter to use the default.

An example is provided, your exact configuration will differ.

```css
would you like to use a yaml config file, 
 if yes you will be prompted for further configuration options [yes]:
where would you like to save the yaml config [/opt/fts/FTSConfig.yaml]: 
enter ip [127.0.0.1]: 
enter the preferred database type (MySQL is highly experimental if you're not sure leave default) [SQLite]: 
enter the preferred database path [/opt/fts/FTSDataBase.db]: 
enter the preferred main path [/usr/local/lib/python3.11/site-packages/FreeTAKServer]: 
enter the preferred log file path [/opt/fts/Logs]: 

```

**The IP in this configuration wizard is the FTS_MAIN_IP.
This must be your EXTERNAL IP.**

MySQL usage is beyond the scope of this guide.

The database and log filepath can be anywhere that the host user can access.

The main path should be the directory where pip installed FreeTAKServer. This can be found under your python packages directory. In virtualenv installations, it is inside the virtualenv directory.


The wizard creates the YAML configuration file is created under the location you selected (default is /opt/FTSConfig.yaml).

FreeTAKServer will then proceed start all the services.
![image](https://user-images.githubusercontent.com/60719165/142766645-210f09c3-88f5-435a-8a0d-d27bc3d4f1c3.png)

---
## 7. FTSConfig.yaml Additional Configuration

![image](https://user-images.githubusercontent.com/60719165/142766660-daac490a-3c0c-4089-b3b8-40c5e520c1ff.png)

Before modifying the YAML file FreeTAKServer **must be stopped**.

Use the keyboard  chord CTRL + C twice in the console will stop FreeTAKServer.

## 8. Additional FTS configuration
FTS sends a welcome message on client connection which is configurable. See the `FreeTAKServer/core/configuration/MainConfig.py` file to change it.

```
        ConnectionMessage = f'Welcome to FreeTAKServer {version}. The Parrot is not dead. It’s just resting'
```

---
## 9. Configure Web UI


Edit the `config.py` file in the `FreeTAKServer-UI` directory where it was installed by pip.


Edit the IP value to your external IP, for example:

```python
# this IP will be used to connect with the FTS API
IP = '192.168.1.100'
```

Set the web map IP address, for example:

:warning: **Warning: Original intent is unknown, this configuration is a best-guess.**

```python
# the public IP your server is exposing
APPIP = '0.0.0.0'
# webmap IP
WEBMAPIP = "192.168.1.100"

```

In a default installation, the port should be `19023`.
Advanced users may wish to use a different port.


```python
    # Port the  UI uses to communicate with the API
    PORT = '19023'
```
 
The following can be updated to use your own secrets, however the values must be
updated in both the `FreeTAKServer-UI/config.py` and the `FreeTAKServer/core/configuration/MainConfig.py` files.

 If you change those values in the UI you must change also the YAML file configurtation
the API key used by the UI to comunicate with FTS. generate a new system user and then set it

```python
app.config['APIKEY'] = 'Bearer [API_TOKEN]'
app.config['WEBSOCKETKEY'] = '[Your_Web_socket_Key]'
```
 
### 9.1 MySQL Configuration

To use a MySQL database, update the URI to point to your database.

Database setup is beyond the scope of this document.

```python
SQLALCHEMY_DATABASE_URI = 'mysql://' + 'user:pass@localhost/dbname'
```
 
### 9.2 Miscellaneous Parameters
Additional parameters can be found in the `__init__.py` file.

```
FreeTAKServer-UI/app/__init__.py
```

this include the frequence of the update for the dashboard and the file limit for data packages

```python
app.config['USERINTERVAL'] = '180000';
app.config['SERVERHEALTHINTERVAL'] = '180000';
app.config['SYSSTATUSINTERVAL'] = '600000';
app.config['DATAPACKAGESIZELIMIT'] = '15360000';
```

### 10. Start UI
While in terminal, navigate to the `FreeTAKServer-UI` directory wherever it was
installed by the pip utility.
 
 Run the UI using

**Ubuntu** 

 ```bash
 sudo python3 run.py
 ```
 
 **RHEL**
 
 ```bash
 python run.py
 ```
 
 ![image](https://user-images.githubusercontent.com/60719165/142767800-e09ef09c-d6d7-4a11-bcc4-0f4a09597bb1.png)


---
## 11. Next Steps

### Create a service

To run the server without keeping the console open, a service can be created.

*See: [Service](Service.md)*

### Installation on a Separate machine
Typically the web UI  is installed on the same machine as FTS, however you can install it on a separate machine and even use it to manage several instances.

If you're installing FTS-UI on a separate server the following commands may help:

```bash
sudo pip install WTForms==2.3.3
sudo pip install SQLAlchemy==1.3.20
sudo pip install eventlet
```

The config file will also need to be updated.

```python
IP = [FTS external IP]
APPIP = [FTS-UI internal IP]
```
 
## Troubleshooting
### WTForms Error Troubleshooting

In the event of a wtforms error, install it using pip:

```bash
pip3 install WTForms==2.3.3 
```

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

