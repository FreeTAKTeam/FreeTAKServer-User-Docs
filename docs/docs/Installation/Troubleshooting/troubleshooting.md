# Troubleshooting

## My Windows Installation is failing
While FTS will work with thiis OS, we do not support it

## My Ubuntu 22.04 Installation is failing
FTS 2.0 supports 22.04 older versions require Ubuntu 20.04

## My FTS Installation is failing
FTS 2.0 has been tested with Python 3.11, should work with others verson (3.10). Older versions require 3.8

## My Raspberry Pi installation has an issue with the WebMap
This has been adressed, so you should have the issue.
The older webmap was a Nodered packaged component, compiled for AMD64, so it will not run in the Pi.
You need to:
 * install Node Red 
 * import the flow from source
 * configure the flow

## Initial setup doesn't ask to create a YAML file, how to make one manually?
copy this code, adapting to your enviroment

```
System:
  FTS_DATABASE_TYPE: SQLite
  FTS_CONNECTION_MESSAGE: Connected
  FTS_OPTIMIZE_API: True
  FTS_MAINLOOP_DELAY: 1
Addresses:
  FTS_COT_PORT: 8087
  FTS_SSLCOT_PORT: 8089
  FTS_DP_ADDRESS: [YOUREXTERNALIP]
  FTS_USER_ADDRESS: [YOUREXTERNALIP]
  FTS_API_PORT: 19023
  FTS_FED_PORT: 9000
  FTS_API_ADDRESS: [YOUREXTERNALIP]
FileSystem:
  FTS_CONFIG_PATH: /opt/FTSConfig.yaml
  FTS_DB_PATH: /opt/FreeTAKServer.db
  FTS_COT_TO_DB: True
  FTS_MAINPATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer
  FTS_CERTS_PATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs
  FTS_EXCHECK_PATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/ExCheck
  FTS_EXCHECK_TEMPLATE_PATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/ExCheck/template
  FTS_EXCHECK_CHECKLIST_PATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/ExCheck/checklist
  FTS_DATAPACKAGE_PATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/FreeTAKServerDataPackageFolder
  FTS_LOGFILE_PATH: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/Logs
Certs:
  FTS_SERVER_KEYDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/server.key
  FTS_SERVER_PEMDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/server.pem
  FTS_TESTCLIENT_PEMDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/Client.pem
  FTS_TESTCLIENT_KEYDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/Client.key
  FTS_UNENCRYPTED_KEYDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/server.key.unencrypted
  FTS_SERVER_P12DIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/server.p12
  FTS_CADIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/ca.pem
  FTS_CAKEYDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/ca.key
  FTS_FEDERATION_CERTDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/server.pem
  FTS_FEDERATION_KEYDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/server.key
  FTS_CRLDIR: /usr/local/lib/python3.11/dist-packages/FreeTAKServer/certs/FTS_CRL.json
  FTS_FEDERATION_KEYPASS: [YOURPASS]
  FTS_CLIENT_CERT_PASSWORD: [YOURPASS]
  FTS_WEBSOCKET_KEY: [YOURPASS]
```


## after XXX months of use the disk is full
 * FTS writes the output of the service to a log located here:
```
/var/log/fts/fts-stdout.log
```
 * depending from traffic this can become very large and need to be manually deleted

## My XXX component is not connecting / showing
for fts check out 
```
/opt/FTSConfig.yaml
```

for the UI check out
```
/usr/local/lib/python3.11/dist-packages/FreeTAKServer-UI/config.py
```

for the webmap check out
```
/opt/webMAP_config.json
```
for the video server check out
```
/opt/mediamtx.yml
```

## using SSL I get frequent disconnects
This is a problem of the client not sending data. 
WinTAK: under settings/network preferences set the TCP Connection timeout higher, (e.g. 60 seconds)
ATAK:  under settings/network preferences/ network connection preferences / TCP conection timeout  (e.g. 40 seconds)

## package not found'
if, trying to start FTS you get an error 'package not found'
```
'package not found'
```
navigate to the physical location where the controllers are installed and start the server from there.

You may also check for missing libraries and install then using pip

## issue connecting in WinTAK
if you have issues connecting winTAK to FTS, try to deactivate the TAKChat plugin, under the plugin section

## client2client datapackages
If you have issues sending datapackages directly to clients via FTS, make sure the `-IP` argument you specified can be reached from your device.  
A quick way to test if it works is to take a picture with Quick Pic in ATAK and send it to another client. Please also note that for that test ATAK clients needs to be on different network (ie one on mobile and one on wifi), because if you run them in same network (wifi, vpn, etc) they will just use same multicast group, bypassing FTS completely.  
When you post package to specific contact in ATAK, following happens:  

  1) Datapackage is uploaded to server, recorded in database and stored in FTS directory  
  2) Client receives payload with URL pointing to datapackage so ATAK can download it   

Assuming you want to run open-to-everyone FTS instance, and you have server hosted somewhere, you need to specify _public_ IP address in `-IP` argument. And just in case, `-IP` also accepts domain names.   
If you run it at home and port forward on router doesn't work, check if you receive actual IP address and not being NATed and ports 8080 and 8087 are not filtered - you can ask your ISP about that.
