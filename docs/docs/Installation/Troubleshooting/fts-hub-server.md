---
status: ood
---

# Integration Server


![image](../images/zero-touch-deply-default.png)

The integration server is [NodeRed]()

1. Instructions here: <https://freetakteam.github.io/FreeTAKServer-User-Docs/FreeTAKHub/Integration/NodeRedinstallation/>
2. Use command: `bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)`
   * Select `Y` to continue and `Y` to install Pi specific nodes
   * For additional settings, you can run the command: `node-red admin init`
3. Enable Node Red service:
   * Use command: sudo systemctl enable nodered.service
4. Run Node Red service:
   * Use command: sudo node-red-start
5. Login to Node Red at `<IP address>:1880`
6. Check to see if you have tabs for Webmap and FTH Video Checker Flows in Node Red
   1. If not, go to: <https://github.com/FreeTAKTeam/FreeTAKHub-Webmap/blob/main/WebMap.json>
   2. Click the copy button on the right side of the line to copy the raw contents of WebMap.json to your clipboard
   3. Go back to your Node Red and click the Hamburger menu icon (right upper corner) and select Import
   4. Paste the raw contents here and click import
   5. If you get an error about missing “world map, world map in & config”
      1. Click Hamburger menu and select Manage palette
      2. Select install and search for “node-red-contrib-web-worldmap” and click install
      3. Click back in search field and search for “node-red-contrib-config” and click install
7. In Node Red WebMap flow tab:
8. Select the FTH Global Config node and update the FTH_FTS_URL and FTH_FTS_VIDEO_URL fields with your IP (or ZeroTier) address 
   * Select the Post CoT to FTS node and update the “bearer authentication” Token field with ‘<Your_Bearer_Token>’
9. Click DEPLOY in upper right corner of Node Red to save settings
10. You should now get green “connected” indicators under one or all these nodes: FTS Server, TAK Map, tak-map & event
11. Confirm that the flow is working by logging back into the FTS Web UI: `<IP address>:5000` and click on the WebMap tab.
    Now you should see the world map displayed

