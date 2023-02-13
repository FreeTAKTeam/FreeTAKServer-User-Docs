# setup in AWS

* Select EC2 as the service from the AWS Console 
* Click "Launch Instance"
* Enter a name for your instance, e.g., "FreeTAK-AWS-001".
* Under the Application and OS Images menu, select Ubuntu, then from the dropdown select Ubuntu Server 20.04 LTS (HVM) SSD Volume Type

![image](https://user-images.githubusercontent.com/9298197/197416511-805196e6-09c5-4b0f-8a99-ab48b6d14328.png)


* Under instance type, select the instace type appropriate for your deployment size. For testing servers a t2.micro is sufficient.
* Under Key Pair, select a key pair in your account. If you do not have one, create one.
* Under Network Settings, select a security group that has the necessary ports configured inbound for both SSH and FreeTAK server operations.

## FTS Ports (FTSConfig.yaml) 
* 8087 - TCP COT (FTS_COT_PORT)
* 8089 - SSL COT (FTS_SSLCOT_PORT)
* 19023 - API (FTS_API_PORT)

## FTS UI Ports (config.py)
* 5000 - Web UI (APPPort)
* 1880 - Webmap (WEBMAPPORT)

## RTSP-simple-server -AKA video Server 
9997 - REST API
9998 - Metrics Listener

![image](https://user-images.githubusercontent.com/9298197/197417005-db917902-421d-4609-8786-9e0662cfadb3.png)



* Under storage configuration, for testing an 8GiB GP2 volume will be sufficient.
* Once complete, select launch instance.
* Once ready to connect to the instance, use powershell / ssh client
```
sudo apt-get update && sudo apt-get upgrade -y 
```
* now

```
sudo reboot
```

* reconnect via ssh 
```
ip a 
```

* confirm ethernet adapter name (i.e. ens33)
```
grab $[publicip] from your instance details page 
```

* add the Public IP to ethernet adapter by using the following command
```
sudo ip addr add $publicip dev $ethernetadapter
```

* run zero touch installer 
```
wget -qO - bit.ly/ftszerotouch | sudo bash
```

## Troubleshooting
If anything fails, check IP values in the following files:

### config.py
* APPIP: Internal IP 
* IP: Public IP
* WEBMAPIP: Public IP

### FTSConfig.yaml
* FTS_DP_ADDRESS: Public IP
* FTS_USER_ADDRESS: Public IP
* FTS_API_ADDRESS: 0.0.0.0
