---
status: current
---

# TAK ICU

TAK ICU is an Android Team Awareness Kit (`ATAK`) support plugin that allows a user to stream video and position to a compatible RTSP server.
An operator running TAK ICU sends video and telemetry to the RTSP server,
and the observer(s) can view the video and telemetry on any compatible end-user device (EUD) that is connected to the server.
Telemetry transmitted includes the senders position location information (PLI),
field-of-view (FOV), focal point distance, and compass heading. 
 
The product is a bundled support app, and is maintained by the [TAK Product Center](https://tak.gov/products/atak-civ).

This page describes the TAK ICU tool only.

## Client Installation (ANDROID ONLY)

* Install `ATAK` from the [TAK Product Center](https://tak.gov/products/atak-civ)
* Install/Enable the TAK ICU support plugin from Settings > Plugins
* The install/enable creates a separate app icon to access TAK ICU, which may need to be added to your home screen

## Client configuration

* Start TAK ICU
* Tap the preferences (hamburger menu, top-right) 
* Tap Settings (gear icon) 
* Under Application Settings, select Broadcast Preferences
* In BROADCAST PREFERENCES, select Destination Type > Wowza Server
* In BROADCAST PREFERENCES, select Broadcast Alias and set it to your TAK ID (e.g. Corvo). It needs to be a single word, if broadcast alias contains a space it will fail.
* Scroll down to WOWZA SERVER PREFERENCES
* In WOWZA SERVER PREFERENCES > Wowza Server IP, specify your RTSP server IP address (e.g. 147.182.190.54)
* In WOWZA SERVER PREFERENCES > Wowza Server Port, Set the server port to 8554
* Tap the gear icon to close Settings

## Usage

* Ensure that you have a GPS fix
![image](https://user-images.githubusercontent.com/60719165/140655585-ebd10d4d-620e-4259-85e2-897770d08fed.png)
*  Again, ensure that you have a GPS fix!  Best-case, without a GPS fix, your video will not be associated to a map location and telemetry will fail.  Worst-case, the video broadcast will not even start.
*  Check the Broadcast checkbox
*  Press the Broadcast/Record button to begin streaming

## Integration with FTS

The FTS integration, [FreeTAKHub_VideoChecker](https://github.com/FreeTAKTeam/FreeTAKHub_VideoChecker) exists since FTS 1.9.5.
It allows for seamless streaming of videos by simply connecting to the video server.

Normally, when a device is streaming video, connected TAK EUD will be not notified,
it's necessary to manually create a new feed in the software.

![image](https://user-images.githubusercontent.com/60719165/139940405-8e841a98-58e3-431a-8bb6-fce8462b3ef7.png)

The video stream is sent to all the connected TAK Devices

![image](https://user-images.githubusercontent.com/60719165/139935868-59624431-1f17-4503-8c6a-d682f75d97c1.png)

Now you can retrieve it in your video list

![image](https://user-images.githubusercontent.com/60719165/140366998-04bf25e8-f45e-4e8b-9752-742f2502ca50.png)

In the video you can open the feed and visualize it.
![image](https://user-images.githubusercontent.com/60719165/140365180-253b2150-24d5-48b4-94f5-e66d1d02f053.png)

Touching the globe, you will jump to the location of the stream,
to see its context

![image](https://user-images.githubusercontent.com/60719165/140366296-bf24262a-ba53-47f9-bafa-952d917350e0.png)



