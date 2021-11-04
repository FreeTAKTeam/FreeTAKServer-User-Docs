# TAK ICU
TAK ICU is a Android application allowing to stream video and position to a compatible RTSP server. When TAK device connects to the stream, not only it gets the video feed but also his current position and bearing visualized in the map.
The product is maitanined by the TAK product center and can be accessed here (https://drive.google.com/drive/folders/1PmCiWlHvIWXdW7pcudCFg6irghvOn6Ah)[https://drive.google.com/drive/folders/1PmCiWlHvIWXdW7pcudCFg6irghvOn6Ah].

## Integration with FTS
The FTS integration exists since FTS 1.9.5, it allows to seamless stream videos by simply connecting to the video server.

Normally, when a device is streaming video, connected TAK EUD will be not notified, it's necessary to manually create a new feed in the software.

![image](https://user-images.githubusercontent.com/60719165/139940405-8e841a98-58e3-431a-8bb6-fce8462b3ef7.png)


the video stream is sent to all the connected TAK Devices

![image](https://user-images.githubusercontent.com/60719165/139935868-59624431-1f17-4503-8c6a-d682f75d97c1.png)

Now you can retrieve it in your video list

![image](https://user-images.githubusercontent.com/60719165/140366998-04bf25e8-f45e-4e8b-9752-742f2502ca50.png)

in the video you can open the feed and visualize it.
![image](https://user-images.githubusercontent.com/60719165/140365180-253b2150-24d5-48b4-94f5-e66d1d02f053.png)

touching the globe, you will jump to the location of the stream, to see it's context

![image](https://user-images.githubusercontent.com/60719165/140366296-bf24262a-ba53-47f9-bafa-952d917350e0.png)


## Architecture
![image](https://user-images.githubusercontent.com/60719165/140407685-ce123520-6199-4cc6-ab3f-d07103dc868e.png)
FTS 1.9 requires up-to 5 different nodes (VMs). In this use case it's suggested to use 3 different servers.

_While it's possible to run all on the same machine, performances will be severly affected_

Android Phone for spotter: an android phone with TAK ICu installed. Used by the spotter to send the video stream.

Video Service: simple RTSP server 0.7 or better with APi activated. 
the video Service checker uses the API to verify if streams are running there and notify FTS
FTH server: runs other integrations such as Telegram Connector, Video Service Checker, check-in system, SALUTe report  and Global Emergency Checker
FTS Cloud Server: hosts the core of FTS
Android Phone(s) for team member(s): this phone has ATAK installed
FTS send a notification with the COT
ATAK shows the video, connecting to the FTS to visualized the COT and to the video server to get the video feed.


## Installation
* install FTS 1.9 +
* Install RTSP-simple Server v0.17.0 +
* install the NodeRed Flow in your FTS hub

## Configuration
* API service must be active on FTS 
* API service must be active on RTSP-simple Server
* in the node "Post  Video to FTS" configure your Rest API token

![image](https://user-images.githubusercontent.com/60719165/139943631-4c6dd8ef-80fa-439c-be9c-84280ad8103c.png)
