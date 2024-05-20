
# Removing or Updating FTS

In **certain cases**, if you already installed FTS with ZeroTouch Installer or pip you can use
the pip upgrade command to update your FTS to the current version.

This is **not** warranted to work, so backup your data before attempting.



## To update your FTS installation:

- SSH to your FTS server

- Run upgrade commands:

```shell
	/opt/fts.venv/bin/pip install --upgrade freetakserver-ui
```

```shell
	/opt/fts.venv/bin/pip install --upgrade freetakserver
```
	
- Reconfigure your config.py file:
```shell
	sudo nano /root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/config.py
		- Change the IP and WEBMAPIP to the address of your FTS server
		- Change the APPIP to 0.0.0.0
```
	
- Restart Services
```shell
    sudo systemctl stop fts
	sudo systemctl stop fts-ui
	sudo systemctl start fts
	sudo systemctl start fts-ui
```
