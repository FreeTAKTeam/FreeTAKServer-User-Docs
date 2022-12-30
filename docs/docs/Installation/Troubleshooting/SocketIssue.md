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
