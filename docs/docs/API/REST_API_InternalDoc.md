# REST API - Internal
Internal APIs are primarly used by the FTS UI to communicate with the server. 
See also the [REST API DOC](REST_API_Doc.md) for APIs used in integration
they may be used to create other user interfaces such as CLI.

In the current release (1.9), FTS supports following Internal API :

  * authenticate
  * users
  * logs
  * serviceInfo
  * serverHealth
  * systemStatus
  * DataPackageTable
  * MissionTable
  * ExCheck
  * Federation

there are two types of Internal API:
- Websocket, using socketIO
- REST

## Websocket, using SocketIO
FTS uses **SocketIO** for the communication, ensure that you understand SocketIO concepts:

- Emits: those are events sent from/to the client with requests
- Listener: are events that client/server can subscribe to


## Authorization Websocket
to use websocket events you need to trigger the event 'authenticate' after connection and pass
as the body of the message ```{"Authenticate": [YOUR WEBSOCKET KEY]}```

# Connect

## description
event triggered on initial connection to server<br />
Event: `connect` (this is a special event as it is called automatically on connection)<br />
Subscription: `connectUpdate`

## returns
```json
{
"starttime": "", 
"version": "" 
}
```
- "starttime": the time at which server was started
- "version":   the version of FTS currently running

# Authenticate

## description
  event used to authenticate new clients in the websocket<br />
  Event: `authenticate` <br />
  Subscription: `authentication`
  
## returns
  will call the event authentication on client with message body
```{'successful': 'True'/'False'}``` depending on whether the authentication was accepted.

## parameters
a JSON body in the following format
```json
{"Authorization": ["YOUR WEBSOCKET KEY"]}
```
# Users
## description
event used to access list of connected client aswell as data
relating to each client.<br />
 Event: `users` <br />
 Subscription: `userUpdate`

## returns
a JSON message containing connected clients
```json
{
  "Users":[
    "user:", {"ip": "24.114.74.13", "callsign": "CorvoMobile", "team": "Yellow"},
    "user:", {"ip": "24.144.79.13", "callsign": "Ghost", "team": "Blue"}
  ]
}
```
## parameters
None

# Manage System users
## systemUser
retrieve all system users and their associated information<br />
Event: `systemUser` <br />
Subscription: `systemUserUpdate`
 
### returns
system user information
```json
{
	"systemUsers": [
		  {"Name": "Dan", "Group": "Yellow", "Token": "", "Password": "", "Certs": "a.zip", "Uid": ""},
		  {"Name": "Joe", "Group": "Yellow", "Token": "", "Password": "", "Certs": "b.zip", "Uid": ""},
		  {"Name": "Bill", "Group": "Yellow", "Token": "", "Password": "", "Certs": "c.zip", "Uid": ""}
	]
}
```

### parameters
None

## addSystemUser
### description
add one or many system users to the server<br />
Event: `addSystemUser`

### returns
None

### parameters
```json
{
	"systemUsers": [
		  {"Name": "Dan", "Group": "Yellow", "Token": "", "Password": "", "Certs": "true"},
		  {"Name": "Joe", "Group": "Blue", "Token": "", "Password": "", "Certs": "true"},
		  {"Name": "Bill", "Group": "Red", "Token": "", "Password": "", "Certs": "true"}
	]
}
```

## removeSystemUser
### description
remove a system user from the server<br />
Event: `removeSystemUser`

### returns
None

### parameters
```json
{
  "systemUsers": [
    {"uid": "[uid of system user to be deleted]"},
    {"uid": "[uid of system user to be deleted]"},
    {"uid": "[uid of system user to be deleted]"}
  ]
}
```
## logs
### description
event used to retrieve recent error log entries
from the server<br />
Event: `logs` <br />
Subscription: `logUpdate`

### returns
recent error logs in JSON to the client event `logUpdate` with data in the following format
```json
{
  "log_data": [
    {"time": "2020-12-16 21:15:14,618", "type": "ERROR", "file":"TCPCoTServiceController.py:31", "message": "there has been an exception in Data Package service startup maximum recursion depth exceeded while calling a Python object"}
  ]
}
```

### parameters
the timestamp on the most recent log entry in format `%Y-%m-%d %H:%M:%S,%f`

## events
### description
event used to retrieve last 5 events<br />
Event: `events` <br />
Subscription: `eventsUpdate`

### returns
```json
{
  "events": ["server event 1", "server event 2", "server event 3", "server event 4", "server event 5"]
}
```
 
### parameters
None

# serviceInfo
## description
event used to retrieve information about all services including
their current status and port<br />
Event: `serviceInfo` <br />
Subscription: `serviceInfoUpdate`

