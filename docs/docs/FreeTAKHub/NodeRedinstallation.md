## Prerequisites
This guide assumes that you are using Ubuntu 20.04. Before you begin, you should have a non-root user account with sudo privileges set up on your system. 

## Node JS
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

## NodeRed
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
In order to start Node-RED automatically on startup, we’ll need to install a node-red.service file instead of the more traditional init script. 

first create a special user and dedicated group

```
sudo useradd -m nodered -G nodered
```

now creates the service
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
Point a browser back at the server’s port 1880 and verify that Node-RED is back up. If it is, shut it back down until we secure the install in the next step.

```
sudo systemctl stop node-red
```
