# REST API - Public

The FreeTAKServer REST API is a human readeble approach to the TAK world. The API allows you to easily connect third parties to the TAK family, without the need to understand the complexity of the COT structure or what a TCP connection is. FTS also supports an [Internal API](REST_API_InternalDoc.md).

## How FTS manages the information

FTS will send the  information coming trough the API to all the connected clients, addtionally it will save it to the persistency, to be query in future. 

## List of supported API

In the current release (1.9), FTS supports following API:

  * ManageAPI/getHelp
  * ManageGeoObject/postGeoObject
  * ManageGeoObject/putGeoObject
  * ManageGeoObject/getGeoObject
  * ManageGeoObject/getGeoObjectByZone
  * ManageEmergency/postEmergency
  * ManageEmergency/getEmergency
  * ManageEmergency/deleteEmergency 
  * ManageChat/postChatToAll
  * ManageRoute/postRoute
  * ManagePresence/postPresence
  * ManagePresence/putPresence 
  * ManageVideoStream/postVideoStream
  * Sensor/postDrone
  * Sensor/postSPI
  * /ManageKML/postKML
  
## General Configuration

> To quickly test the API, you can use a browser extension like ARC Advanced rest client (Chrome). REST APIs are easy to use, however they require a minimum ammount of knowledge, we DO NOT provide support to explain WHAT an API is. Please refer to an online tutorial such as [this](http://www.steves-internet-guide.com/using-http-apis-for-iot-beginners-guide/). 

### Endpoint

The API uses the following format:

```
VERB [Protocol]://IP:PORT/APIName/action
```

For example:

```
POST http://104.58.20.216:19023/manageGeoObject/postGeoObject
```

### Authorization

To use the API you need to have a REST API key.
The authorization is placed in the header of the message.

```
Authorization: Bearer [YOUR_API_KEY]
```

> You need to use the string 'Bearer' before YOUR_API_KEY

A valid key is generated from FTS' [CLI](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/CLI.md) or, since 1.4 also from the Web UI, and stored into the DB.

To add an API user in the CLI type:

```
add_api_user
```

See CLI help for details.
To create a REST API key using the Web UI, go to the User section and give an user a token..
Token: gives an unique combination that this user can leverage for the FTS REST API. NOTICE:  the field token is for any alphanumeric string. the prefix 'bearer' is NOT part of the token. The name “Bearer authenticatio
To consume the API you will need to request a key to your FTS admin. 

The following is a non-working example of a key:

```json
{
  "Authorization": "Bearer meg@secre7apip@guesmeIfyouCan"
}
```

### Message

In most end points, the message is placed in the body of the request as JSON formatted. See below for detailed examples.
In the API using the *Get* verbs it's a variable.

## API Details

### manageAPI

Set of commands relative to API management.

#### getHelp

Retrieve API version and supported endpoints.
 * verb: GET
 * endpoint: /manageAPI/getHelp
 * returns: json containing API version and supported endpoints

##### getHelp Example: return data (1.9.5)

```json
{"APIVersion": "1.9.5", "SupportedEndpoints":
["/ManageNotification/getNotification", "/ManageVideoStream/deleteVideoStream", "/ManageVideoStream/postVideoStream", "/ManageVideoStream/getVideoStream", "/ManageSystemUser/putSystemUser",
"/ManageEmergency/deleteEmergency",
"/ManageGeoObject/postGeoObject",
"/ManageEmergency/postEmergency",
"/ManageGeoObject/getGeoObject", "/ManageGeoObject/putGeoObject", "/ManageEmergency/getEmergency", "/ManagePresence/postPresence", "/ManagePresence/putPresence", "/ManageRoute/postRoute", "/SystemUser/deleteSystemUser", "/SystemUser/postSystemUser", "/ManageChat/postChatToAll", "/ManageCoT/getZoneCoT", "/ManageKML/postKML", "/manageAPI/getHelp", "/Sensor/postDrone", "/Sensor/postSPI", "/BroadcastDataPackage", "/ManageVideoStream", "/AuthenticateUser", "/DataPackageTable", "/ManageGeoObject", "/ManageEmergency", "/FederationTable", "/ManagePresence", "/MissionTable", "/ExCheckTable", "/SendGeoChat", "/ManageRoute", "/checkStatus", "/GenerateQR", "/ManageChat", "/RecentCoT", "/APIUser", "/Clients", "/Sensor", "/MapVid", "/Alive", "/URL"]}
```

### manageGeoObject 

A GeoObject is an element place on a map. It has a name, characteristics, and an attitude.

#### postGeoObject

* verb: POST
* endPoint: /ManageGeoObject/postGeoObject
* returns: UID
 
##### Parameters

* GeoObject: It's the information that will determine which type will be placed on the tak maps including his icon. Please see API documentation for a list of valid entries. Since 1.7 you can also use nicknames for the geo objects.
* longitude: OPTIONAL the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: OPTIONAL the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682).
* how: the way in which this geo information has been acquired. Please see API documentation for a list of valid entries.
* attitude: OPTIONAL the kind of expected behavior of the GeoObject (e.g friendly, hostile, unknown). Please see API documentation for a list of valid entries.
* name: a string to ID the GeoObject on a map.
* bearing: OPTIONAL since 1.7, the direction expressed in degrees (1-360). Default: 0.
* distance: OPTIONAL since 1.7, the distance in meters from the Lat/long or address.
* timeout: OPTIONAL the length, expressed in seconds until the point will stale out. Default is 300 seconds or 5 minutes.
* uid: optional input parameter, need to be an Unique Id for this element, if not present will be  server generated, if sent ATAK will try to update an existing geoObject. Use `putGeoObject` instead
* address: OPTIONAL address of destination. If sent will try to solve the exact geolocation of the destination. Possible valid examples are:
     - Big Arkansas River Park, Wichita, KS, USA 
     - Wichita, KS, USA 
     - Big Arkansas River Park, Wichita
     - and so on.