## returns
status and port of each service aswell as the server starttime to the client event `serviceInfoUpdate`
with body data in the following format
```json
{
    "services": {
        "SSL_CoT_service": {
                      "status": "on",
                      "port": 11111
                  },
        "TCP_CoT_service": {
                      "status": "off",
                      "port": 55555
                  },
        "SSL_DataPackage_service": {
                      "status": "on",
                      "port": 52345
                  },
        "TCP_DataPackage_service": {
                      "status": "on",
                      "port": 55235
                  },
        "Federation_server_service": {
                      "status": "on",
                      "port": 55235
                  },
        "Rest_API_service": {
                      "status": "on",
                      "port": 55235
                  }
    },
    "IP": "127.0.0.1"
}
```
## parameters
None

# serverHealth
## description
event used to retrieve information regarding
the status of the server hardware including
cpu, disk and memory usage.<br />
Event: `serverHealth` <br />
Subscription: `serverHealthUpdate`

## returns
current hardware usage to the client event `serverHealthUpdate` with body

```json
{
    "CPU": 56,
    "memory": 39,
    "disk": 94
}
```

## parameters
None
 
# systemStatus
## description
event used to execute test of all currently active
services and return their respective status.<br />
  Event: `systemStatus` <br />
  Subscription: `systemStatusUpdate`

## returns
current and expected status of all services on the server in JSON format 
to the event `systemStatusUpdate` on the client with the body of the message 
in the following format

```json
{
  "services": {
      "SSL_CoT_service": {
          "status_expected": "on",
          "status_actual": "off"
      },
      "TCP_CoT_service": {
          "status_expected": "on",
          "satus_actual": "on"
      },
      "SSL_DataPackage_service": {
          "status_expected": "on",
          "status_actual": "on"
      },
      "TCP_DataPackage_service": {
          "status_expected": "on",
          "status_actual": "on"
      },
      "SSL_Federation_service": {
          "status_expected": "off",
          "status_actual": "off"
      },
      "TCP_API_service": {
          "status_expected": "on",
          "status_actual": "on"
      }
  }
}
```

## parameters
None
 
# changeServiceInfo

## description
Event used to change the status of each service running on the server<br />
Event: `changeServiceInfo` <br />
Subscription: `systemStatusUpdate`
 
## returns
```json
{
"services": {
    "SSL_CoT_service": {
                  "status": "on",
                  "port": 11111
              },
    "TCP_CoT_service": {
                  "status": "off",
                  "port": 55555
              },
    "SSL_DataPackage_service": {
                  "status": "on",
                  "port": 52345
              },
    "TCP_DataPackage_service": {
                  "status": "on",
                  "port": 55235
              }
},
"ip": "127.0.0.1"
}
```

## parameters
accepts JSON data containing information regarding the desired status of each service in the following format
```json
{
  "services": {
      "SSL_CoT_service": {
                    "status": "on",
                    "port": 11111
                },
      "TCP_CoT_service": {
                    "status": "off",
                    "port": 55555
                },
      "SSL_DataPackage_service": {
                    "status": "on",
                    "port": 52345
                },
      "TCP_DataPackage_service": {
                    "status": "on",
                    "port": 55235
                }
  },
  "ip": "127.0.0.1"
}
```

`ip`: ip on which the server should be listening eg: `0.0.0.0`<br/>
`status`: whether the service is to be started or stopped eg: `on`, `off` <br />
`port`(optional): the port on which the service should be listening eg: `8089` <br />
not all services need to be in every message only those you would like to change
 
# systemUsers
Event used to retrieve all system users<br />
  Event: `systemUsers` <br />
  Subscription: `systemUsersUpdate`
  
## returns
the metadata of each user
```json
{
  "systemUsers":[
    {"Name": "Dan", "Group": "Yellow", "Token": "Token1", "Password": "psw1", "Certs": "a.zip"},
    {"Name": "Joe", "Group": "Yellow", "Token": "Token1", "Password": "psw1", "Certs": "a.zip"},
    {"Name": "Bill", "Group": "Yellow", "Token": "Token1", "Password": "psw1", "Certs": "a.zip"}
  ]
}
```

## parameters
None

# addSystemUsers
used to create a new system user on the server<br />
Event: `addSystemUsers` <br />

## returns
None

## parameters
```json
{
  "systemUsers":[
    {"Name":"dan", "Group":"Yellow", "Token":"token", "Password": "psw1", "Certs":"true" }
	]
}
```

* Name: name of user
* Group: group of user
* Token: api token of user(optional)
* Password: password for user(optional)
* Certs: whether the user should have certs generated(should be true in ui)

## removeSystemUsers
used to remove a system user and their associated files from the server<br />
Event: `removeSystemUsers` <br />

### returns
None

