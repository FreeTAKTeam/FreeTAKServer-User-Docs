# setup in AWS

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