###### Example body

```json
{
  "longitude": -77.0104,
  "latitude": 38.889,
  "attitude": "hostile",
  "bearing": 132, 
  "distance": 1,
  "geoObject": "Gnd Combat Infantry Sniper",
  "how": "nonCoT",
  "name": "Putin",
  "timeout": 600  
}
```

###### Example body alternate

```json
{
  "address": "Washington, DC, USA",
  "attitude": "hostile",
  "geoObject": "Gnd Combat Infantry Sniper",
  "how": "nonCoT",
  "name": "Putin",
  "timeout": 600  
}
```

###### Other Example body alternate

```json
{
  "longitude": -77.0104,
  "latitude": 38.889,
  "distance": 500,
  "bearing": 92,
  "attitude": "hostile",
  "geoObject": "Gnd Combat Infantry Sniper",
  "how": "nonCoT",
  "name": "Putin",
  "timeout": 600  
}
```

###### Example 1.7 body

```json
{
  "longitude": -77.0104,
  "latitude": 38.889,
  "attitude": "hostile",
  "bearing": 132, 
  "distance": 1,
  "geoObject": "Medevac",
  "how": "nonCoT",
  "name": "Medevac",
  "timeout": 600  
}
```

###### Response

* 200 Success: uid. you have created the geoObject.
* [MISSING PARAMETERNAME]: you have omitted a parameter that is required.
* server error 500: you have probably misspelled the list of parameters (e.g geoObjects/supported attitude). The names are case sensitive!
* server error 400: you have probably an error in the format of your JSON query.
* server error 404: you have an error in the end point definition.
 
###### Basic GeoObjects

* "Gnd Combat Infantry Rifleman",  Nickname: "Rifleman"
* "Gnd Combat Infantry grenadier", Nickname: "Grenadier"
* "Gnd Combat Infantry Mortar" , Nickname: "Mortar" 
* "Gnd Combat Infantry MachineGunner (LMG)",  Nickname: "LMG" 
* "Gnd Combat Infantry Medic" ,  Nickname: "Medic"
* "Gnd Combat Infantry Sniper",  Nickname: "Sniper"
* "Gnd Combat Infantry Recon" ,  Nickname: "Recon"
* "Gnd Combat Infantry anti Tank" ,  Nickname: "anti Tank"
* "Gnd Combat Infantry air defense",  Nickname: "AA"
* "Gnd Combat Infantry Engineer",  Nickname: "Engineer"
* "Ground"
  
###### GeoObjects Extensions for EMS

**Extensions since 1.7**

