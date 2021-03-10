# FTS Installation with Android
FTS 1.6 supports Android deployment. The following instructions refers to a pre-beta version (1.6.6), you install it at your own risk. This has been tested with Android 9, 10, 11 and Samsung S7, S8 and S9.

- download the APK installation package from github to  your phone
- start the installation using Android
- **open the configuration of the APP and allow storage rights: in the app icon, click on the info, scroll down to "permission", and allow storage. Failure to do so will stop the APP to work!!!!**
- Start the the FTS app
- set your devices IP in the text box
- Set the slider to "ON"
- In the notifications you will see that FTS is running as a service in background
- Open your network connection and note your IP (e.g. 192.168.1.25)
- On a separate phone, open ATAK and create a new connection
- Set  connection to TCP, to the previosly noted IP and port **15777**

## UI Setup
FTS  Android Edition has a minimal user interface, allowing to start and stop the FTS (including all the services).  For advanced management you will need to install the web UI.
since 1.6 you can now run the UI independently from the backend. THis allow you to install your web UI centrally and to manage several instances of FTS.

- install the UI with this command
```
sudo python3 -m pip install FreeTAKServer-UI=0.1.6.5
```
- to find where your UI is installed you run
```pip show FreeTAKServer-UI```
- in [INSTALLPATH]/config.py  set line 29 IP as device IP. e.g. REMEMBER THAT THIS IP MUST BE VISIBLE TO THE UI MACHINE
```
    # this IP will be used to connect with the FTS API
    IP = '192.168.1.25'
```
- start UI server
```sudo FLASK_APP=/usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI/run.py python3 /usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI/run.py```
- Open a browser to [UIIP]:5000
- login with default creds(admin, password)
- you can now controll your FTS Android Edition from this UI 


# Troubleshooting
if FTS crashes at the start, please check out the following

1. ensure you have the following paths on your phone
```/FreeTAKServer/certs/ClientPackages
/FreeTAKServer/logs
```
2. ensure once again that storage permissions are enabled

# Notes
* Dynamic DP IP changing in UI currently isn't functional
* Federation as the server isn't functional, you can still connect your Android Edition instance as a client to another regular FTS.  

# changes:
- runs now as a service
- UI improved with sliders and spy
- Icon added
- Splashscreen added
