
# Manual Configuration

### Configure FreeTAKServer

Depending on the linux distro your config file for FTS will be in a python version dependant location.
You can use pip to discover the location. Type:
```
 sudo python3 -m pip show FreeTAKServer
```

If you are running python 3.11

```text
/usr/local/lib/python3.11/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

You can edit the file via nano with the following command

```
sudo nano /usr/local/lib/python3.11/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

To exit nano `ctrl+x` and then enter `y` to save and hit enter.

#### DBFilePath
OPTIONAL this should not be necessary since FTS 1.5
you need to change the `DBFilePath` value to something valid,
if you are running as root, `/root` is a good choice.

Original Value
```python
# this should be set before startup
DBFilePath = str(r'/opt/fts/FTSDataBase.db')
```

As roots Home Folder

```python
# this should be set before startup
DBFilePath = str(r'/root/FTSDataBase.db')
```
###  MySQL database
FTS supports an abstraction layer, so it's easy to use a different database like MySQL.
MYSQL is still experimental support, so use at your own risk.
To switch to a MySQL database
```python
# this should be set before startup
DBFilePath = str('user:pass@localhost/dbname')
```

And then under
```
sudo nano /usr/local/lib/python3.11/dist-packages/FreeTAKServer/controllers/configuration/DatabaseConfiguration.py
```

Change
```python
DataBaseType = str('sqlite:///')
```
To
```python
DataBaseType = str('mysql://')
```
