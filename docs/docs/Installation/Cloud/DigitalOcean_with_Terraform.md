# DigitalOcean with Terraform

This installation has only been tested on Ubuntu 22.04.

Other operating systems may work, but are untested.

## Step 1. Create admin user

The later executions will require admin privileges.

Create an `adminuser` first:

```console
sudo adduser adminuser
```

Add `passwordless` to `adminuser`.

First type:

```console
sudo visudo
```

Then add at the bottom:

```console
adminuser ALL=(ALL) NOPASSWD: ALL
```

To save and quit in the `nano` editor:

1. Press `CTRL + O` then `ENTER` to save.
2. Then press `CTRL + X` to exit.

## Step 2. Download Terraform and Ansible

In the Ubuntu console:

```console
sudo apt update
```

```console
sudo apt install -y software-properties-common gnupg curl git
```

```console
sudo add-apt-repository -y --update ppa:ansible/ansible
```

```console
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

```console
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

```console
sudo apt install -y ansible terraform
```

## Step 3. Clone the `FreeTAKHub-Installation` Git repository

Go to the home directory:

```console
cd ~
```

```console
git clone https://github.com/FreeTAKTeam/FreeTAKHub-Installation.git
```

Go to the `FreeTAKTeam/FreeTAKHub-Installation` directory:

```console
cd FreeTAKTeam/FreeTAKHub-Installation
```

## Step 4. Generate a public/private key pair

For the default, enter (and keep pressing enter):

```console
ssh-keygen
```

Print out the public key for the next step.

If you did the default, the command will be:

```console
cat ~/.ssh/id_rsa.pub
```

## Step 5. Add your public key to your Digital Ocean project

See: <https://docs.digitalocean.com/products/droplets/how-to/add-ssh-keys/to-account/>

## Step 6. Generate a Digital Ocean Personal Access Token

See: <https://docs.digitalocean.com/reference/api/create-personal-access-token/>

## Step 7. Execute

In the top-level directory of the project, initialize Terraform:

```console
terraform init
```

Then apply:

```console
terraform apply
```

You will then be prompted for your DigitalOcean Token and private key path:

```console
var.digitalocean_token
  Enter a value: <DIGITALOCEAN_TOKEN_HERE>

var.private_key_path
  ABSOLUTE path to private key, for example: /home/adminuser/.ssh/id_rsa

  Enter a value: /home/adminuser/.ssh/id_rsa
```
