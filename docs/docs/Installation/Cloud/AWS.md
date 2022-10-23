# setup in AWS

Select EC2 as the service from the AWS Console 

Click "Launch Instance"

Enter a name for your instance, like "FreeTAK-AWS-001" 

Under the Application and OS Images menu, select Ubuntu, then from the dropdown select Ubuntu Server 20.04 LTS (HVM) SSD Volume Type

![image](https://user-images.githubusercontent.com/9298197/197416511-805196e6-09c5-4b0f-8a99-ab48b6d14328.png)


Under instance type, select the instace type appropriate for your deployment size. For testing servers a t2.micro is sufficient.

Under Key Pair, select a key pair in your account. If you do not have one, create one.

Under Network Settings, select a security group that has the necessary ports configured inbound for both SSH and FreeTAK server operations.

FTS Core Services - 
8087 - raw TCP client port
8089 - TLS client port
19023 - REST API

FTU UI -
5000 - Web UI
1880 - Web Map + Others

RTSP-simple-server - 
9997 - REST API
9998 - Metrics Listener

![image](https://user-images.githubusercontent.com/9298197/197416484-c578754d-fc4c-4bfe-98d5-4985a85d3f5a.png)


Under storage configuration, for testing an 8GiB GP2 volume will be sufficient.

Once complete, select launch instance.

* Once ready to connect to the instance, use powershell / ssh client
```
sudo apt-get update && sudo apt-get upgrade -y 
```
now
```
sudo reboot
```

reconnect via ssh 
```
ip a 
```
confirm ethernet adapter name (i.e. ens33)
```
grab $[publicip] from your instance details page 
```
add the public IP to ethernet adapter by using the following command
```
sudo ip addr add $publicip dev ens33
```
run zero touch installer 
```
wget -qO - bit.ly/ftszerotouch | sudo bash
```

## Troubleshooting
if anything failes check this
### config.py values
* APPIP - Internal IP 
* IP - Public IP
* WEBMAPIP - Public IP

### FTSConfig.yaml values
* dp_address: public 
* user address: public
* API Address: Public