* "Gnd Equip Vehic Civilian", Nickname: Vehicle (OK)
* "Gnd Equip Vehic Ambulance": "a-.-G-E-V-m" , Nickname: Ambulance (OK)
* "Gnd Structure IM Facilities Emergency Management": "a-.-G-I-i-e" Nickname: Emergency Station (empty shape)
* "Gnd Structure IM Facilities Law Enforcement": "a-.-G-I-i-l",  Nickname: Police Station (empty shape)
* "Gnd Structure petroleum gas oil": "a-.-G-I-R-P", Nickname: gas Station (empty shape)
* "Gnd Structure Utility Electric Power": "a-.-G-I-U-E", Nickname: Power Station (empty shape)
* "Gnd Structure Utility Telecommunications": "a-.-G-I-U-T", Nickname: Telco Station (empty shape)
* "Gnd Structure Hospital": "a-.-G-I-X-H", Nickname: Hospital (empty shape)
* "Gnd IM Resources": "a-.-G-U-i" Nickname: Resources (empty shape)
* "FOOD DISTRIBUTION": "b-r-.-O-O-O", Nickname: Food (OK, only label, need to implement nick) 
* "Gnd Crowd Control Team": "a-.-G-U-i-l-cct" Nickname: Police (OK)
* "Gnd Generators ": "a-.-G-U-i-p-gen" Nickname: Generator (empty shape)
* "Other incident other": "a-.-X-i-o" Nickname: Incident (OK, missing nick name?) 
* "Combat search &amp; rescue (CSAR)": "a-.-A-M-F-Q-H", Nickname: SAR (OK)
* "Medevac": "a-.-G-U-C-V-R-E",, Nickname: Medevac  (OK)
* "Alarm": "b-l",  Nickname: Alarm
* "Alarm/Security/Law Enforcement/Civil Disturbance or Disorder": "b-l-l-l-cd", Nickname: Disorder
* "REFUGEES": "b-r-.-O-I-R" Nickname: Refugees
* "VANDALISM/RAPE/LOOT/RANSACK/PLUNDER/SACK": "b-r-.-O-I-V" Nickname: Riot

**extensions in 1.8**

* "Other incident geo": "a-.-X-i-g", , Nickname: geo incident
* "Other incident geo avalanche": "a-.-X-i-g-a", Nickname: avalanche
* "Other incident geo earthquake": "a-.-X-i-g-e",  Nickname: earthquake
* "Other incident geo landslide": "a-.-X-i-g-l",  Nickname: landslide
* "Other incident geo subsistance": "a-.-X-i-g-s",  Nickname: subsistance
* "Other incident geo volcano": "a-.-X-i-g-v",  Nickname: volcano
* "Other incident geo eruption": "a-.-X-i-g-v-e",  Nickname: eruption
* "Other incident met drought": "a-.-X-i-m-d",  Nickname: drought
* "Other incident met cyclone": "a-.-X-i-m-c",  Nickname: cyclone
* "Other incident met tsunami": "a-.-X-i-m-n",  Nickname: tsunami
* "Other incident fire": "a-.-X-i-f",  Nickname: fire
* "Other incident medical public health": "a-.-X-i-h",  Nickname: medical incident
* "Other incident transportation vehicle accident": "a-.-X-i-t-v-a",  Nickname: vehicle accident

###### List of supported Attitudes

* "friend"
* "friendly"
* "hostile"
* "unknown"
* "pending" 
* "assumed"
* "neutral" 
* "suspect" 

###### List of supported HOW
the following list contains 
API term : Translation in the COT 

* "nonCoT": "h-g-i-g-o",
* "mensurated": "m-i",
* "human": "h-t",
* "retyped": "h-t",
* "machine": "m-",
* "gps": "m-g",       
*  "gigo": "h-g-i-g-o",
*  "mayday": "a-f-G-E-V-9-1-1",
*  "estimated": "h-e",
*  "calculated": "h-c",
*  "transcribed": "h-t",
*  "pasted": "h-p",
*  "magnetic": "m-m",
*  "ins": "m-n",
*  "simulated": "m-s",
*  "configured": "m-c",
*  "radio": "m-r",
*  "passed": "m-p",
*  "propagated": "m-p",
*  "fused": "m-f",
*  "tracker": "m-a",
*  "ins+gps": "m-g-n",
*  "dgps": "m-g-d",
*  "eplrs": "m-r-e",
*  "plrs": "m-r-p",
*  "doppler": "m-r-d",
*  "vhf": "m-r-v",
*  "tadil": "m-r-t",
*  "tadila": "m-r-t-a",
*  "tadilb": "m-r-t-b",
*  "tadilj": "m-r-t-j"}

#### putGeoObject

