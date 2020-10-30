Running FreeTAKServer as a service on your linux server can be achieved multiple ways.

## Cron
Cron or Crontab is a basic scheduler that ships with most linux distributions.

We can use this to get a very basic service running with minimal effort.

### Edit Crontab
```bash
sudo crontab -e
```

Add this line to the bottom of the file

```
@reboot nohup sudo python3 -m FreeTAKServer.controllers.services.FTS &
```

You will need to add any start parameters to the crontab file such as `-DataPackageIP`.

## Systemd
WIP
