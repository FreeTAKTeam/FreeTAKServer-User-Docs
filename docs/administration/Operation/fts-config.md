
## Configuration

`ZeroTouch` will have configured the system and started the services for you. 
However, there are many corner cases which `ZeroTouch` may miss.

### [Verify and/or Edit the `fts-ui` configuration file](../usingConsole.md)  
```text
/opt/fts.venv/lib/python3.11/site-packages/FreeTAKServer-UI/config.py
or
/usr/local/lib/python3.11/dist-packages/FreeTAKServer-UI/config.py
```
`WEBMAPPORT` is 1880 for a `NodeRedFlow` install and `8000` for a compiled `webmap`.

For specific instructions on validating the configuration,
see [these notes](../../Troubleshooting/fts-ui-server.md).

### [Verify and/or Edit the `fts` configuration file](../usingConsole.md) 
```text
/opt/fts/FTSConfig.yaml
```

For specific instructions on validating the configuration,
see [these notes](../../Troubleshooting/fts-server.md).