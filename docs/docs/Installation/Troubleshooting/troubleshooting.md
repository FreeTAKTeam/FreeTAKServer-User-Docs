# Troubleshooting

## My XXX component is not connecting / showing
for fts check out 
/opt/FTSConfig.yaml

for the UI check out
/usr/local/lib/python3.8/dist-packages/FreeTAKServer-UI/config.py

for the webmap check out
/opt/webMAP_config.json

for the video server check out
/opt/rtsp-simple-server.yml

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
