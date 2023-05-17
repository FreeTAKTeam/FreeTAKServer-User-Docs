# UAS tool

The UAS Tool is a plug-in that provides integration of Unmanned Aircraft Systems (UAS) for enhanced Situational Awareness (SA) and telemetry data, Full Motion Video (FMV), and command and control (C2).
 Connects UAS tool to FTS infrastructure
 * Make sure all devices are connected to the FTS server on the Digital Ocean (DO) droplet.
 * Open UAS tool settings, go to "network preferences", click on "video broadcast destination and change it to Wowza Server"
 * Scroll down to the "Wowza preferences" section, click the "video destination ip adress" and enter only the ip adress of the DO droplet, do not enter port or paths here. hit ok.*
 * Next click on the "video destination port", enter only the port of the video server here (8554 worked for me). hit ok.
 * Click on "video broadcast Identifier" and enter something like "live/example" (no quotation marks) unless its already filled in. hit ok
 *  Scroll down and under the "other" section click on "video observer URL". If this is not already filled in, enter "rtsp://[yourIPhere]:[port]/live/example" (should look something like this "rtsp://132.233.124.12:8554/live/example" , again no quotation marks)
 * Then on the recieving device repeat steps 5a-9a and enter the same information that you did on the UAS EUD. All devices wishing to view the stream should now have identical settings (including same ip, port, video broadcast identifier etc). 
* Start streaming the broadcast from the UAS EUD. On the recieving EUD back out to the list of uas's and click the play button. Should start streaming the video.
