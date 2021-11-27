# Install NodeRed for FreeTAKHub
there are several ways to install NodeRed.
- Install Using Script (simple)
- Install using APT (advanced Users)

# Install Using Script (simple)

the following script will do Installing and Upgrading Node-RED to install Node.js, npm and Node-RED onto a Ubuntu Raspberry Pi. The script can also be used to upgrade an existing install when a new release is available.

Running the following command will download and run the script. If you want to review the contents of the script first, you can view it on Github.
```
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

enable service so that statrs automagically
```
sudo systemctl enable nodered.service
```
Run service
```
node-red-start
```
navigate to your NodeRed
```
http://<IP>:1880
```


# Install using APT (advanced Users)
to install NodeRed with APT you will need to:
- Satisfy the requirements
- create a Non root user
- Install Node JS

## Prerequisites
This guide assumes that you are using Ubuntu 20.04 on cloud installation (we use digital Ocean). 


##  create a Non root user
first create a special user and dedicated group

```
sudo useradd -m nodered -G nodered
```

## Install Node JS
 you can use the apt package manager. Refresh your local package index first by typing:

```
sudo apt update
```

Then install Node.js:
```
sudo apt install nodejs
 ```
 
Check that the install was successful by querying node for its version number:
```
node -v
 ```
Output something like this
```
v10.19.0
```

If the package in the repositories suits your needs, this is all you need to do to get set up with Node.js. In most cases, you’ll also want to also install npm, the Node.js package manager. You can do this by installing the npm package with apt:

```
sudo apt install npm
```
This will allow you to install modules and packages to use with Node.js.

## Install NodeRed
Use npm to install node-red and a helper utility called node-red-admin.
```
sudo npm install -g --unsafe-perm node-red node-red-admin
```

npm normally installs its packages into your current directory. Here, we use the -g flag to install packages ‘globally’ so they’re placed in standard system locations such as /usr/local/bin. The --unsafe-perm flag helps us avoid some errors that can pop up when npm tries to compile native modules (modules written in a compiled language such as C or C++ vs. JavaScript).

After a bit of downloading and file shuffling, you’ll be returned to the normal command line prompt. Let’s test our install.

First, we’ll need to open up a port on our firewall. Node-RED defaults to using port 1880, so let’s allow that.
```
sudo ufw allow 1880
``` 
And now launch Node-RED itself. No sudo is necessary, as port 1880 is high enough to not require root privileges.
```
node-red
```
## Create the Service
In order to start Node-RED automatically on startup, we’ll need to install a node-red.service file 

let's creates the service using the Tee command
```
sudo tee /etc/systemd/system/node-red.service >/dev/null << EOF
Description=Node-RED
After=syslog.target network.target

[Service]
ExecStart=/usr/local/bin/node-red-pi --max-old-space-size=128 -v
Restart=on-failure
KillSignal=SIGINT

# log output to syslog as 'node-red'
SyslogIdentifier=node-red
StandardOutput=syslog

# non-root user to run as
WorkingDirectory=/home/nodered/
User=nodered
Group=nodered

[Install]
WantedBy=multi-user.target
EOF
 ```
 
Now that our service file is installed , we need to enable it. This will enable it to execute on startup.
```
sudo systemctl enable node-red
```

Let’s manually start the service now to test that it’s still working.
```
sudo systemctl start node-red
 ```
 to shut it back down you can use

```
sudo systemctl stop node-red
```
## test your installation 
Point a browser back at the server’s port 1880 and verify that Node-RED is back up. e.g. if your server is installed under the IP 143.198.39.135
``` browser
http://143.198.39.135:1880/
```
you will see the welcome screen of NodeRed with the tutorial
Now, to install the flows, click on the hanburger menu and then import

![image](https://user-images.githubusercontent.com/60719165/143110628-d5e1d2b9-15e8-4b34-b977-abdc99c205f9.png)

download  one of the FreeTAKHub integrations (json files)
import into your Nodered
resolve any conflict by importing additional nodes in you palette

![image](https://user-images.githubusercontent.com/60719165/143121789-3e751ff1-9d07-4089-9668-644962a19986.png)

Success!!!!

![image](https://user-images.githubusercontent.com/60719165/143122002-35f25669-17c3-4dfa-9655-14b52612bd04.png)
