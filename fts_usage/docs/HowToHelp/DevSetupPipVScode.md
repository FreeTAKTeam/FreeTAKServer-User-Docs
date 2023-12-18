# Setup a development environment for FTS
## introduction
this tutorial assumes that you are working under windows (tested under 11)

# Tools Installation
## Install Python
Download python-3.11.1-amd64.exe from the [source](https://www.python.org/downloads/release/python-3111/)

## Get the IDE: VisualStudio Code
As an integrated Development Environment (IDE) we use VisualStudio Code.
Visual Studio Code is integrated with GitHub, in fact you can start editing any file directly in the browser for committing lightweight code changes.

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

Clone from the `https://github.com/orgs/FreeTAKTeam/repositories` group
`FreeTakServer` and `DigitalPy` repositories locally.
![image](https://user-images.githubusercontent.com/60719165/210428765-86b5cd37-e23b-43b4-905a-84b300fa7f36.png)
```shell
git clone https://github.com/FreeTAKTeam/FreeTakServer.git fts
git clone https://github.com/FreeTAKTeam/DigitalPy dipy
```

Some other optional repositories:
```shell
git clone https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs fts-docs
git clone https://github.com/FreeTAKTeam/UI.git fts-ui
```

# Configuration
## create a virtual Environment
* open a command prompt and navigate to the FreeTakServer repo
* Type:
```powershell
py -m venv venv
```

Having set up a virtual environment
you now take a look inside the directory of your venv.
You will see something like this (on Windows):
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
Activate the virtual environment
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
* Look for "Python: Select Interpreter".
* Select the one in your `venv/scripts/python.exe`
* Go to "Run and Debug"
* Select “Create launch.json” file
* copy this configuration  over the created file and configure `[YOURPATH]` with your actual path 
```json
{
    "version": "0.2.0",
    "configurations": [
      {
        "name": "FTS",
        "type": "python",
        "request": "launch",
        "program": "C:\\[YOURPATH]\\src\\FreeTakServer\\FreeTAKServer\\controllers\\services\\FTS.py",
        "console": "integratedTerminal",
        "justMyCode": false,
        "env": {
          "FTS_CONFIG_PATH": "C:\\[YOURPATH]\\src\\FreeTakServer\\FreeTAKServer\\FTSConfig.yaml",
          "FTS_FIRST_START": "false",
          "PYTHONTRACEMALLOC": "25"
        }
      }
    ]
}  
```

![image](https://user-images.githubusercontent.com/60719165/210416985-b588273a-93bc-4b20-abdf-5ebcea2f5c44.png)


### FTS YAML File
In the  folder containing FreeTakServer repo create a file:
 FTSConfig.yaml
 
 

Copy the example FTSConfig.yaml into the file just created
```yaml
{!HowToHelp/FTSConfig.yaml!}
```

1. Adjust paths to point to point to dir structure
2. Create a certs folder at the same level
3. Adjust FTS_CERTS_PATH to point to the newly created dir
4. Create new directory for the FreeTakServerLogs
5. Adjust FTS_LOGFILE_PATH to point to the newly created dir

# you're Done!
Hit `[F5]` to run debug

