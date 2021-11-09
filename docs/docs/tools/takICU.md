# TAK ICU
TAK ICU is a Android application allowing to stream video and position to a compatible RTSP server. When TAK device connects to the stream, not only it gets the video feed but also his current position and bearing visualized in the map.
The product is maitanined by the TAK product center and can be accessed [here](https://drive.google.com/drive/folders/1PmCiWlHvIWXdW7pcudCFg6irghvOn6Ah).

This page describe the TAK ICU tool only. Please refer to other pages for configuaration of the different parts.





## client Installation ANDROID ONLY
* dowload [TAK ICU](https://drive.google.com/drive/folders/1PmCiWlHvIWXdW7pcudCFg6irghvOn6Ah)
* install TAK ICU as a regular Android App

## Client configuration
* Start ICU
* Tap the preferences 
* As destination type use "Wonza Server"
* As Broadcast Alias use your TAK ID (e.g. Corvo). It needs to be a single word, if broadcast alias has space it fails.
* Scroll down to "Wonza Server preferences"
* Set your RTSP server Ip as Wonza server IP (e.g. 147.182.190.54)
* Set the server port to 8554
* close the preferences

## Usage
* Ensure that you have a GPS fix
![image](https://user-images.githubusercontent.com/60719165/140655585-ebd10d4d-620e-4259-85e2-897770d08fed.png)
with GPS unavailable your stream cannot be associated to a map
*  check that broadcast is checked
*  press the broadcast button

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