### parameters
```json
{ "systemUsers": 
  [ 
    { "uid": "46b3de87-85f5-400d-a098-536f2e1421ce" } 
  ] 
}
```

* uid: uid of user to remove


# REST Services

## Authorization: API
to use the REST API you need to have a REST API key.
the authorization is placed in the header of the message.
Authorization: Bearer [YOUR_API_KEY]

> you need to use the string 'Bearer' before your API KEY

# ManageSystemUser
### nested resources
* postSystemUser
* deleteSystemUser   
* putSystemUser

## postSystemUser
used to create a new system user on the server

### methods
```POST```
### returns
`user created`  
code: `201`

### body
```json
{
  "systemUsers":[
    {"Name":"dan", "Group":"Yellow", "Token":"token", "Password": "psw1", "Certs":"true", "DeviceType": "mobile" }
  ]
}
```

* Name: name of user
* Group: group of user
* DeviceType: the device type [mobile, wintak]
* Token: api token of user(optional)
* Password: password for user(optional)
* Certs: whether the user should have certs generated(should be true in ui)

## deleteSystemUser
used to remove a system user and their associated files from the server as well as revoking the users certificate

### methods
```DELETE```
### returns
`user deleted`  
code: `200`

### body
```json
{ "systemUsers": 
  [ 
    { "uid": "46b3de87-85f5-400d-a098-536f2e1421ce" } 
  ] 
}
```

* uid: uid of user to remove

## putSystemUser
update an existing system user
### methods
```PUT```
### returns
`user updated`  
code: `200`

```json
{"systemUsers": [
		{"uid": "existing user id", "password": "new user password", "token": "new user token", "group": "new user group"}
	]
}
```
* uid: uid of the user
* Group: new user group (optional)
* Token: new api token of user(optional)
* Password: new password for user(optional)
# DataPackageTable
## description
Endpoint used to access data regarding DataPackages

### methods
* POST
* GET
* DELETE   

## GET
returns JSON data containing information regarding all DataPackages currently on server
```json
{
  "DataPackages":[
    {"Keywords": "88.104.44.76", "name": "WWIII Locations","privacy":"public", "size":"345KB", "submitted":"2020-02-10" },
    {"Keywords": "112.144.567.257", "name": "WWIII Locations","privacy":"public", "size":"345KB", "submitted":"2020-02-10" }
  ]
}
```

## POST
accepts the zipped form of the file in the body of the message and the following arguments in the url
* filename: the name of the zipped file
* creatorUid(optional): the uid of the user associated with the DataPackage defaults to ```server``` if none is provided
  
## DELETE
accepts the following JSON data
```json
{
  "DataPackages":[
    {"hash": "194728885783f87ws84888943fjew"},
    {"hash": "19472mw45783f7ws848758943fjegr"}
  ]
}
```
the hash values are the hashes of DataPackages to be deleted

## PUT
accepts the following JSON data
```json
{
  "DataPackages":[
    {"PrimaryKey": "1", "Name": "new_name", "Keywords": "new keywords", "Privacy": "0"}
  ]
}
```
* PrimaryKey: primary key of DataPackage to be modified
* Name: optional new name of DataPackage if not set name will not be changed
* Keywords: optional new keywords of DataPackage if not set keywords will not be changed
* Privacy: optional new privacy of DataPackage if not set privacy will not be changed must be 1(Private) or 0(Public)

# MissionTable
## description 
Endpoint used to access data regarding mission packages

## methods
* GET
* POST
* DELETE

## GET
return JSON data containing information about all current Missions
with the following format
```json
{
    "version": "3",
    "type": "Mission",
    "data": [{
            "name": "save the world",
            "description": "Protect the world from Aliens",
            "chatRoom": "",
            "tool": "public",
            "keywords": ["War"],
            "creatorUid": "Anonymous",
            "createTime": "2020-12-09T15:53:42.873Z",
            "groups": ["__ANON__"],
            "externalData": [],
            "uids": [{
                    "data": "32e9089c-6ae0-4c7e-b4cd-cb16d3f46933",
                    "timestamp": "2020-12-09T15:58:10.635Z",
                    "creatorUid": "aa0b0312-b5cd-4c2c-bbbc-9c4c70216261",
                    "details": {
                        "type": "a-h-G",
                        "callsign": "R.9.155734",
                        "iconsetPath": "COT_MAPPING_2525B/a-h/a-h-G"
                    }
                }
            ],
            "contents": [{
                    "data": {
                        "filename": "Sout",
                        "keywords": [],
                        "mimeType": "application/octet-stream",
                        "name": "SWN Threat",
                        "submissionTime": "2020-12-09T15:55:21.468Z",
                        "submitter": "anonymous",
                        "uid": "3ec22850-d6de-44a5-b79c-3af16695af60",
                        "hash": "8a99e610d223426caaf267f12c3100513bbb62a66d07c5feb624d4cf5b90b69b",
                        "size": 18360
                    },
                    "timestamp": "2020-12-09T15:55:21.559Z",
                    "creatorUid": "Anonymous"
                }
            ],
            "passwordProtected": false
        }
    ],
    "nodeId": "6ff99444fa124679a3943ee90308a44c9d794c02-e5a5-42b5-b4c8-625203ea1287"
}
```
## POST
not yet implemented

