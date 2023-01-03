# Setup a development enviroment for FTS
## introduction
this tutorial assumes that you are working under windows

## install Python
Download python-3.11.1-amd64.exe from the [source](https://www.python.org/downloads/release/python-3111/)

#### Get the IDE
As an integrated Development Environment (IDE) we use VisualStudio Code.
VIsual Studio Code is integrated with GitHub, in fact you can start editing any file directly in the browser for committing lightweight code changes.

For a more serious collaboration you should install the desktop version:
https://code.visualstudio.com/Download
with the following plugins:

![image](https://user-images.githubusercontent.com/60719165/189349403-3b4d400b-2fe1-4ea1-a0ae-f0b164346bd5.png)

we use the **Setting Sync** plugin to keep the team setting aligned, ask us for the coordinates of the settings.


install a source code manager like [TortoiseGit](https://tortoisegit.org/)

Clone both FreeTakServer and DigitalPy repos locally

From FreeTakServer repo:
```
py -m venv venv # setup virtual environment
```

Activate the virtual enviroment
```
# In cmd.exe
venv\Scripts\activate.bat
# In PowerShell
venv\Scripts\Activate.ps1
```
show tools (should be none)
```
pip list
```

 #install dependencies and FreeTAKServer as package
```
pip install —-upgrade pip
pip install -e .
```

change directory to DigitalPy dir
```
cd .../DigitalPy
pip install -e .
```

obtain launch configuration json




open VS Code to FreeTAKServer project
Go to Run in Debug
Select “Create launch.json” file
copy launch configuration json file over the created file
If needed, update paths
Be sure to uncomment FTS_CONFIG_PATH line

In VS Code: 
Set Python Interpreter to the version in the venv

At folder containing DigitalPy and FreeTakServer repo:
touch FTSConfig.yaml

Copy in example FTSConfig.yaml into the file just created
Adjust paths to point to point to dir structure
Create a certs folder at the same level
Adjust FTS_CERTS_PATH to point to the newly created dir
Create new directory for the FreeTakServerLogs
Adjust FTS_LOGFILE_PATH to point to the newly created dir

python FreeTAKServer/controllers/services/FTS.py

set first_start in MainConfig.py to False
