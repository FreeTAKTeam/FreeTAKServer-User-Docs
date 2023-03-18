# General Tips
## Helpful Tools
* **PuTTy** – Allows you to remotely connect and manage your RPi. Helpful for being able to copy/paste from this document into the RPi Terminal
CLI. 
1. Download PuTTY here: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
2. To setup: Under Host Name, enter your RPi IP address and select SSH for Connection type

* **WinSCP** – A GUI-type file manager. Helpful for basic file management and understanding the RPi’s file structure. You can also start Putty from a WinSCP
1. Download WinSCP here: https://winscp.net/eng/download.php
2. To setup: Click New Site; select SCP for File protocol; enter RPi’s IP address for Host name; click Advanced button, select ‘Shell’ under
environment and change Shell setting from Default to Sudo su - (this will allow your changes to have Root privileges)
3. Click OK and then Save (if desired)

* **ZeroTier** - A software-defined wide area networking infrastructure that allows you to create a virtual network that is relatively secure and under
your control. Allows clients to have static IPs that can be accessed regardless of location on the internet and can be toggled on/off instantly
