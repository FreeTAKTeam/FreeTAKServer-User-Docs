
# How to autostart the video server on the Pi

Hardware: Raspberry Pi 4b- 8g  
OS: Ubuntu Server 22.04 lts  
Program: mediamtx

When trying to accomplish Auto start on system startup/reboot, 

Solution:
For the `mediamtx.service` file, you will need to add and edit the following:
```ini
{!administration/brokered/Video/mediamtx.service!}
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
@reboot sudo systemctl enable mediamtx.service &
@reboot sudo systemctl stop mediamtx.service &
@reboot nohup sudo mediamtx.service &
```