update an existing geoObject coordinates (can also update other features)

* verb: PUT
* endPoint: /ManageGeoObject/putGeoObject
* returns: UID

##### Parameters

* uid:  **REQUIRED**, input parameter, need to be an Unique Id for this element, if not present will be server generated, if sent ATAK will try to update an existing geoObject. Use `putGeoObject` instead.
* longitude: **REQUIRED**, the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: **REQUIRED**, the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682).
* attitude: **REQUIRED**, the kind of expected behavior of the GeoObject (e.g friendly, hostile, unknown). Please see API documentation for a list of valid entries.
* how: the way in which this geo information has been acquired. Please see API documentation for a list of valid entries.
* name: a string to ID the GeoObject on a map.
* bearing: since 1.7, the direction expressed in degrees (1-360). 
* distance: since 1.7, the distance in meters from the Lat/long.
* timeout: the length, expressed in seconds until the point will stale out. Default is 300 seconds or 5 minutes.
  
###### Example body

```json
{
  "uid": "44455566775623",
  "longitude": -66.12614,
  "latitude": 43.96552,
  "attitude": "hostile",
  "geoObject": "Sniper",
}
```

##### Response

 * 200 with UID

#### getGeoObject

retrieve in a array all geoObjects in a given radius. It uses JSON variables, not the json body

* verb: GET
* endPoint: /ManageGeoObject/getGeoObject

##### Parameters

NOTE: these should be provided in the form of url encoded variables.
 * radius: radius in meters where geoObjects, default(100).
 * longitude: longitude from which radius is calculated, default(0).
 * latitude: latitude from which radius is calculated, default(0).
 * attitude: (optional) the attitude which will be filtered, default(any). See list of supported attitudes above.

###### Example Variables

```json
{
  "longitude": -77.02385,
  "latitude": 38.989,
  "attitude": "Hostile",
  "radius": 500
}
```
 
*Params in the URL*
 http://[IP]:[PORT]/ManageGeoObject/getGeoObject?longitude=-77.0104&latitude=38.889&radius=5000

#### GetRepeatedMessages
get geo objects  that are regularly resend by the servers
* verb: GET
* endPoint: /ManageGeoObject/GetRepeatedMessages
 
### ManageChat
  
#### SendGeoChatObject
   * verb: POST
   * endPoint: /ManageChat/postChatToAll
   
##### Parameters

* message: the text of the GeoChat message
* sender: the name of the chat's sender, changing this will also change the chat room for the client.

###### Example body

```json
{
  "message": "sending this over Rest API",
  "sender": "Admin"
}
```
### ManageEmergency

#### postEmergency

create a emergency into the server

  * verb: POST
  * endPoint: /ManageEmergency/postEmergency
 
##### Parameters

  * name: the name of the person that has an emergency.
  * emergencyType: the type of emergency to be displayed
  * longitude: the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
  * latitude: the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682)
  * uid: server generated Unique Id of this element.
  * address: OPTIONAL address of emergency.

##### List of supported Emergency Types

* "911 Alert"
* "Ring The Bell"
* "Geo-fence Breached" 
* "In Contact" 

###### Example body

```json
{
  "name": "Corvo",
  "emergencyType": "In Contact",
  "longitude": -77.01395,
  "latitude": 38.889
}
```

#### getEmergency

get a list of current active emergencies 

* verb: GET
* endPoint: /ManageEmergency/getEmergency

no parameter required

##### Example  response

```json
{
  "json_list": [
    {
      "PrimaryKey": 1,
      "event_id": "459b5874-1ebf-11eb-9e70-4e58de281c19"
    }
  ]
}
```
#### deleteEmergency

delete an active emergency.
(TODO: delete of emergencies can be only done by the originator of it.)

* verb: DELETE
* endPoint: /ManageEmergency/deleteEmergency

##### Parameters

* uid: server generated Unique Id of this emergency
* status: if the emergency is currently active or not (on/off)

###### Example body

```json
{
  "uid": "459b5874-1ebf-11eb-9e70-4e58de281c19",
  "status": "off"
}
```

### ManagePresence

Manage a team member position

#### postPresence

* verb: POST
* endPoint: /ManagePresence/postPresence
* returns: UID

##### Parameters

