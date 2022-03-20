# Ansible Manual Install

Ansible is an Infrastructure-As-Code tool used for managing and monitoring remote FTS related servers.

# FreeTAKHub Installation

FreeTAKHub installation is a set of Ansible/Terraform scripts that allow you to:

- create the target nodes
- install FTS and all the additional modules
- configure FTS

# Windows Prerequisites

Currently FreeTAKServer and components have been tested successfully on Ubuntu 20.04.

Other Linux distributions may work, but they have not been tested.

To install on Windows, you will have to:

1. Install WSL2.

    See: <https://docs.microsoft.com/en-us/windows/wsl/install>

    See also: <https://www.omgubuntu.co.uk/how-to-install-wsl2-on-windows-10>

    See also: <https://www.sitepoint.com/wsl2/>

1. Install the WSL Ubuntu 20.04 distribution.

    See: <https://www.microsoft.com/en-us/p/ubuntu-2004-lts/9n6svws3rx71>

# Install with Ansible

## Step 1. Install Ansible and package dependencies

In the Ubuntu console:

```console
sudo apt update
```

```console
sudo apt -y install software-properties-common
```

```console
sudo add-apt-repository --y --update ppa:ansible/ansible
```

```console
sudo apt install -y ansible git
```

See: <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu>

## Step 2. Clone the FreeTAKHub-Installation Git repository

```console
git clone https://github.com/FreeTAKTeam/FreeTAKHub-Installation.git
```

In case you already created the repository previously, pull the latest:

```console
cd FreeTAKHub-Installation
```

```console
git pull  https://github.com/FreeTAKTeam/FreeTAKHub-Installation.git
```

## Step 3. Install with Ansible

An example default install playbook is defined in: `install_all.yml`.

This playbook installs all FreeTAKServer and components to your machine.

To execute the default install playbook, go into FreeTAKHub-Installation

```console
cd FreeTAKHub-Installation
```
execute the script
```console
sudo ansible-playbook install_all.yml
```

## Step 4. [check installation](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/blob/main/docs/docs/Installation/Troubleshooting/InstallationCheck.md)