## DELETE
not yet implemented

# ExCheckTable
Endpoint used to access data regarding ExCheck items such as checklists and templates

## POST
creates a template on the server from a supplied xml file accepting the following URL encoded values:
* clientUid: the uid of the client to be recognized as the creator of the template

body of the message should be the xml of the template

## DELETE
accepts the following data
```json
{
  "ExCheck": 
  {
    "Templates": [{"uid": "TemplateUID1"}, {"uid": "TemplateUID2"}],
    "Checklists": [{"uid": "ChecklistUID1"}, {"uid": "ChecklistUID2"}]  
  }
}
```
`uid`: the uid of those Checklists and Templates to be deleted

## GET
return JSON data containing the following information about Checklists and Templates present on the server
```json
{
  "ExCheck": {
    "Templates": [
      {
        "filename": "cdd39d06-b43e-42f4-839d-32362febe9a1.xml", 
        "name": "test from atak",
        "submissionTime": "2020-12-22T22:07:31.749284Z", 
        "submitter": "[('NOVA',)]", 
        "uid": "cdd39d06-b43e-42f4-839d-32362febe9a1", 
        "hash": "bfb97ed985f789b0c97cf3a93a4354e36eadadd0b6d156c4e4a5ad25330a8c45", 
        "size": 1735, 
        "description": "test from atak desc" 
      }
    ],
    "Checklists": [
      {
        "filename": "c5322e53-5b95-4def-953d-6be9e42e79fd.xml", 
        "name": "test from atak", 
        "startTime": "2020-12-22T22:07:32.841000Z", 
        "submitter": "NOVA", 
        "uid": "c5322e53-5b95-4def-953d-6be9e42e79fd", 
        "description": "test from atak desc",
        "template":"cdd39d06-b43e-42f4-839d-32362febe9a1" 
      }
    ]
  }
}
```
### Templates
* "filename":  name of file containing template xml
* "name":  name associated with template
*  "submissionTime":  time template was submitted to server
* "submitter":  callsign of submitter
* "uid": uid of template
*  hash": hash of template
* "size": size of template in bytes
*  "description":  description of template

### Checklists 
* "filename":  name of file containing checklist xml
* "name": name associated with template
*  "startTime": time checklist was created
* "submitter": callsign of user to submit checklist
* "uid": uid of checklist
* "description": "description of checklist
*  "template":"uid of template of which the checklist is an instance


# FederationTable
endpoint used to access federation objects

## GET
return JSON data containing the following information regarding current checklists and templates present on the server
```json
{
"activeFederations":
	[
        {
            "id": "111-111-111",
            "address": "127.0.0.1",
            "port": "9000",
            "initiator": "Self",
            "readCount": "0",
            "processedCount": "0"
        },
        {
            "id": "111-111-112",
            "address": "1.1.1.1",
            "port": "11111",
            "initiator": "Remote",
            "readCount": "0",
            "processedCount": "0"
        }
    ],
"federations": 
  [
    {
      	"name": "federation 1",
		"id": "111-111-111",
		"address": "127.0.0.1",
		"port": "9000",
		"fallBack": "federation 2",
		"status": "Disabled",
		"reconnectInterval": "32",
		"maxRetries": "15",
		"lastError": "Timeout"
    }
  ]
}
```

## POST
create a new federation configuration
```json
{
"outgoingFederations":
    [
      {
      	"name": "federation 1",
		"address": "127.0.0.1",
		"port": "9000",
		"fallBack": "federation 2",
		"status": "Disabled",
		"reconnectInterval": "32",
		"maxRetries": "15"
	  }
    ]
}
```

## DELETE
delete an existing federation configuration
```json
{
  "federations": 
    [
      {
        "id": "111-111-111"
      }
    ]
}
```

## PUT
modify an existing federation configuration
```json
{
  "federations": 
    [
      {
        "id": "111-111-111",
        "name": "new federation 1",
        "fallBack": "new fallback",
        "status": "Enabled",
        "reconnectInterval": "15",
        "maxRetries": "10"
      } 
    ]
}
```

* id: must be id of existing federation configuration
* name(optional): new name of federation configuration
* fallback(optional): name of new fallback
* status(optional): new status of connection
* reconnectInterval(optional): new reconnect interval
* maxRetries(optional): new maximum number of retries
