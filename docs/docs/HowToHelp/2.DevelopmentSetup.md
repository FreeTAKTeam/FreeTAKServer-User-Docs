# Setup a development enviroment for FTS
## introduction
this tutorial assumes that you are working under windows (tested under 11)

# Tools Installation
## install Python
Download python-3.11.1-amd64.exe from the [source](https://www.python.org/downloads/release/python-3111/)

## Get the IDE: VisualStudio Code
As an integrated Development Environment (IDE) we use VisualStudio Code.
VIsual Studio Code is integrated with GitHub, in fact you can start editing any file directly in the browser for committing lightweight code changes.

For a more serious collaboration you should install the desktop version:
https://code.visualstudio.com/Download
with the following plugins:

![image](https://user-images.githubusercontent.com/60719165/189349403-3b4d400b-2fe1-4ea1-a0ae-f0b164346bd5.png)

we use the **Setting Sync** plugin to keep the team setting aligned, ask us for the coordinates of the settings.

## Install visual-cpp-build-tools
 Get [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)
![image](https://user-images.githubusercontent.com/60719165/210389806-6f252b06-529b-433c-86e1-6fe8c6e09a2c.png)

ensure that you have "Desktop development with C++" installed
![image](https://user-images.githubusercontent.com/60719165/210411265-2bb7957d-1438-429e-95cb-e80afbd5d1c0.png)


##  Install a source code manager: TortoiseGit
install a source code manager like [TortoiseGit](https://tortoisegit.org/)

Clone both FreeTakServer and DigitalPy repos locally
![image](https://user-images.githubusercontent.com/60719165/210428765-86b5cd37-e23b-43b4-905a-84b300fa7f36.png)

# Configuration
## create a virtual Enviroment
* open a command prompt and navigate to the FreeTakServer repo
* Type:
```
py -m venv venv # setup virtual environment
```

if you now take a look inside the directory of your venv, you’ll see something like this on Windows:
```
.
├── Include
├── Lib
│   └── site-packages
├── pyvenv.cfg
└── Scripts
    ├── activate
    ├── activate.bat
    ├── Activate.ps1
    ├── deactivate.bat
    ├── pip3.10.exe
    ├── pip3.exe
    ├── pip.exe
    ├── python.exe
    └── pythonw.exe
```
Activate the virtual enviroment
```
# In cmd.exe
venv\Scripts\activate.bat
# In PowerShell
venv\Scripts\Activate.ps1
```
# Install FTS locally
show installed packages  
```
pip list
```
output

![image](https://user-images.githubusercontent.com/60719165/210388514-b3cd99c0-476d-48eb-8efd-c6f3efdc7902.png)

* now install dependencies and FreeTAKServer as package
```
pip install -e .
```

change directory to DigitalPy dir
```
cd .../DigitalPy
```
install dependencies and DigitalPy as package
```
pip install -e .
```
# Configure VS Code
open VS Code Explorer to the location of the FreeTAKServer project

![image](https://user-images.githubusercontent.com/60719165/210416689-9ee810ee-4970-40b6-a9fa-8cda8e1f8b8d.png)

* change the VSCODE Python Interpreter (ctrl + shift + p).
* Look for "Python: Select Interpreter.
* Select the one in your venv/scripts/python.exe
* Go to "Run and Debug"
* Select “Create launch.json” file
* copy this configuration  over the created file and configure [YOURPATH] with your actual path 
```
      {
    "version": "0.2.0",
    "configurations": [

        {
            "name": "FTS",
            "type": "python",
            "request": "launch",
            "program": "C:\[YOURPATH]\\src\\FreeTakServer\\FreeTAKServer\\controllers\\services\\FTS.py",
            "console": "integratedTerminal",
            "justMyCode": false,
             "env": {
                    "FTS_CONFIG_PATH": "C:\[YOURPATH]\\src\\FreeTakServer\\FreeTAKServer\\FTSConfig.yaml",
                    "FTS_FIRST_START": "false",
                    "PYTHONTRACEMALLOC": "25"
                 }
    ]
}  
```

![image](https://user-images.githubusercontent.com/60719165/210416985-b588273a-93bc-4b20-abdf-5ebcea2f5c44.png)


### FTS YAML File
In the  folder containing FreeTakServer repo create a file:
 FTSConfig.yaml
 
 

Copy the example FTSConfig.yaml into the file just created
```
System:
  #FTS_DATABASE_TYPE: SQLite
  FTS_CONNECTION_MESSAGE: Welcome to FreeTAKServer FreeTAKServer-2.X alpha. The
    Parrot is not dead. It’s just resting
  #FTS_OPTIMIZE_API: True
  #FTS_MAINLOOP_DELAY: 1
Addresses:
  #FTS_COT_PORT: 8087
  #FTS_SSLCOT_PORT: 8089
  FTS_DP_ADDRESS: 192.168.100.105
  FTS_USER_ADDRESS: 192.168.100.105
  #FTS_API_PORT: 19023
  #FTS_FED_PORT: 9000
  #FTS_API_ADDRESS: 0.0.0.0
  FTS_FIRST_START: false
Filesystem:
  FTS_DB_PATH: [PATH]\\FreeTakServer\\FreeTAKServer.db
  #FTS_COT_TO_DB: True
  FTS_MAINPATH:  [PATH]\\FreeTakServer\\FreeTAKServer
  FTS_CERTS_PATH: [PATH]\\FreeTakServer\\FreeTAKServerCerts
  FTS_EXCHECK_PATH: [PATH]\\FreeTakServer\\ExCheck
  FTS_EXCHECK_TEMPLATE_PATH: [PATH]\\FreeTakServer\\ExCheck\\template
  FTS_EXCHECK_CHECKLIST_PATH: [PATH]\\FreeTakServer\\ExCheck\\checklist
  FTS_DATAPACKAGE_PATH: [PATH]\\FreeTakServer\\FreeTAKServerDataPackageFolder
  FTS_LOGFILE_PATH: [PATH]\\FreeTakServer\\FreeTakServerLogs
  FTS_CORE_COMPONENTS_PATH: \\home\\ariel\\Workspace\\FTAK\\FreeTakServer\\FreeTAKServer\\components\\core
  FTS_EXTERNAL_COMPONENTS_PATH: [PATH]\\FreeTakServer\\components\\extended
  FTS_CLIENT_PACKAGES: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\clientPackages
Certs:
  FTS_SERVER_KEYDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\server.key
  FTS_SERVER_PEMDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\server.pem
  FTS_TESTCLIENT_PEMDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\Client.pem
  FTS_TESTCLIENT_KEYDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\Client.key
  FTS_UNENCRYPTED_KEYDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\server.key.unencrypted
  FTS_SERVER_P12DIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\server.p12
  FTS_CADIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\ca.pem
  FTS_CAKEYDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\ca.key
  FTS_FEDERATION_CERTDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\server.pem
  FTS_FEDERATION_KEYDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\server.key
  FTS_CRLDIR: [PATH]\\FreeTakServer\\FreeTAKServerCerts\\FTS_CRL.json
  FTS_FEDERATION_KEYPASS: demopassfed
  FTS_CLIENT_CERT_PASSWORD: demopasscert
  FTS_WEBSOCKET_KEY: YourWebsocketKey
```


Adjust paths to point to point to dir structure
Create a certs folder at the same level
Adjust FTS_CERTS_PATH to point to the newly created dir
Create new directory for the FreeTakServerLogs
Adjust FTS_LOGFILE_PATH to point to the newly created dir

# you're Done!
Hit F5 to run debug

