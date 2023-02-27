# SSL Issue: Regenerate Certificate Revocation List
SSL stop to work after a period of time. Even restarting the server would not help. Documented under https://github.com/FreeTAKTeam/FreeTakServer/issues/368 . The cause is that  Certificate Revocation List (CRL) is expired. 
A Certificate Revocation List (CRL) is a type of security feature used in public key infrastructure (PKI) systems. It is a list of digital certificates that have been revoked by the certificate authority (CA) before their scheduled expiration date. This list contains information about the certificate serial numbers, the revocation dates, and the reason for revocation.  Since version FTS 1.9 when you delete an user that has a certificate, the certificate will be invalid.. We have now created a script that will fix the issue re-creating the CRL.
Please follow the steps below:
 1. Begin by installing DigitalPy>=0.3.9.1 (the version where CRL regeneration support was added) with the following command 
 ```
pip install DigitalPy>=0.3.9.1
```
 2. Now execute the CRL-Regen utility 
 ```
 python3 -m digitalpy.core.security.crl_regen --ca-pem-path /path/to/fts/certs/ca.pem --ca-key-path /path/to/fts/certs/ca.key --crl-path /path/to/fts/certs/FTS_CRL.json
 ```
 3. Now stop fts 
 ```
 sudo systemctl stop fts && sudo pkill python
 ```
 4. Finally restart your system for good measure (not required but recommended to ensure CRL updates are applied)
```
sudo reboot -n
```
* note: the your fts certs directory can generally be found at 
```
/usr/local/lib/python[insert your python version]/dist-packages/FreeTAKServer/certs
```

# SSL issue: Change the Number of max file open 
If you have an issue with SSL probably depends on a limited ammount of socket files you can open on the machine.
in a console type 
```ulimit -n```
If you get 1024 or less you will need to change it
The procedure on ubuntu 20.04 is this.

g.
```
sudo sed -i 's/DefaultLimitNOFILE=1024/DefaultLimitNOFILE=1048576 /g' /etc/systemd/system.conf
```
in alternative

```
grep NOFILE /etc/systemd/system.conf DefaultLimitNOFILE=1048576
```
or
open the file with an editor
```
vi /etc/systemd/system.conf
```

open the file with an editor and edit line 61
Uncomment DefaultLimitNOFILE and set your limit there, e.

Restart with reboot

type again
```ulimit -n```
Before:
```
$ ulimit -n
1024
$ ulimit -Sn
1024
$ ulimit -Hn
1024
```
After:
```
$ ulimit -n
1048576
$ ulimit -Sn
1048576
$ ulimit -Hn
1048576
```
The limits can be controlled by systemd and this is what we do here — instruct systemd to set it to 100k. 
Note that this setting will apply to all users

by increasing the soft limit for no file here
/etc/security/limits.conf

you should be able to increase this time, try 20000 and in theory the time should multiply 20x
so you should be able to run for about 40 hours uninterrupted
the file may also be under the path /etc/limits.conf
also add this line: 
```
fs.file-max = 65536
```
to this file: /etc/sysctl.conf
then restart and check file limits with this 
```
ulimit -Sn
```
