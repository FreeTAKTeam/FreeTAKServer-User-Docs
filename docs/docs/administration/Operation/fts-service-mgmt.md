
## Mange the FTS services

If the `ZTI` had run it will have attempted to start the `fts` services.
As you make changes to their configurations you will need to restart them.
```bash
sudo systemctl stop fts-ui
sudo systemctl stop fts

sudo systemctl start fts
sudo systemctl start fts-ui
```

Your `FTS` should now be running.

See [troubleshooting](../../Troubleshooting/troubleshooting_faq.md) for more information.

There are other services which `ZTI` will start.
They are also managed by `systemd`.

```bash
sudo systemctl status nodered.service
sudo systemctl status mediamtx.service
sudo systemctl status webmap.service
sudo systemctl status murmur.service
```
