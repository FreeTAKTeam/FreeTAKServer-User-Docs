If you have not installed FreeTAKServer please follow the installation guide first.

## Parameters

| Flag             | Description                                                              |
|------------------|--------------------------------------------------------------------------|
| -AutoStart       | Weather the full server start or just the RestAPI, must be True or False |
| -CoTIP           | Your Server IP                                                           |
| -DataPackageIP   | The IP where CoTs are send                                               |
| -CoTPort         | The port you want clients to connect to                                  |
| -DataPackagePort | The port you want Data Packages to be sent and received on                |

## Run FTS in the Console

```bash
sudo python3 -m FreeTAKServer.controllers.services.FTS -DataPackageIP 0.0.0.0 -AutoStart True
```

If you have FTS running in the terminal how you would like it's time to move on to running FTS as a service.
