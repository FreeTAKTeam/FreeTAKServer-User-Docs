---
status: ood
---

# CLI

## Availability

The CLI has been sunset since version 1.5 of FTS, because of the new way to access the server.

It may be reintroduced in the future.

## Access

To access the CLI open a new terminal and run the command:

```console
sudo python3 -m FreeTAKServer.views.CLI
```

## Commands

| Command                    | Purpose                                                        |
|----------------------------|----------------------------------------------------------------|
| help                       | List all commands                                              |
| start_all                  | Begin all services type                                        |
| start_CoT_service          | Begin CoT service type                                         |
| start_data_package_service | Begin data package service type                                |
| stop_all                   | Terminate all services type                                    |
| stop_CoT_service           | Terminate CoT service type                                     |
| stop_data_package_service  | Terminate data package service type                            |
| change_connection_info     | Change the address and port of the server you're connecting to |
| show_users                 | Show connected user information type                           |
| kill                       | Kill the full server type                                      |
| show_DP                    | Show all DataPackages on the server                            |
| remove_DP                  | Remove a DataPackages on the server                            |
| add_api_user               | add a user and a token for API consumption                     |
| show_api_users             | show a list of users and their tokens                          |
| remove_api_user            | remove a user and a token for API consumption                  |

