# Ansible

Ansible is an Infrastructure-As-Code tool used for managing and monitoring remote FTS related servers.

## PRE-INSTALLATION STEPS: Windows

Currently FreeTAKServer and components have been tested successfully on Ubuntu 20.04.

Other Linux distributions may work, but they have not been tested.

To install on Windows, you will have to:

1. Install WSL2.

    See: <https://docs.microsoft.com/en-us/windows/wsl/install>

    See also: <https://www.omgubuntu.co.uk/how-to-install-wsl2-on-windows-10>

    See also: https://www.sitepoint.com/wsl2/

2. Install the WSL Ubuntu 20.04 distribution.

    See: <https://www.microsoft.com/en-us/p/ubuntu-2004-lts/9n6svws3rx71>

### Step 1. Install Ansible and package dependencies

In the Ubuntu console:

```console
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible git
```

See: <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu>

### Step 2. Clone the FreeTAKHub-Installation Git repository

```console
git clone https://github.com/FreeTAKTeam/FreeTAKHub-Installation.git
```

### Step 3. Install with Ansible

An example default install playbook is defined in: `freetakhub_install.yml`.

This playbook installs all FreeTAKServer and components to your machine.

To execute the default install playbook, from the top directory, enter:

```console
sudo ansible-playbook freetakhub_install.yml
```

# Uninstall

An example default uninstall playbook is defined in: `freetakhub_uninstall.yml`.

The playbook uninstalls all FreeTAKServer and components on your machine.

To execute the default uninstall playbook, from the top directory, enter:

```console
sudo ansible-playbook freetakhub_uninstall.yml
```


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


# Clone the repository locally
* install tortoiseSVN (or anything equivalent)
* clone the repository
```
https://github.com/FreeTAKTeam/FreeTAKHub-Installation
```

![image](https://user-images.githubusercontent.com/60719165/147416679-013d818e-2ad2-405c-ae9d-cd996fcca478.png)
