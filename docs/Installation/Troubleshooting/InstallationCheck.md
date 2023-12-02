# Checking Your Installation

## Check FreeTAKServer, FreeTAKServer-UI, and WebMap

Open a web browser to:

```
http://<YOUR_IP_ADDRESS>:5000/
```

- login with your credentials
- by default is admin/password (you should immediately change the standard password) 
- check whether services are OK (blue)
![image](https://user-images.githubusercontent.com/60719165/148986287-0c83aa3f-e909-4b38-bc81-d66cddb08f89.png)
- connect a client to the server
- click on the WEBMAP button
- confirm the client is connected in the WEBMAP

## Check The Video Server

Open a web browser to:

```
http://<YOUR_IP_ADDRESS>:9997/v1/config/get
```

Confirm the configuration (which is in `json` format):

```json
{
  "logLevel": "info",
  "logDestinations": [
    "stdout"
  ],
  "logFile": "rtsp-simple-server.log",
  "readTimeout": "10s",
  "writeTimeout": "10s",
  "readBufferCount": 512,
  "api": true,
  "apiAddress": "<YOUR_IP_ADDRESS>:9997",
  "metrics": false,
  "metricsAddress": "127.0.0.1:9998",
  "pprof": false,
  "pprofAddress": "127.0.0.1:9999",
  "runOnConnect": "",
  "runOnConnectRestart": false,
  "rtspDisable": false,
  "protocols": [
    "multicast",
    "tcp",
    "udp"
  ],
  "encryption": "no",
  "rtspAddress": ":8554",
  "rtspsAddress": ":8555",
  "rtpAddress": ":8000",
  "rtcpAddress": ":8001",
  "multicastIPRange": "224.1.0.0/16",
  "multicastRTPPort": 8002,
  "multicastRTCPPort": 8003,
  "serverKey": "server.key",
  "serverCert": "server.crt",
  "authMethods": [
    "basic",
    "digest"
  ],
  "readBufferSize": 2048,
  "rtmpDisable": false,
  "rtmpAddress": ":1935",
  "hlsDisable": false,
  "hlsAddress": ":8888",
  "hlsAlwaysRemux": false,
  "hlsSegmentCount": 3,
  "hlsSegmentDuration": "1s",
  "hlsAllowOrigin": "*",
  "paths": {
    "~^.*$": {
      "source": "publisher",
      "sourceProtocol": "automatic",
      "sourceAnyPortEnable": false,
      "sourceFingerprint": "",
      "sourceOnDemand": false,
      "sourceOnDemandStartTimeout": "10s",
      "sourceOnDemandCloseAfter": "10s",
      "sourceRedirect": "",
      "disablePublisherOverride": false,
      "fallback": "",
      "publishUser": "",
      "publishPass": "",
      "publishIPs": [],
      "readUser": "",
      "readPass": "",
      "readIPs": [],
      "runOnInit": "",
      "runOnInitRestart": false,
      "runOnDemand": "",
      "runOnDemandRestart": false,
      "runOnDemandStartTimeout": "10s",
      "runOnDemandCloseAfter": "10s",
      "runOnPublish": "",
      "runOnPublishRestart": false,
      "runOnRead": "",
      "runOnReadRestart": false
    }
  }
}
```

## Check the FreeTAKHub Server (or Node-RED Server)

Open a web browser to:

```
http://<YOUR_IP_ADDRESS>:1880/
```

Confirm you see a login prompt.
see [NodeRed](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/FreeTAKHub/Integration/NodeRedinstallation.md) for more information

## Check Voice server
connect a client to <YOUR_IP_ADDRESS>:64738
