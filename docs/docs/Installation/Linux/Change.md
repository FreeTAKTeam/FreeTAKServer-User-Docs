The procedure changed on recent ubuntu compared to what I used to do. I used change /etc/security/limits.conf.

The procedure on ubuntu 18.10 that worked for me is this.

Go to /etc/systemd/system.conf
Uncomment DefaultLimitNOFILE and set your limit there, e.g.
``
$ grep NOFILE /etc/systemd/system.conf
DefaultLimitNOFILE=1048576
```
Restart
Profit
Before:
```
$ ulimit -n
1024
$ ulimit -Sn
1024
$ ulimit -Hn
1048576
```
After:
```
$ ulimit -n
65535
$ ulimit -Sn
65535
$ ulimit -Hn
65535
```
The limits can be controlled by systemd and this is what we do here — instruct systemd to set it to 100k. 
Note that this setting will apply to all users
