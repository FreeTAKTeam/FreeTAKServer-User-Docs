# Configure and Connect to your cloud server
In this example we will use the provider Digital Ocean

## Creates target machines
in this example we will use Digital ocean.

1. create a DO account

![image](https://user-images.githubusercontent.com/60719165/142765115-3e2a579e-a3fe-4049-beb9-c070f7966f9c.png)

2. create a 2 new droplets

![image](https://user-images.githubusercontent.com/60719165/142765256-c03f7653-fc80-40ab-845f-304399154313.png)

4. Select Ubunbt 20.04 LTS
5. Plan basic
6. recomended the 15 $ Mo plan (it would work with the 5 $ plan but very slow). 
7. For heavy production (50-100 Concurrent users) you may want to use 8 CPUS and 32 MB RAM

![image](https://user-images.githubusercontent.com/60719165/144713041-ec46453a-09b6-4db1-81c4-7a4acc817f0d.png)

8. select the region that is the closesest to you
![image](https://user-images.githubusercontent.com/60719165/142765192-7504fcd9-790b-4c30-b7a8-c30f84488b3d.png)

9. generate a new SSH key and dowload it. It will download 2 files 1 with PEM extension and the second without extension
10.  Select project (FTYS)
11.  Press "create droplet"

### Setup you access to the VM 
- download winSCP and Putty
- open Puttygen 

#### Web
- you can use a console directly in your web browser.
- this is not the best approach for long term management but it works
- press the button
![image](https://user-images.githubusercontent.com/60719165/144713616-202b0477-4d65-463a-b74e-3afb89173499.png)
- run any command


#### SSH (Mac/Linux)
- Copy .PEM file to the machine from which you are going to connect.
- Make sure permissions on .PEM file are appropriate (chmod 600 file.pem)
- Connect with ssh command: 
```ssh vcloud@ipaddress –i privkey.pem ```

#### Putty (Windows)
- Download [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and puttygen 
- Use puttygen to convert  file without extesion to .PPK file.
- Start puttygen and select “Load”
- Select your file without extension 
- Putty will convert format to .PPK format. enter image description here
- Select “Save Private Key” A passphrase is not required but can be used if additional security is required.
- Connect with Putty.
- Launch Putty and enter the host IP address. If connecting to the 10.X private address you must first establish an SSL VPN connection.
- Navigate to Connection/SSH/Auth
- Click “Browse” and select the .PPK file you exported from puttygen. enter image description here

#### WinSCP (Windows)
WinSCP can be used on the top of Putty to make browsing and editing of files more confortable.

- Download [WInSCP](https://winscp.net/eng/download.php)
- Open WinSCP and create a new site

![image](https://user-images.githubusercontent.com/60719165/142771002-3a713b87-768c-48e8-a448-323e28e345a6.png)

![image](https://user-images.githubusercontent.com/60719165/142771008-d272d5df-3e78-4f0c-8be8-a43028414c77.png)

 ## Next step
 you can now start installing [FTS](https://freetakteam.github.io/FreeTAKServer-User-Docs/Installation/Linux/Install/)
