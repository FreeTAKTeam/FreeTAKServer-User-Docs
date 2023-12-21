---
status: ood
---

# Install FreeTAKHub with Ansible

Ansible is an Infrastructure-As-Code (IAC) tool used for managing and monitoring local or remote FTS servers.

This repository includes Ansible roles to:

- create the target nodes.
- install FTS and additional modules.
- configure FTS.

## Windows Prerequisites

Below is required for Windows machines.

The machine must be running: Windows 10 Version 2004 or higher (Build 19041 or higher) or Windows 11.

For Windows installations:

1. Install WSL2.

    See: <https://docs.microsoft.com/en-us/windows/wsl/install>

    See also: <https://www.omgubuntu.co.uk/how-to-install-wsl2-on-windows-10>

    See also: <https://www.sitepoint.com/wsl2/>

2. Install the WSL Ubuntu 22.04 distribution.

    See: <https://www.microsoft.com/en-us/p/ubuntu-2004-lts/9n6svws3rx71>

## Step 1. Clone the `FreeTAKHub-Installation` repository

In the console:

```console
sudo apt update
```

Make sure you have `git` installed:

```console
sudo apt install -y git
```

Go to the home directory:

```console
cd ~
```

Clone the `FreeTAKHub-Installation` repository:

```console
git clone https://github.com/FreeTAKTeam/FreeTAKHub-Installation.git
```

Go to the top-level directory of the FreeTAKHub-Installation repository:

```console
cd FreeTAKHub-Installation
```

If you have previously cloned the repository, update the repository:

```console
git pull
```

## Step 2. Install Ansible

### Automated Ansible Installation

At the top-level directory of the `FreeTAKHub-Installation` repository, enter:

```console
./scripts/init.sh
```

Optional (But Recommended!): Activate the Python virtual environment:

```console
activate
```

To deactivate the Python virtual environment:

```console
deactivate
```

To learn more about Python virtual environments and why they are a good idea, see:

<https://realpython.com/python-virtual-environments-a-primer/>

### Manual Ansible Installation
 
The manual installation allows more control.

In the console, enter:

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
sudo apt install -y ansible
```

See: <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu>

## Step 3. Install FreeTAKServer and Components

Go to the top-level directory of the `FreeTAKHub-Installation` repository:

```console
cd ~/FreeTAKHub-Installation
```

Run the Ansible playbook to install FreeTAKServer and components:

```console
sudo ansible-playbook install_all.yml
```

## Step 4. Check Installation

Directions to check installation [here](../Troubleshooting/InstallationCheck.md).
