---
status: ood
---

# FTS-UI Installation with Android
FTS-UI is installed with python's pip.
One way to get pip on Android is with Pydroid3,
available here: <https://play.google.com/store/apps/details?id=ru.iiec.pydroid3>.

If you've installed Pydroid3 open the App and navigate to the terminal:
- In the upper right corner of Pydroid3, touch the 3 horizontal bars.
- Select "Terminal"
- Enter the following commands:
```
pip3 install FreeTAKServer-UI==0.1.6.5
pip3 install SQLAlchemy==1.3.23
pip3 install requests
pip3 install eventlet
pip3 show eventlet
```

After eventlet installs we need to update a file to hardcode
the tcp/udp protocol numbers due to incompatibilities with Android
- The output of `pip3 show eventlet` Location should be similar to `/data/user/0/ru.iiec.pydroid3/files/arm-linux-androideabi/lib/python3.8/site-packages`
- The file we need to update with the tcp/udp protocol numbers is located in `dns/rdtypes/IN/WKS.py`
- The full path of the file to edit using the eventlet Location output:
`/data/user/0/ru.iiec.pydroid3/files/arm-linux-androideabi/lib/python3.8/site-packages/dns/rdtypes/IN/WKS.py`

Now edit `WKS.py` and update as indicated below:

BEFORE:
```
_proto_tcp = socket.getprotobyname('tcp')
_proto_udp = socket.getprotobyname('udp')
```

AFTER: 
```
_proto_tcp = 6
_proto_udp = 17
```

FTS-UI `config.py` assumes a Linux environment,
we need to update this for Android by replacing the appropriate paths with `/sdcard` for the following:
- `SQLALCHEMY_DATABASE_URI`
- `certpath`
- If you are not running FTS and FTS-UI on the same device you will need to update `IP`
- The config file is located here: `/data/user/0/ru.iiec.pydroid3/files/arm-linux-androideabi/lib/python3.8/site-packages/FreeTAKServer-UI/config.py`

Now edit `config.py` and update as indicated below:

BEFORE:
```
# This will connect to the FTS db
SQLALCHEMY_DATABASE_URI = 'sqlite:///' + '/root/FTSDataBase.db'

# certificates path
certpath = "/usr/local/lib/python3.8/dist-packages/FreeTAKServer/certs/"
```

AFTER:
```
# This will connect to the FTS db
SQLALCHEMY_DATABASE_URI = 'sqlite:///' + r'/sdcard/FTSDataBase.db'

# certificates path
certpath = "/sdcard/FreeTAKServer/certs/"
```

# Run FTS-UI
- Make sure your FTS is already up and running.
- From the pydroid3 terminal
```
FLASK_APP=/data/user/0/ru.iiec.pydroid3/files/arm-linux-androideabi/lib/python3.8/site-packages/FreeTAKServer-UI/run.py nohup python3 /data/user/0/ru.iiec.pydroid3/files/arm-linux-androideabi/lib/python3.8/site-packages/FreeTAKServer-UI/run.py
```

Now open your web browser and navigate to <http://127.0.0.1:5000>
and login with the default creds `(admin/password)`.

# Troubleshooting

Error: `ImportError: cannot import name '_ColumnEntity' from 'sqlalchemy.orm.query'`  
Solution: You didn't downgrade SQLAlchemy correctly

Error: `Protocol not found`  
Solution: You didn't update `WKS.py` correctly

# Notes
* All testing was performed with a RaspPi4 8GB running LineageOS 18.1 32bit and Pydroid3
* These instructions assume you are running FTS and FTS-UI on the same device
* We downgrade SQLAlchemy because versions 1.4+ were not compatible with SQLAlchemy-utils
* You need root access to update the tcp/udp protocol numbers (if you are using a RaspPi4 and LineageOS it is trivial to enable)
