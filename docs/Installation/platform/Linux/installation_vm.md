---
status: current
---

# FreeTAK Server Installation on an Ubuntu Virtual Machine

This guide will walk you through installing FreeTAKServer 2.1 on an Ubuntu virtual machine.
These instructions are on preparing an Ubuntu VM suitable for using the FTS Zero Touch Installer.

Obviously, the ZTI can be installed in a clean native Ubuntu environment.
However, cleanly setting up such an environment can consume time.
So, while running FTS on dedicated hardware may be a more performant choice 
in a production environment it is more convenient with a virtual machine.

## Setting up the Virtual Machine

Thankfully, Canonical has provided tooling to make setting up an Ubuntu VM easy.

[Multipass Tutorials](https://multipass.run/docs/tutorials)

* [Multipass Windows](https://multipass.run/docs/windows-tutorial)
* [Multipass Linux](https://multipass.run/docs/get-started-with-multipass-linux)
* [Multipass MacOS](https://multipass.run/docs/mac-tutorial)

Any of these are suitable for testing.

We will want to specify a specific Ubuntu version.
```shell
multipass find
```
Of the choices available we want `v22.04`.
```shell
multipass launch 22.04 --name fts-test --memory 4G --disk 10G --cpus 2
```
We can verify the image.
```shell
multipass exec fts-test -- lsb_release -a
```

Open a shell on the new VM.
```shell
multipass shell fts-test
```

## Install FTS on the VM

Yow will probably need to install with an explicit IP address.

The [complete ZTI instructions are here](../../mechanism/Ansible/ZeroTouchInstall.md).