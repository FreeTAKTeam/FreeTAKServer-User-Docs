# FreeTAKHub Voice installation

the FTH Voice server is based on Mumble
to install it manually:
* open a console terminal
* Do some cleaning
```
sudo apt-get update
sudo apt-get upgrade
```
* If will be asked to confirm installing any packages. Type Y and press Enter.

* Now Install Mumble Server.
```
sudo apt-get install mumble-server
```

as soon it' started you may want to configure it
```
sudo dpkg-reconfigure mumble-server
```

You can use your arrow keys to select your answer, then press Enter to continue.

![image](https://user-images.githubusercontent.com/60719165/159131852-ebda53e1-1ed8-4f3f-bacd-b60ed7ed2664.png)

you will accept the default value of Yes because we want Mumble-Server to run when the server boots.

![image](https://user-images.githubusercontent.com/60719165/159131856-e7510b41-bfdd-43ba-ad5a-efe89fbd3d4d.png)

Even if this will be a dedicated Mumble-Server, Now select Yes since this will ensure the lowest possible latency.

### Mumble SuperUser Password
SuperUser is the highest-level administrative account for the server. You’ll need to log in to Mumble with this user when you want to manage the server.

![image](https://user-images.githubusercontent.com/60719165/159131862-e9dc9b27-9974-4fd4-8db9-0c97cad064db.png)

Type a password, press Tab to select Ok, and press Enter.

## Init configuration
you will need to edit some configuration file. 
with WinSCP navigate to 
```
/etc/mumble-server.ini
```

In general you want to setp the following:
```
; Port to bind TCP and UDP sockets to you can leave the standard.
port=64738
; Password to join server.
serverpassword=
;Welcome message sent to clients when they connect.
welcometext= 
bandwidth=
users=
registerName=
```
check out the complete file for more info
