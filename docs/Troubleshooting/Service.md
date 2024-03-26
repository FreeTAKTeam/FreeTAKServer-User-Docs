---
status: ood
---

Running FreeTAKServer as a service on your Linux server can be achieved in multiple ways.

## Cron
Cron or Crontab is a basic scheduler that ships with most linux distributions.

We can use this to get a very basic service running with minimal effort.

### Edit Crontab
```bash
sudo crontab -e
```

Add this line to the bottom of the file

```text
@reboot nohup sudo python3 -m FreeTAKServer.controllers.services.FTS &
```

You will need to add any start parameters to the crontab file such as `-DataPackageIP`.

## Systemd

### Introduction
Systemd is nearly unavoidable.
It has permeated so many aspects of the Linux ecosystem
that it is necessary for any Linux admin to know at least the basics of how it works.
One of the major selling points of systemd is the ease of writing service files. 
They aren't scripts.
Instead, they're basic configuration files.
While they can grow to be complex, they are usually very simple.
### background
The main directive is ExecStart, which specifies the command that should be run when the service is started. The command is 
```bash
/usr/bin/python3 /root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/run.py. 
```
Here's what each part of the command does:

/usr/bin/python3
: This specifies the Python interpreter that should be used to run the code.

-m
: This option tells Python to run a module as a script.

/root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/run.py
: This is the path to the Python module that should be run as a script.

So when the service is started,
the Python interpreter will run the `run.py` module
located in the `/root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/` directory.

This code above is running `FreeTAKServer-UI`,
which is a user interface for  `FreeTAKServer`.
When the Systemd service is started,
it will start the `FreeTAKServer-UI` interface,
allowing users to interact with the `FreeTAKServer` software through a web browser.

!!! note
    You will need create two separate systemd files, if you're using Web UI
    - fts.service
    - fts-ui.service


### Create The File
Systemd services exist at 
```/etc/systemd/system.```
or
```
/usr/lib/systemd/system/
```
Any `.service` file that you create in that directory can be run as a service,
if you construct it properly. 
Create a file that you would like with the `.service` extension. 
In our case,
to create a file as `/etc/systemd/system/FreeTAKServer.service` with the following content:
(modify the parameters as needed)

```ini
{!Troubleshooting/fts.service!}
```

And reload systemd, so it will load new unit file:
```
sudo systemctl daemon-reload
```

### Start the `fts.service`
```
sudo systemctl start fts.service
```

### Get the Status of the `fts.service`
```
sudo systemctl status fts.service
```

### Stop the `fts.service`
```
sudo systemctl stop fts.service
```

### Start the `fts.service` with the system
```
sudo systemctl enable fts.service
```

## UI Service
similarly the UI service can be created with `/etc/systemd/system/fts-ui.service`
```ini
{!Troubleshooting/fts-ui.service!}
```

started 

see also [ZeroTouchInstall Services section](../Installation/mechanism/Ansible/ZeroTouchInstall.md)
to see the complete list of the services created by the installer
