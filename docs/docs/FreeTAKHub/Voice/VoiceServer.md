---
status: ood
---

# FreeTAKHub Voice installation

the FTH Voice server is based on Mumble
to install it manually:
* open a console terminal
* Do some cleaning
```bash
sudo apt-get update
sudo apt-get upgrade
```
* If asked to confirm installing any packages; then, type `Y` and press Enter.

* Now Install Mumble Server.
```bash
sudo apt-get install mumble-server
```

as soon it is started you may want to configure it
```bash
sudo dpkg-reconfigure mumble-server
```

You can use your arrow keys to select your answer, then press Enter to continue.

![image](https://user-images.githubusercontent.com/60719165/159131852-ebda53e1-1ed8-4f3f-bacd-b60ed7ed2664.png)

you will accept the default value of Yes because we want Mumble-Server to run when the server boots.

![image](https://user-images.githubusercontent.com/60719165/159131856-e7510b41-bfdd-43ba-ad5a-efe89fbd3d4d.png)

Even if this will be a dedicated Mumble-Server,
now select `Yes` since this will ensure the lowest possible latency.

### Mumble SuperUser Password
SuperUser is the highest-level administrative account for the server. 
You will need to log in to Mumble with this user when you want to manage the server.

![image](https://user-images.githubusercontent.com/60719165/159131862-e9dc9b27-9974-4fd4-8db9-0c97cad064db.png)

Type a password, press `Tab` to select `Ok`, and press Enter.

## Configuring Certificates

To create a self-signed cert that is fulfils all requirements for the TAK Voice Plugin, you can run the following command:
```
openssl req -x509 -sha256 -nodes -days 1080 -newkey rsa:2048 -keyout (servername).key -out (servername).cer -subj '/CN=(IP Address)' -addext extendedKeyUsage=1.3.6.1.5.5.7.3.1
```
This OpenSSL command is used to create a self-signed X.509 certificate along with a new private key. Here's a breakdown of each part of the command:

* openssl req: Invokes the OpenSSL utility to generate a new X.509 certificate signing request (CSR). However, in this context, combined with -x509, it's used to create a self-signed certificate instead of just a CSR.
* x509: This option specifies that a self-signed certificate is to be generated instead of a certificate request.
* sha256: Specifies the hashing algorithm for signing the certificate. SHA-256 is a secure hashing algorithm, making the certificate more secure.
* nodes: Stands for "no DES". This option specifies that the private key should not be encrypted with a passphrase, allowing applications to use the key without manual intervention.
* days 1080: Sets the validity of the certificate to 1080 days from the issue date.
* newkey rsa:2048: Generates a new RSA private key of 2048 bits. This is a good default for secure communications.
* keyout ftsmurmur.key: Specifies the filename to save the newly created private key to, named ftsmurmur.key.
* out ftsmurmur.cer: Specifies the filename to save the newly created certificate to, named ftsmurmur.cer.
* subj '/CN=(IP Address)': Sets the subject of the certificate. In this case, it sets the Common Name (CN) to an IP address e.g. 117.154.131.250. Commonly, the CN is a domain name for SSL certificates, but an IP address can be used for specific purposes.
* addext extendedKeyUsage=1.3.6.1.5.5.7.3.1: Adds an extension to the certificate for extended key usage. The specified Object Identifier (OID) 1.3.6.1.5.5.7.3.1 corresponds to TLS Web Server Authentication, indicating that the certificate is intended for use as a TLS/SSL server certificate.

for example if your IP is 117.154.131.250 and registerName is 'ftsmurmur'
```
openssl req -x509 -sha256 -nodes -days 1080 -newkey rsa:2048 -keyout ftsmurmur.key -out ftsmurmur.cer -subj '/CN=117.154.131.250' -addext extendedKeyUsage=1.3.6.1.5.5.7.3.1
```

## Use the voice Tak plugin
now create a certificate for local CA
```
openssl x509 -in ftsmurmur.cer -outform der -out ftsmurmur.der
```
Transfer the Certificate to Your Android Device:

Connect your device to your computer via USB, email the certificate to an account accessible from your device, or use a cloud storage service to transfer the ftsmurmur.der file to your Android device.
Install the Certificate:

### For Android Nougat (7.0) and above:

Go to Settings > Security & location > Encryption & credentials (the exact path might vary).
Tap Install a certificate > CA certificate.
Navigate to the location where you saved the certificate file on your device.
Select the certificate file to be installed. You might need to change the file type to "All files" or similar to see the DER file.


## Init configuration
you will need to edit some configuration files.

Using `WinSCP` navigate to 
```text
/etc/mumble-server.ini
```

In general, you want to set the following values:
```text
; Port to bind TCP and UDP sockets to you can leave the standard.
port=64738
; Password to join server.
serverpassword=
;Welcome message sent to clients when they connect.
welcometext= "<br />Welcome to this server running <b>FTH Voice</b>.<br />the Parrot is not dead!<br />"
bandwidth=
; the maximum users allowed on the server
users=
registerName=ftsmurmur
; If you have generated a proper SSL certificate using the instructions above, you can provide the filenames here.
; Otherwise, Murmur will create its own certificate automatically.
sslCert=/opt/ftsmurmur.cer
sslKey=/opt/ftsmurmur.key
```
examine the complete file for more settings.
