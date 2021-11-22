# Video Server
A the video server is a RTSP / RTPM capable software to stream in real time from / to TAK devices.
It's used with the [FreeTAK UAS](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/tools/FreeTAKUAS.md) and [TAK ICU](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/tools/takICU.md)

## Installation
get the linux_amd64 installation package link  from the [release page](https://github.com/aler9/rtsp-simple-server/releases/) 
![image](https://user-images.githubusercontent.com/60719165/142771721-3479eda5-5a0c-49a3-ba34-f0970bd4882d.png)

type in the console wget and the link
```
wget https://github.com/aler9/rtsp-simple-server/releases/download/v0.17.9/rtsp-simple-server_v0.17.9_linux_amd64.tar.gz
```

Untar the package
```
tar -zxvf rtsp-simple-server_v0.17.9_linux_amd64.tar.gz
```


Edit the YAML file
![image](https://user-images.githubusercontent.com/60719165/142767943-a3363aec-a250-4b02-9156-3b9a58627665.png)

- enable API to yes
- support protocols only TCP
- set the  API address 0.0.0.0

![image](https://user-images.githubusercontent.com/60719165/142767998-72a03e49-9055-4d4e-ac90-e8e00c51ffa9.png)

### configure to start as a service
Systemd is the service manager used by Ubuntu, Debian and many other Linux distributions, and allows to launch rtsp-simple-server on boot.

move the executable 

```
sudo mv rtsp-simple-server /usr/local/bin/
```
and configuration in the system:
```
sudo mv rtsp-simple-server.yml /usr/local/etc/
```

Create the service. copy this complete text and paste into the console:
```
sudo tee /etc/systemd/system/rtsp-simple-server.service >/dev/null << EOF
[Unit]
After=network.target
[Service]
ExecStart=/usr/local/bin/rtsp-simple-server /usr/local/etc/rtsp-simple-server.yml
[Install]
WantedBy=multi-user.target
EOF
```

Enable  the service:
```
sudo systemctl enable rtsp-simple-server
```
 start the service
```
sudo systemctl start rtsp-simple-server
```


