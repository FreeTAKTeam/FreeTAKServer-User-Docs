
# Free TAK Server : core

![image](../Installation/images/zero-touch-deply-default.png)

## Zero Touch Installer 

`ZeroTouch` makes assumptions configuring the system. 
However, there are many corner cases which `ZeroTouch` may miss.
For example, `ZTI` acquires the IP address by, effectively using:
```bash
curl http://ifconfig.me/ip
```
In many environments this produces the desired result.
In cases, not on the public internet, this result will be incorrect.
The following is more likely to be what you want.
```bash
ip addr
```

Validate the properties set in the `fts-ui` configuration file.

[Verify and/or Edit the `fts` configuration file](../administration/usingConsole.md)  
```
/opt/FTSConfig.yaml
```
Here is a fragment of that configuration file.
```yaml
Addresses:
  FTS_COT_PORT: 8087
  FTS_SSLCOT_PORT: 8089
  FTS_DP_ADDRESS: 127.0.0.1
  FTS_USER_ADDRESS: 127.0.0.1
  FTS_API_PORT: 19023
  FTS_FED_PORT: 9000
  FTS_API_ADDRESS: 127.0.0.1
```
Adjust `FTS_DP_ADDRESS`, `FTS_USER_ADDRESS` & `FTS_API_ADDRESS`
to reflect your IP (or ZeroTier IP) address.

