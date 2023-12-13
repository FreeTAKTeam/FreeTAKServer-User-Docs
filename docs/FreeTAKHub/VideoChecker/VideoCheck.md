# 
The VideoChecker allows a video stream to be published to all the connected clients. It's used with TAK ICU, but any type of client can be also used.

## Requirements
- FTS 1.8+
- Video Service
- NodeRed

## Installation

- Download the `video checker`  `NodeRed` flow from [github](https://github.com/FreeTAKTeam/FreeTAKHub_VideoChecker/releases)
- open your node red installation at `<YOURIP>:1880`
- Import into NodeRed the VideoChecker flow (you may already have it installed by the [ZeroTouch](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/Installation/Ansible/ZeroTouchInstall.md) )
 ![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/9f4427c9-015f-4246-9808-4acf99f858c7)

- open the config node

![image](https://user-images.githubusercontent.com/60719165/167701401-87cb0df7-c256-4d2b-b44e-be7b1ed59e93.png)

- Set up the EXTERNAL IP of the video server 
 
![image](https://user-images.githubusercontent.com/60719165/167701322-46eb1def-cad0-48ed-9d25-872751a38bd0.png)

- in the same node set the IP of FTS (probably the same as the video Server)
- open the "Post Video to FTS" node

- ![image](https://user-images.githubusercontent.com/60719165/167701564-ab16cf03-c20a-4dfb-a05d-b283bc6d00b9.png)

- insert a valid API token

![image](https://user-images.githubusercontent.com/60719165/167701159-fb6e9998-08cf-4251-b5f4-5437832528e8.png)
