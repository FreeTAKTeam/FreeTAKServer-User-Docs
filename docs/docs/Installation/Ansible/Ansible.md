# Ansible 
Ansible is an Infrastructure as Code tool used for managing and monitoring remote FTS related servers.

## Windows installation
you can install ansible under windows 10

### Prerequisites

* A system running Windows 10
* A user account with administrator privileges


* Open the Start menu and search for 
```
Turn Windows features on or off
```
and select "Windows Subsystem for Linux" 
![image](https://user-images.githubusercontent.com/60719165/147415385-e0a9fa0b-2223-4651-ba3a-066f122fdada.png)

* restart your machine
* go to the windows store
* search for Ubuntu 20.04 LTS
* Press "Get"
* Click "Open"
* decide an user name and password
![image](https://user-images.githubusercontent.com/60719165/147415590-3897963b-839a-4f84-95e2-6566d001def4.png)

* types the following
```
sudo apt-get update
```

```
sudo apt-get install software-properties-common
```

```
sudo apt-add-repository ppa:ansible/ansible
```

```
sudo apt-get update
```

```
sudo apt-get install ansible -y
```
the step 'unpaking ansible' will take a while, be patient.