* longitude: the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682)
* how: the way in which this geo information has been acquired. Please see API documentation for a list of valid entries.
* role: the given role within the team . Please see API documentation for a list of valid entries.
* name: a string to ID the GeoObject on a map.
* team: the color of the team 
* uid: optional Unique Id of this element. if present will update an existing element. use the put insted *V. 1.7 only If you send the UID an existing CLI will be updated#

###### Example body

```json
{
  "uid": "999b5874-1ebf-11zz-9e70-4e58de281c19",
  "how": "nonCoT",
  "name": "POTUS",
  "longitude": -77.01385,
  "latitude": 38.889,
  "role": "Team Member",
  "team": "Yellow"
}
```

#### putPresence

Updates the location of a team member
 * verb: PUT
 * endPoint: /ManagePresence/putPresence
 * returns: UID
 
##### Parameters

 * uid: server generated Unique Id of this emergency
   
### ManageRoute

manage routes on the map

#### postRoute

 * verb: POST
 * endpoint: /ManageRoute/postRoute
 * returns: uid
 
##### parameters

 * timeout: OPTIONAL the length, expressed in seconds until the point will stale out. Default is 300 seconds or 5 minutes.
 * address: OPTIONAL address of destination. If sent will try to solve the exact geolocation of the destination. Possible valid examples are:
     - Big Arkansas River Park, Wichita, KS, USA 
     - Wichita, KS, USA 
     - Big Arkansas River Park, Wichita
     - and so on.
 * method: OPTIONAL the method we plan to use for the route (Driving, Flying, Walking, Swimming, Watercraft). currently not used and set to Driving in the client.
 * longitudeDest: OPTIONAL if address is not sent.
 * latitudeDest: OPTIONAL if address is not sent.
 * uid: OPTIONAL server generated Unique Id of this element. it will  update the existing element.  
 * routeName:OPTIONAL the name of the route.
 * endName: OPTIONAL the name of the destination (end point on the route).
 * startName: OPTIONAL the  name of the start (start point of the route).
 * uid: OPTIONALserver generated Unique Id of this element. it will  update an existing route.  
* longitude: the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682).
 

##### Example body
```json
{
  "longitude": -77.02385,
  "latitude": 38.999,
  "routeName": "trip to Phil",
  "startName": "Washington",
  "endName": "Philadelphia",
  "timeout": 40000,
  "latitudeDest": 39.940,
  "longitudeDest": -75.01385
}
```

##### Example body 2
```json
{
  "longitude": -77.01385,
  "latitude": 38.889,
  "routeName": "trip to wichita",
  "timeout": 40000,
  "address": "Wichita, KS, USA"
}
```

##### Example body 3
```json
{
  "longitude": -77.02385,
  "latitude": 38.999,
  "routeName": "trip to halifax",
  "latitudeDest": 44.69,
  "longitudeDest": -63.57,
  "method": "Flying"
}
```
### ManageVideoStream

Manages creation of videos endpoints in the clients. The videos are visible under 'Video Player'

#### postVideoStream

 * verb: POST
 * endpoint: /ManageVideoStream/postVideoStream
 * returns: uid
 
##### parameters

* "streamAddress": the IP of the video server.
* "streamPort": the port the video server respond to.
* "streamPath": the unique path of the video stream* "alias": a name for the stream.
* "streamProtocol": the type of protocol used (e.g. rtsp, rtmp, raw).
  
###### Example body 

```json
 {
  "streamAddress": "64.227.70.77",
  "streamPort": "1935",
  "streamPath": "/LiveApp/342508189321134315564775",
  "alias": "Demo Stream From Drone ",
  "streamProtocol": "rtmp"
}
```

###### Example body 2

streamPort and streamPort params still required but will be ignored

```json
{
  "streamAddress": "rtsp://64.227.70.77:1935/LiveApp/342508189321134315564775",
  "alias": "raw Stream From Drone ",
  "streamPort": "1935",
  "streamPath": "/LiveApp/342508189321134315564775",
  "streamProtocol": "raw"
}
```

#### getVideoStream

retrieves list of stream paths

* verb: GET
* endpoint: /ManageVideoStream/getVideoStream
* returns: json with path

##### example return

``` json
{
  "video_stream": [
    "/LiveApp/342508189321134315564775",
    "/test/other"
  ]
}
```

### Sensor

since 1.9
manage sensors (name to be changed in ManageSensor)

