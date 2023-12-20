# Connecting `WinTAK` to Pub Server
The FTS team supports a public instance of FTS with the last version installed so that you can test it.


## Issues

`WinTAK` has a known issue with the TAK Chat Plugin.
You Must disable the plugin,
or you will have frequent disconnects from FTS.

### Disable TAK Chat
Navigate to the plugin management menu.

![`WinTAK` Plugin Manager](images/wintak_menu_main.png)

Then select unload on `TAK Chat`

## Connect to FTS

Navigation:  
`Settings`

![`WinTAK` Menu Main Select Settings](images/wintak_menu_main_select_settings.png)

&rarr; `Network Preferences` 

![`WinTAK` Dialog Main Settings](images/wintak_dialog_main_settings.png)

&rarr; `Mange Server Connections`

![`WinTAK` Dialog Network Prefs](images/wintak_dialog_network_prefs.png)

&rarr; `FTS Public 2.1`
From here you can add your FTS server: 
Description; IP or host name, and; port.

![`WinTAK` Dialog Server Connect](images/wintak_dialog_server_connect.png)

&rarr; `Ok` If the connection is made you will see it reflected in the `TAK Network Status`.

![`WinTAK` Dialog Server Connected](images/wintak_dialog_server_connected.png)

## Connect to FTS via Configuration File

![`WinTAK` Menu Main Import](images/wintak_menu_main_import.png)

This will bring up a file selection dialog. 

* [Configuration `fts-official-pub.zip`](../assets/fts-official-pub.zip) 

Note: This reads the file, but it does not seem to update the server connections.
