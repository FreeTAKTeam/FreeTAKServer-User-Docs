# FTS Installation with Android
FTS 1.6 supports Android deployment. The following instructions refers to a pre-beta version, you install it at your own risk

- download the APK [installation package](https://ssna.box.com/s/6375rsnp2eftxnulonz7h0byduqjyd7l) to  your phone
- start the installation using Android
- **open the configuration of the APP and allow storage rights: in the app icon, click on the info, scroll down to "permission", and allow storage. Failure to do so will stop the APP to work!!!!**
- Start the the FTS app
- set your devices IP in the text box
- Set the slider to "ON"
- In the notifications you will see that FTS is running as a service in background
- Open your network connection and note your IP (e.g. 0.0.0.0)
- On a separate phone, open ATAK and create a new connection
- Set  connection to TCP, to the previosly noted IP and port **15777**

UI setup:
- install UI
- in config.py of UI set IP as device IP
- start UI server
- login with default creds(admin, password)

this has been tested with Android 9, 10, 11

changes:
- runs now as a service
- UI improved with sliders and spy
- Icon added

Troubleshooting:
1. ensure you have the following paths /FreeTAKServer/certs/ClientPackages, /FreeTAKServer/logs
2. ensure once again that storage permissions are enables
