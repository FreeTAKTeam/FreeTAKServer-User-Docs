# Check your installation
set of test to see that your FTS installation was successful

## Check FTS (Core + UI + WebMap) 
open a browser to

```
http://[YOURIP]::5000/
```
- login with admin / password
- change your password immediately
- check if the services are on OK (blue)
![image](https://user-images.githubusercontent.com/60719165/148986287-0c83aa3f-e909-4b38-bc81-d66cddb08f89.png)
- connect a client to the server
- click on the Webmap tab
- you should see the client connected in the webmap



## Check video server
open a browser to
http://[YOURIP]:9997/v1/config/get

you will see a configuration in Json format like this
```
{"logLevel":"info","logDestinations":["stdout"],"logFile":"rtsp-simple-server.log","readTimeout":"10s","writeTimeout":"10s","readBufferCount":512,"api":true,"apiAddress":"167.71.128.102:9997","metrics":false,"metricsAddress":"127.0.0.1:9998","pprof":false,"pprofAddress":"127.0.0.1:9999","runOnConnect":"","runOnConnectRestart":false,"rtspDisable":false,"protocols":["multicast","tcp","udp"],"encryption":"no","rtspAddress":":8554","rtspsAddress":":8555","rtpAddress":":8000","rtcpAddress":":8001","multicastIPRange":"224.1.0.0/16","multicastRTPPort":8002,"multicastRTCPPort":8003,"serverKey":"server.key","serverCert":"server.crt","authMethods":["basic","digest"],"readBufferSize":2048,"rtmpDisable":false,"rtmpAddress":":1935","hlsDisable":false,"hlsAddress":":8888","hlsAlwaysRemux":false,"hlsSegmentCount":3,"hlsSegmentDuration":"1s","hlsAllowOrigin":"*","paths":{"~^.*$":{"source":"publisher","sourceProtocol":"automatic","sourceAnyPortEnable":false,"sourceFingerprint":"","sourceOnDemand":false,"sourceOnDemandStartTimeout":"10s","sourceOnDemandCloseAfter":"10s","sourceRedirect":"","disablePublisherOverride":false,"fallback":"","publishUser":"","publishPass":"","publishIPs":[],"readUser":"","readPass":"","readIPs":[],"runOnInit":"","runOnInitRestart":false,"runOnDemand":"","runOnDemandRestart":false,"runOnDemandStartTimeout":"10s","runOnDemandCloseAfter":"10s","runOnPublish":"","runOnPublishRestart":false,"runOnRead":"","runOnReadRestart":false}}}
```

### NodeRed
open a browser to
```
http://[YOURIP]::8081/
```
you should see a prompt to login
