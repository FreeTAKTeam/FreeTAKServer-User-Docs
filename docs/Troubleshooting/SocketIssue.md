
# SSL Issue: Regenerate Certificate Revocation List
Currently, there is a known issue of a socket leak, causing SSL to stop working after a period of time.
Even restarting the server OS would not help,
documented under: <https://github.com/FreeTAKTeam/FreeTakServer/issues/368>

The cause is that  Certificate Revocation List (CRL) is expired.
A Certificate Revocation List (CRL) is a type of security feature used in public key infrastructure (PKI) systems.
It is a list of digital certificates that have been revoked by the certificate authority (CA) before their scheduled expiration date.
This list contains information about the certificate serial numbers, the revocation dates, and the reason for revocation.
Since FTS version 1.9, when you delete a user that has a certificate, the certificate will be revoked.
We have now created a script that will fix the issue re-creating the CRL.

Please follow the steps below.

!!! note
    If you are trying to use this with 2.x.y the first step is not necessary

1. Install DigitalPy>=0.3.9.1 (the version where CRL regeneration support was added) with the following command:
    ```shell
    pip install DigitalPy>=0.3.9.1
    ```
2. Now execute the CRL-Regen utility. The location of the certs would under /path/to/fts/certs/ca.pem typically would be /opt/fts/certs:
    ```shell
     python3 -m digitalpy.core.security.crl_regen --ca-pem-path /opt/fts/certs/ca.pem --ca-key-path /opt/fts/certs/ca.key --crl-path /opt/fts/certs/FTS_CRL.json
    ```
3. Now stop FTS:
    ```shell
     sudo systemctl stop fts && sudo pkill python
    ```
4. Finally, restart your system for good measure (not required but recommended to ensure CRL updates are applied)
```shell
sudo reboot -n
```

!!! note
    The FTS certs directory can generally be found at
    ```shell
    /root/fts.venv/lib/python3.11/site-packages/FreeTAKServer/certs
    ```

# SSL issue: Change the Number of max file open
If you have an issue with SSL probably depends on a limited amount of socket files you can open on the machine.
in a console type

```bash
ulimit -n
```
If you get 1024 or less you will need to increase the allowed file descriptors for the user.

The procedure on Ubuntu 20.04 and 22.04 is this:

```bash
sudo sed -i 's/DefaultLimitNOFILE=1024/DefaultLimitNOFILE=1048576 /g' /etc/systemd/system.conf
```


```bash
grep NOFILE /etc/systemd/system.conf DefaultLimitNOFILE=1048576
```
or
open the file with an editor
```bash
vi /etc/systemd/system.conf
```

open the file with an editor and edit line 61
Uncomment DefaultLimitNOFILE and set your limit there, e.

Restart with:

```bash
shutdown -r 0
```
Then, check the user file descriptor limit again:

```bash
ulimit -n
```

Before:

```bash
ulimit -n
ulimit -Sn
ulimit -Hn
```
```text
1024
1024
1024
```

After:

```bash
ulimit -n
ulimit -Sn
ulimit -Hn
```
```text
1048576
1048576
1048576
```

The limits can be controlled by systemd and this is what we do here 
— instruct systemd to set it to 100k.
Note that this setting will apply to all users

by increasing the soft limit for no file here
`/etc/security/limits.conf`

you should be able to increase this time, 
try 20000 and in theory the time should multiply 20x.
so, you should be able to run for about 40 hours uninterrupted
the file may also be under the path `/etc/limits.conf`
also add this line:

```text
fs.file-max = 65536
```
to this file: `/etc/sysctl.conf`
then restart and check file limits with this

```bash
ulimit -Sn
```
