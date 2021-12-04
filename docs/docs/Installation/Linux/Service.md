Running FreeTAKServer as a service on your linux server can be achieved multiple ways.

## Cron
Cron or Crontab is a basic scheduler that ships with most linux distributions.

We can use this to get a very basic service running with minimal effort.

### Edit Crontab
```bash
sudo crontab -e
```

Add this line to the bottom of the file

```
@reboot nohup sudo python3 -m FreeTAKServer.controllers.services.FTS &
```

You will need to add any start parameters to the crontab file such as `-DataPackageIP`.

## Systemd

### Introduction
Systemd is nearly unavoidable. It has permiated so many aspects of the Linux ecosystem that it's necessary for any Linux admin to know at least the basics of how it works. 
One of the major selling points of systemd is the ease of writing service files. 
They aren't scripts. Instead, they're basic configuration files. While they can grow to be complex, they are usually very simple.

### Create The File
Systemd services exist at /etc/systemd/system. If you look on your system, they're all there. 
Any .service file that you create in that directory can be run as a service, if you construct it properly. 
Create a file that you would like with the .service extension. 
In our case, create a file as /etc/systemd/system/FreeTAKServer.service with the following content:
(modify the parameters as needed)

```
[Unit]
Description=FreeTAK Server service
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1
ExecStart=/usr/bin/python3 -m FreeTAKServer.controllers.services.FTS

[Install]
WantedBy=multi-user.target

```

And reload systemd so it will load new unit file:
```
systemd daemon-reload
```

### Start the FreeTAKServer.service
```
systemctl start FreeTAKServer.service
```

### Get the Status of the FreeTAKServer.service
```
systemctl status FreeTAKServer.service
```

### Stop the FreeTAKServer.service
```
systemctl stop FreeTAKServer.service
```

### Start the FreeTAKServer.service with the system
```
systemctl enable FreeTAKServer.service
```
