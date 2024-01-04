---
status: ood
---

# Video Server (third party application)


![image](../images/zero-touch-deply-default.png)

The video server is a third party application.

The video server is [Media MTX](https://github.com/bluenviron/mediamtx).

## Acquire the Appropriate Version

The specific version used is <https://github.com/bluenviron/mediamtx/releases/tag/v0.18.5>.
The application was rebranded in <https://github.com/bluenviron/mediamtx/releases/tag/v0.22.0>.
The reason why we use the 0.18 version is
because the ability to stream videos with `winTAK` was lost in latter versions.
Different versions exist depending on the type of RaspPi you are using.  

Instructions below are for RPi 4, which has an ARM64 v8 processor.

```bash
wget https://github.com/bluenviron/mediamtx/releases/download/v1.4.1/mediamtx_v1.4.1_linux_arm64v8.tar.gz
```

Extract the application into a suitable directory, e.g. `/opt`.
```bash
sudo tar -zxvf mediamtx_v1.4.1_linux_arm64v8.tar.gz /opt/
```

Edit the configuration file `mediamtx.yml`.

* Enable the HTTP API – api: yes
* Set the address of the API listener – apiAddress:  `<RaspPi’s IP address>:9997`
* Change `rtspAddress` to the RaspPi's IP address (or ZeroTier) – Only the line ending with port `:8554`.

