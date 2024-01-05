---
status: ood
---

# Video Server (third party application)


![image](../images/zero-touch-deply-default.png)

The video server is a third party application.

The video server is [Media MTX](https://github.com/bluenviron/mediamtx).

## Known Issues

The specific version verified is <https://github.com/bluenviron/mediamtx/releases/tag/v0.18.5>.
The application was rebranded in <https://github.com/bluenviron/mediamtx/releases/tag/v0.22.0>.
The reason why we use the 0.18 version is <https://github.com/bluenviron/mediamtx/issues/1790>.
This may only be a problem for `WinTAK` and not `ATAK`.


## Acquire the Appropriate Version

The release to use is <https://github.com/bluenviron/mediamtx/releases/tag/v0.18.5>.
The reason why we use the 0.18 version is
because the ability to stream videos with `winTAK` was lost in latter versions.

Different versions exist depending on the type of RaspPi you are using.
Instructions below are for RPi 4, which has an ARM64 v8 processor.

```bash
wget https://github.com/bluenviron/mediamtx/releases/download/v0.18.5/rtsp-simple-server_v0.18.5_linux_arm64v8.tar.gz
```

Extract the application into a suitable directory, e.g. `/opt`.
```bash
sudo mkdir -p /opt/mediamtx
sudo tar -zxvf rtsp-simple-server_v0.18.5_linux_arm64v8.tar.gz -C /opt/mediamtx/
```

Edit the configuration file `/opt/mediamtx/rtsp-simple-server.yml`.
The following shows the fragments of interest, before editing.
```yaml
# Enable the HTTP API.
api: no
# Address of the API listener.
apiAddress: 127.0.0.1:9997

# Encrypt handshake and TCP streams with TLS (RTSPS).
# Available values are "no", "strict", "optional".
encryption: "no"
# Address of the TCP/RTSP listener. This is needed only when encryption is "no" or "optional".
rtspAddress: :8554
# Address of the TCP/TLS/RTSPS listener. This is needed only when encryption is "strict" or "optional".
rtspsAddress: :8322
```
* Enable the HTTP API
* Set the listener's address to the RaspPi's IP address (or ZeroTier)
```yaml
# Enable the HTTP API.
api: yes
# Address of the API listener.
apiAddress: 10.2.118.237:9997

# Encrypt handshake and TCP streams with TLS (RTSPS).
# Available values are "no", "strict", "optional".
encryption: "no"
# Address of the TCP/RTSP listener. This is needed only when encryption is "no" or "optional".
rtspAddress: 10.2.118.237:8554
# Address of the TCP/TLS/RTSPS listener. This is needed only when encryption is "strict" or "optional".
rtspsAddress: :8322
```

## Smoke Test (is it running?)

* https://github.com/FreeTAKTeam/FreeTAKHub-Installation/blob/main/roles/videoserver/templates/rtsp-simple-server.service.j2

```text
{!Installation/Troubleshooting/mediamtx.service!}
```

Put the `mediamtx.service` file in `/etc/systemd/system/mediamtx.service`.
```bash
sudo systemctl daemon-reload
sudo systemctl enable mediamtx.service
sudo systemctl start mediamtx.service
```

## Integrate Media Server with Integration Server

This presumes the prior installation of [`NodeRed`](integration-server.md).

configure integration

## Connect a Client (ICU and/or drone) to Video Server

* Receive the COT notification in TAK client (`WinTAK` / `ATAK`)
* Use notification to start video (`WinTAK` / `ATAK`)

