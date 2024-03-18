---
status: ood
---

# Troubleshooting

## My Windows Installation is failing
While FTS will work with this OS, we do not support it

## My Ubuntu 22.04 Installation is failing
FTS 2.0 supports 22.04 older versions require Ubuntu 20.04

## My FTS Installation is failing
FTS 2.0 has been tested with Python 3.11, 
should work with others version (3.10). 
Older versions require 3.8

## My Raspberry Pi installation has an issue with the WebMap
This has been addressed, so you should not have the issue. 
The older webmap was a Nodered packaged component, compiled for AMD64, so it will not run in the Pi.
You need to:
 * install Node Red 
 * import the flow from source
 * configure the flow

## Initial setup doesn't ask to create a YAML file, how to make one manually?
copy this code, adapting to your environment

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
 * depending on inbound traffic, this can become very large and subsequently, need to be manually deleted

## My XXX component is not connecting / showing
for fts check out 
```
/opt/FTSConfig.yaml
```

for the UI check out
```
/root/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/config.py
or
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

## SSL connection is working but in an inconsistent way
ISSUE: SSL certs are not working
Cause: the certs are duplicated on your machine

This has been observed on `ATAK` 4.7 + and `WinTAK` for functions that requires both encrypted TCP and SSL connections.
The `ExCheck` plugin is an example of that. 
The main symptom on the client is that the connection to the server fails (for specific functions).
This is NOT a FTS issue, it's provoked by the way `ATAK` stores certificates.

### Workaround `ATAK` 
 * clear the content using the `ATAK` function  
![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/70561476-2252-46eb-8a9e-c7a0717b8d78)
 * create a new user with mobile certs
 * connect to FTS using TCP
 * download new the certs
 * de-activate tcp and activate the new certs
### Workaround `WinTAK` 
 
 * physically delete all the certs with the name (IP) of your sever from the machine in `WinTAK` the certs are located in
   ```C:\Users\[USERNAME]\AppData\Roaming\WinTAK\SslCerts``` 
 * Proceed as above but use `WinTAK` certs

## Using SSL I get frequent disconnects
This is a problem of the client not sending data. 

`WinTAK`
: under settings/network preferences set the TCP Connection timeout higher, (e.g. 60 seconds)

`ATAK`
: under settings/network preferences/ network connection preferences / TCP connection timeout  (e.g. 40 seconds)

## package not found
if, trying to start FTS you get an error 'package not found'
```
'package not found'
```
navigate to the physical location where the controllers are installed and start the server from there.

You may also check for missing libraries and install then using pip

## issue connecting in `WinTAK`
if you have issues connecting `WinTAK` to FTS, 
try to deactivate the TAKChat plugin, under the plugin section

## Issues connecting using SSL
If you have issue connecting to FTS using SSL, 
even if you have downloaded new certs, you need to manually delete the old files from your device. 
In `WinTAK` (tested with 4.9)  you can find certs files under 
```
C:\Users\[USERNAME]\AppData\Roaming\WinTAK\SslCerts
```
you should have 3 certifications files of the form:

 * \[IP]_FreeTAKServer-Hash
 * 198-199-70-185_FreeTAKServer-2-a3_wbu7kirkizulslz1pstvv0xoo5qbcrr4.p12.dat2

and another 3 of the form:

 * [UserNAME]Hash
 * FreeTAKTeamSupporte4fddab2-6102-4ab6-a9ec-0fee8edf8b10.p12

## `client2client` datapackages
If you have issues sending datapackages directly to clients via FTS, 
make sure the `-IP` argument you specified can be reached from your device.
A quick way to test if it works is to take a picture with Quick Pic in `ATAK` and send it to another client.
Please also note that for that test `ATAK` clients needs to be on different network (ie one on mobile and one on `wifi`), because if you run them in same network (`WiFi`, `VPN`, etc.) they will just use same multicast group, bypassing FTS completely.  
When you post package to specific contact in `ATAK`, following happens:  

  1) Datapackage is uploaded to server, recorded in database and stored in FTS directory  
  2) Client receives payload with URL pointing to datapackage so `ATAK` can download it   

Assuming you want to run open-to-everyone FTS instance, and you have server hosted somewhere,
you need to specify _public_ IP address in `-IP` argument.
And just in case, `-IP` also accepts domain names.
If you run it at home and port forward on router doesn't work,
check if you receive actual IP address and not being NATed
and ports 8080 and 8087 are not filtered - you can ask your ISP about that.
