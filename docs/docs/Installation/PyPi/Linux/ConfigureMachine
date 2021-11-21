# Configure and Connect to your server
In this example we will use the provider Digital Ocean

## Creates target machines
in this example we will use Digital ocean.
1.,. create a DO accoutan
![image](https://user-images.githubusercontent.com/60719165/142765115-3e2a579e-a3fe-4049-beb9-c070f7966f9c.png)

2. create a 2 new droplets
![image](https://user-images.githubusercontent.com/60719165/142765256-c03f7653-fc80-40ab-845f-304399154313.png)

4. Select Ubunbt 20.04 LTS
5. plan basic
6. reccomended the 15 $ Mo plan (it would work with the 5 $ plan but very slow)
7. select the region that is the closesest to you
![image](https://user-images.githubusercontent.com/60719165/142765192-7504fcd9-790b-4c30-b7a8-c30f84488b3d.png)

7. generate a new SSH key and dowload it. It will download 2 files 1 with PEM extension and the second without extension
8.
9.  Select project (FTYS)
10.  press create droplet

### Setup you access to the VM 
- download winSCP and Putty
- open Puttygen 
SSH (Mac/Linux)
Copy .PEM file to the machine from which you are going to connect.
Make sure permissions on .PEM file are appropriate (chmod 600 file.pem)
Connect with ssh command: ssh vcloud@ipaddress –i privkey.pem
Putty (Windows)
Download Putty and puttygen from - here
Use puttygen to convert  file without extesion to .PPK file.
Start puttygen and select “Load”
Select your without extesion  file.
Putty will convert format to .PPK format. enter image description here
Select “Save Private Key” A passphrase is not required but can be used if additional security is required.
Open WinSCP and create a new site
![image](https://user-images.githubusercontent.com/60719165/142771002-3a713b87-768c-48e8-a448-323e28e345a6.png)

![image](https://user-images.githubusercontent.com/60719165/142771008-d272d5df-3e78-4f0c-8be8-a43028414c77.png)

Connect with Putty.

Launch Putty and enter the host IP address. If connecting to the 10.X private address you must first establish an SSL VPN connection.
Navigate to Connection/SSH/Auth
Click “Browse” and select the .PPK file you exported from puttygen. enter image description here
 
