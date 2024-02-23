---
status: ood
---

# Connecting `ATAK` to Pub Server
The FTS team supports a public instance of FTS with the last version installed so that you can test it.

## Configure `ATAK` for FreeTakServer on the Pub server
In order to use `ATAK` with a FTS server you need to:
1. Download required files
2. Configure using import manager

### 1. Download required files
The easiest way  is to open this article in your Android phone, so that all the files will be already available there.

#### Download and install `ATAK` 4.10 (updated Nov 2023)
* Play store <https://play.google.com/store/apps/details?id=com.atakmap.app.civ> 
* Secondary  <https://files.civtak.org/> (use CivTAK Community OwnCloud Repo) 

#### Download configurations
* [Configuration `fts-official-pub.zip`](../assets/fts-official-pub.zip) 
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

#### Download maps (optional)
There are places where you may acquire `ATAK` maps.
Representative place are: 

* [ATAK-Maps](https://github.com/joshuafuller/ATAK-Maps)
* [reddit `ATAK` MapSources](https://www.reddit.com/r/ATAK/wiki/index/#wiki_loading_mapsources_.2F_base_maps_to_tak)
* [CivTAK Files](https://www.civtak.org/files/)
* [Roll Your Own with MOBAC](https://mobac.sourceforge.io/)


### 2. Configure using import manager

Navigation:

* Start `ATAK` on android
* Tap the menu selector, i.e. &equiv;, (upper left).

&rarr; Tap `Import` manager

![`ATAK` Menu Main Select Settings](images/atak_menu_main_import.png)

&rarr; Tap `Local SD`

![`ATAK` Dialog Import Type](images/atak_dialog_import_type.png)

&rarr;  Go to the place where you have downloaded the files (probably `/sdcard/Download/`)

![`ATAK` Dialog Select Import](images/atak_dialog_select_import.png)

* Select `fts-official-pub.zip`
* Click `OK`

* A message will appear to inform you that you are connected to Pub Server
* Under servers the Pub Server is green (if connected)
