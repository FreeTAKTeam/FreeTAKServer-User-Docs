### Configure FreeTAKServer < 1.9
![image](https://user-images.githubusercontent.com/60719165/124500136-9aafa500-dd95-11eb-8aa8-67ffda7076f0.png)

Depending on the linux distro your config file for FTS will be in a python version dependant location.
you can use pip to discover the location. Type:
```
 sudo python3 -m pip show FreeTAKServer
```

If you are running python 3.7 you would get
```
/usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

similarly, If you are running python 3.8

```
/usr/local/lib/python3.8/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

You can edit the file via nano with the following command

```
sudo nano /usr/local/lib/python3.7/dist-packages/FreeTAKServer/controllers/configuration/MainConfig.py
```

To exit nano `ctrl+x` and then enter `y` to save and hit enter.

#### DBFilePath
OPTIONAL this should not be necessary since FTS 1.5
you need to change the `DBFilePath` value to something valid, if you are running as root, '/root' is a good choice.

Original Value
```python
    # this should be set before startup
    DBFilePath = str(r'/opt/FTSDataBase.db')
```

As roots Home Folder

```python
    # this should be set before startup
    DBFilePath = str(r'/root/FTSDataBase.db')
