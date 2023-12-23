---
status: ood
---

# How to autostart the video server on the Pi

Hardware: Raspberry Pi 4b- 8g  
OS: Ubuntu Server 22.04 lts  
Program: rtsp-simple-server

When trying to accomplish Auto start on system startup/reboot, 

Solution:
For the `rtsp-simple.service` file, you will need to add and edit the following:
```ini
{!FreeTAKHub/Video/rtsp-simple.service!}
```

To build the auto start file, the Solution:
The root user is needed
```sudo -i```

Build your file:
```bash
crontab -e 
```
(if this is new, select 1 when prompted)

at the end of the file add the 3 @ lines
```
@reboot sudo systemctl enable rtsp-simple-server &
@reboot sudo systemctl stop rtsp-simple-server &
@reboot nohup sudo rtsp-simple-server &
```
