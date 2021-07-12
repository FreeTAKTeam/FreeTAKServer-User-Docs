![freeTAKUAS_Logo](https://user-images.githubusercontent.com/60719165/124395705-edc52180-dcdb-11eb-879b-725d486eaa43.png)

# Introduction
FreeTAK UAS (FTUAS) is an Android application that can:

* Control any DJI drone supported by the current DJI SDK
* Stream the position of the drone to all the connected TAK clients
* Stream the video Feed to all the connected TAK clients
* Create a "target" on the map and stream with all the connected TAK clients

# Requirements

* FreeTAK UAS app
* DJI compatible drone
* FTS v 1.9 (or better): the application will NOT support the legacy TAK server.
* the FTS REST API service must be activated
* You have a valid REST Token (created in the FTS UI under System User) 
* FTH Video Service (or compatible RTMP server) if you want to stream live videos

# Installation

* Assuming that you have installed and configured your [FTS](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/PyPi/Linux/Install.html) 
* and the  [video service](https://github.com/FreeTAKTeam/FreeTAKHub/blob/main/README.md), 
* download the [APK installation file](coming soon) on your phone / tablet and follow the instructions.
* if the installation is suvcessful you should have a new Icon

![image](https://user-images.githubusercontent.com/60719165/124396013-9d4ec380-dcdd-11eb-8cf9-bf1deaa7adc0.png)


# Usage

## Connection
![image](https://user-images.githubusercontent.com/60719165/124395573-3e884a80-dcdb-11eb-8a89-9f6b4a8df202.png)

* start your drone
* start your controller
* connect the phone with FTUAS to the controller
* a popup will ask wich application you want to open
* select FTUAS and configure the following:
  * FTS IP and Port
  * Video Server IP and port
  * the Drone name
  * Now click on UAS [READY]

## Interface
![image](https://user-images.githubusercontent.com/60719165/124395601-64155400-dcdb-11eb-8142-67e14c08d712.png)
the FTUAS interface is typical of DJI the following is special:

* As soon you switch to it  the drone will start streaming the camera
* As soon you switch to it the drone will share his position with the FTS server, that will foward to all the connected clients
* the "Red Dot" in the middle can be tappped to create a geoObject of type "Unknow" call target and send to all the connected clients 
* the vertical aim of the "Red Dot" can be changed by moving the gimbal
* in some model, it's also possible to aim the gimbal independent from the position of the drone by dragging the position on screen
* In the current version, the aim is not perfect so expect some delta

## ATAK Interface
### Map
![image](https://user-images.githubusercontent.com/60719165/124395620-77c0ba80-dcdb-11eb-88dd-f3eac3468962.png)
In ATAK the drone shows:

* a white zone (field of view)
* a Sensor Point of Interest (SPI)
* the position and name of the drone

### Menu
![image](https://user-images.githubusercontent.com/60719165/124395651-9fb01e00-dcdb-11eb-892f-20e3eb8a3484.png)
to visualize the video tap the drone's icon and then the video icon

### Video Player
![image](https://user-images.githubusercontent.com/60719165/124395672-be161980-dcdb-11eb-9aea-162bd605080e.png)
In alternative open the ATAK video player and search for the name of your drone

NOTICE: in the current version, every time a new video endpoint will be created, this must be manually deleted. 


