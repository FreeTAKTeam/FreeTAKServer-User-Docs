
# UAS tool

The UAS Tool is a plug-in that provides integration of Unmanned Aircraft Systems (UAS)
for enhanced Situational Awareness (SA) and telemetry data, Full Motion Video (FMV), and command and control (C2).
The following instructions have been updated for tool compatible with `ATAK` 4.8.1.

## Connect UAS tool to FTS infrastructure
 * Make sure all devices are connected to the FTS server on the Digital Ocean (DO) droplet.
 * Open UAS tool settings, go to "Video Broadcast preferences", click on "video broadcast destination and change it to RTSP-Push"
 * Scroll down to the "RTSP-push configuration " section, click the "video destination ip address" and enter only the ip address of the DO droplet, do not enter port or paths here. hit ok.
 * Next click on the "video destination port", enter only the port of the video server here 8554. hit ok.
 * Click on "video broadcast Identifier" and enter something like
   `live/CorvoUAS` (no quotation marks) unless it is already filled in. hit OK
 *  Scroll down and under the "other" section click on "video observer URL". If this is not already filled in, enter `rtsp://[yourIPhere]:[port]/live/example` (should look something like this  again no quotation marks
   `rtsp://132.233.124.12:8554/live/corvo` 
 * Then on the receiving device repeat steps 5a-9a and enter the same information that you did on the UAS EUD. All devices wishing to view the stream should now have identical settings (including same ip, port, video broadcast identifier etc.). 
* Start streaming the broadcast from the UAS EUD. On the receiving EUD back out to the list of UAS's and click the play button. Should start streaming the video.

* in the client (e.g. `WinTAK`, you can use the plugin to see the position of the Drone
  ![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/382e7f53-4f90-43d0-b901-9a79c0ef3d6d)

* also without a plugin, if you have the [videoCheck] configured, you will receive a new video feed

  ![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/42c4178c-52dc-441c-a395-dcb3c968bdf7)
