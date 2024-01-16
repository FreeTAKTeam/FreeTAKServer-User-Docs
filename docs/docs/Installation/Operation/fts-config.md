
## Configuration

`ZeroTouch` will have configured the system and started the services for you. 
However, there are many corner cases which `ZeroTouch` may miss.

### [Verify and/or Edit the `fts-ui` configuration file](../../administration/usingConsole.md)  
```text
/usr/local/lib/python3.11/dist-packages/FreeTAKServer-UI/config.py
```
`WEBMAPIP` is 1880 for a `NodeRedFlow` install and `8000` for a compiled `webmap`.

For specific instructions on validating the configuration,
see [these notes](../Troubleshooting/fts-ui-server.md).

### [Verify and/or Edit the `fts` configuration file](../../administration/usingConsole.md) 
```text
/opt/FTSConfig.yaml
```

For specific instructions on validating the configuration,
see [these notes](../Troubleshooting/fts-server.md).