![image](https://user-images.githubusercontent.com/60719165/123279688-78d53900-d4de-11eb-8180-054452d5539a.png)

#### postDrone

create a drone object with a field of view, a current aiming point a video stream

* verb: POST
* endpoint: /Sensor/postDrone
* returns: DRONE_UID, SPI_UID
 
##### parameters

* timeout: OPTIONAL the length, expressed in seconds until the point will stale out. Default is 300 seconds or 5 minutes.
* name: the name of the drone, will become also the name of the video stream.
* Range: the range of view of the sensor in meters.
* Bearing: the direction in which the sensor is aimed in degrees.
* FieldOfView: the field of view of the drone in degrees.
* VideoURLUID: the address of the video stream. DJI drones only support RTMP protocol. You need to have FreeTAKHub Video service active to see a stream.
* longitude: the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682).
* uid: OPTIONAL input parameter, needed to update existing drone COT.
* SPIName: the name of the Sensor Point of Interest  the UAS is currently aiming to. currently will NOT work in a update message (when you send the UID).
* SPILongitude: longitude of target. currently will NOT work in a update message (when you send the UID).
* SPILatitude: latitude of target. currently will NOT work in a update message (when you send the UID).

###### Example body: create sensor

```json
{
  "name": "Putin air",
  "Bearing": "90",
  "longitude": -77.01383,
  "latitude": 38.883,
  "FieldOfView":"20",
  "Range": "500",
  "VideoURLUID": "rtmp://64.227.50.48:1935/live/PutinAirVideo",
  "SPILongitude": -77.01393,
  "SPILatitude": 38.885,
  "SPIName": "Putin air SPI"
 }
```

###### Example body creation: update existing sensor
 
```json
{
  "uid": "d033fd0c-d5ac-11eb-ab27-4e58de281c19",
  "name": "Putin air",
  "timeout": 40000,
  "Bearing": "0",
  "longitude": -77.01399,
  "latitude": 38.889,
  "FieldOfView": "20",
  "Range": "500",
  "VideoURLUID": "rtmp://64.227.50.49:1935/live/PutinAirVideo"
}
```

#### postSPI

Creates an SPI at a point or update an existing SPI. If the video source is a UAV, and the UAV is also publishing its own position and sensor point of interest (SPI), those will  be plotted on the map. Being able to see the position of the aircraft and know where on the map the camera is looking in real time, while being able to see the video on the same screen, is a huge boost to SA.

 * verb: POST
 * endpoint: /Sensor/postSPI
 * returns: uid
 
##### parameters

* timeout: OPTIONAL the length, expressed in seconds until the point will stale out. Default is 300 seconds or 5 minutes.
* uid: OPTIONAL input parameter, needed to update existing SPI,
* longitude: the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682).
* droneUid: the uid of the connected drone.
* name: the name of the drone, will become also the name of the video stream.

###### Example Body

```json
{
  "uid": "e452b6bf-d4f0-11eb-b818-2cf05d092d98",
  "timeout": 500,
  "longitude": 4,
  "latitude": 8,
  "droneUid": "d76f608a-d4f0-11eb-b375-2cf05d092d98",
  "name": "test"
}
```

### ManageKML

allows to post a set of geo information with attached metadata in tabular format

![image](https://user-images.githubusercontent.com/60719165/125200108-d5a35400-e23f-11eb-934e-fc04210820c4.png)


#### postKML

 * verb: POST
 * endpoint: /ManageKML/postKML
 * returns: "successful" or HTTP error

##### parameters

* name: the name of the report.
* longitude: the angular distance of the geoobject from the meridian of the greenwich, UK expressed in positive or negative float. (e.g -76.107.7998). Remember to set the display of your TAK in decimal coordinates, where *West 77.08* is equal to '-77.08' in the API.
* latitude: the angular distance of the geoobject from the earths equator expressed in positive or negative float. (e.g 43.855682).
* body: a JSON structure of key pairs (name, value).

###### Example Body

```json
{
  "name": "Putin Report",
  "longitude": -77.01399,
  "latitude": 38.889,
  "body": {
    "userCallsign": "Mr Putin",
    "dateTime": "2021-07-13",
    "type": "Surveillance",
    "eventScale": "Capital",
    "importance": "Routine",
    "status": "FurtherInvestigation",
    "Time Observed": "2021-05-13T13:55:05.19Z",
    "Duration of Event": "All day",
    "Method Of Detection": "General Observation",
    "Surveillance Type": "Discreet",
    "Assessed Threats": "Threat to Mission",
    "Final Remarks": "SNAFU"
  }
}
```
