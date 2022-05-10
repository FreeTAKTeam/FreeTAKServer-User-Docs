# 
The VideoChecker allows a video stream to be published to all the connected clients. It's used with TAK ICU, but any type of client can be also used.

## Requirements
- FTS 1.8+
- Video Service
- NodeRed

## Installation

- Download the flow
- open your node red installation at <YOURIP>:8081
- Import into nodeRed the VideoChecker flow (you may already have it installed by the [ZeroTouch](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/Installation/Ansible/ZeroTouchInstall.md) )
- open the config node

![image](https://user-images.githubusercontent.com/60719165/167701401-87cb0df7-c256-4d2b-b44e-be7b1ed59e93.png)

- Setup the IP of the video server to your FTS code IP
- 
![image](https://user-images.githubusercontent.com/60719165/167701322-46eb1def-cad0-48ed-9d25-872751a38bd0.png)

- in the same node set the IP of FTS
- open the Post Video to FTS node

- ![image](https://user-images.githubusercontent.com/60719165/167701564-ab16cf03-c20a-4dfb-a05d-b283bc6d00b9.png)

- the token of the API

![image](https://user-images.githubusercontent.com/60719165/167701159-fb6e9998-08cf-4251-b5f4-5437832528e8.png)

