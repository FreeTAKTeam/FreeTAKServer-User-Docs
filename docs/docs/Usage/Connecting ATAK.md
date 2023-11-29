# Connecting ATAK to Pub Server
the FTS team  supports a public instance of FTS with the last version installed so that you can test it.

## Configure ATAK for FreeTakServer on the Pub server
In order to use ATAK with a FTS server you need to:
1. Download required files
2. Configure using import manager

### 1. Download required files
The easiest way  is to open this article in your Android phone, so that all the files will be already available there.

Download and install ATAK 4.2 (updated Feb 24 2021)
* Play store https://play.google.com/store/apps/details?id=com.atakmap.app.civ 
* Secondary  https://files.civtak.org/ (use CivTAK Community OwnCloud Repo) 

Download configurations
* [Configuration `fts-official-pub.zip`](fts-official-pub.zip) 
This configuration includes `fts-offical-pub.pref`:
```xml
<?xml version='1.0' standalone='yes'?>
<preferences>
    <preference version="1" name="cot_streams">
        <entry key="count" class="class java.lang.Integer">1</entry>
        <entry key="description0" class="class java.lang.String">FTS Official (Public)</entry>
        <entry key="enabled0" class="class java.lang.Boolean">true</entry>
        <entry key="connectString0" class="class java.lang.String">137.184.101.250:8087:tcp</entry>
    </preference>
    <preference version="1" name="com.atakmap.app_preferences">
        <entry key="displayServerConnectionWidget" class="class java.lang.Boolean">true</entry>
    </preference>
</preferences>
```

Download maps (optional)
* [Basic Maps `Google_Mapsources.zip`](https://bit.ly/2zSxlco)
* [Additional Maps `MOBAC-Maps-master.zip`](https://drive.google.com/file/d/1Ltdp2U7ItEu6b380u9BYswVHLSD9F-vn/view?usp=sharing)
* [Bing Maps](https://bit.ly/3gW6lcj)

### 2. Configure using import manager
* Start ATAK on android
* Tap the "..." (upper left)
* Tap "Import" manager
* Tap "Local SD"
* Go to the place where you have downloaded the files (probably `/sdcard/Download/`)
* Select `fts-official-pub.zip`
* Click `OK`
* A message will appear to inform you that you are connected to Pub Server
* Under servers the Pub Server is green (if connected)
