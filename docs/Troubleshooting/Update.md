
# Update
in **certain cases**, if you already installed FTS with pip you can use
```shell
pip install --upgrade FreeTAKServer[UI]
```
this is **not** warranted to work with version 1.9.9,
often the best way is to delete the installation (saving first the data) and start from zero.

To remove your installation
```shell
sudo rm -r /usr/local/lib/python3.11/FreeTAKServer
```

### SSH to your FTS server

### Run upgrade command:
	/opt/fts.venv/bin/pip install --upgrade freetakserver-ui
	/opt/fts.venv/bin/pip install --upgrade freetakserver
	
### Reconfigure your config.py file:
	sudo nano /root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/config.py
	Change the IP and WEBMAPIP to the address of your FTS server
	Change the APPIP to 0.0.0.0
	
### Restart Services
    sudo systemctl stop fts
	sudo systemctl stop fts-ui
	sudo systemctl start fts
	sudo systemctl start fts-ui
