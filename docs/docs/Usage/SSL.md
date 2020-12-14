# SSL
SSL is a  protocol for secure comunication

## Activate your FTS's SSL service
TBD

## Generate a SSL connection for your server
this method requires understanding of complex console commands, we DO NOT provide support on issues with certs generations

1. Generate the CA key by typing the command
```openssl genrsa -out ca.key 1024```

2. enerate the Certificate Signing Request (CSR) by typing the command: 
```req -new -key ca.key -out ca.csr```

This command prompts you for the information to be contained in the certificate. The prompts should be answered as:

- Country Name (2 letter code) [AU]:CA
- State or Province Name (full name) [Some-State]:NS
- Locality Name (eg, city) []:Yarmouth
- Organization Name (eg, company) [Internet Widgits Pty Ltd]:FTS TEAM
- Organizational Unit Name (eg, section) []:Dev
 - Common Name (e.g. server FQDN or YOUR name) []:FTS Server

3. created ca.cfg

4. 
```x509 -req -extfile ca.cfg -days 1825 -signkey ca.key -in ca.csr -out ca.crt```
Signature ok
```subject=C = CA, ST = NS, L = Yarmouth, O = FTS, OU = Dev, CN = Ghosty```

### Getting Private key

5. created server.cfg

https://gist.github.com/fntlnz/cf14feb5a46b2eda428e000157447309
generating server keys

6. ```genrsa -out server.key 2048 ```

Country Name (2 letter code) [AU]:CA
State or Province Name (full name) [Some-State]:NS
Locality Name (eg, city) []:Yarmouth
Organization Name (eg, company) [Internet Widgits Pty Ltd]:FTS
Organizational Unit Name (eg, section) []:Dev
Common Name (e.g. server FQDN or YOUR name) []:192.168.2.75

7. 
```openssl req -new -key server.key -out server.csr```

8. 
``` openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.crt -days 1000 -sha256 ```
Signature ok
subject=C = CA, ST = NS, L = Yarmouth, O = FTS, OU = Dev, CN = 192.168.2.75
Getting CA Private Key

save key decrypted
9. openssl rsa -in ssl.key.encrypted -out ssl.key.decrypted

https://stackoverflow.com/questions/6307886/how-to-create-pfx-file-from-certificate-and-private-key
generating pfx/p12

9. openssl pkcs12 -export -out server.p12 -inkey server.key -in server.crt
requires password

generate client certs

10. openssl genrsa -out testClient.key 2048

11. openssl req -new -key testClient.key -out testClient.csr
Country Name (2 letter code) [AU]:CA
State or Province Name (full name) [Some-State]:NS
Locality Name (eg, city) []:Yarmouth
Organization Name (eg, company) [Internet Widgits Pty Ltd]:FTS
Organizational Unit Name (eg, section) []:Dev
Common Name (e.g. server FQDN or YOUR name) []:testUser
A challenge password []:atakatak

12. openssl x509 -req -in testClient.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out testClient.crt -days 1000 -sha256
Signature ok
subject=C = CA, ST = NS, L = Yarmouth, O = FTS, OU = Dev, CN = testUser
Getting CA Private Key

13. ```openssl pkcs12 -export -out testClient.p12 -inkey testClient.key -in testClient.crt```
requires pass

https://help.gamesalad.com/gamesalad-cookbook/publishing/4-android-publishing/4-02-creating-a-keystore/



### generate keystore
14. keytool.exe -genkey -v -keystore fts.keystore -alias fts -keyalg RSA -sigalg SHA1withRSA -keysize 2048 -validity 10000
Enter keystore password:
Re-enter new password:
What is your first and last name?
  [Unknown]:  test client
What is the name of your organizational unit?
  [Unknown]:  Dev
What is the name of your organization?
  [Unknown]:  FTS
What is the name of your City or Locality?
  [Unknown]:  Yarmouth
What is the name of your State or Province?
  [Unknown]:  NS
What is the two-letter country code for this unit?
  [Unknown]:  CA
Is CN=test client, OU=Dev, O=FTS, L=Yarmouth, ST=NS, C=CA correct?
  [no]:  yes

Generating 2,048 bit RSA key pair and self-signed certificate (SHA1withRSA) with a validity of 10,000 days
        for: CN=test client, OU=Dev, O=FTS, L=Yarmouth, ST=NS, C=CA

(cert will be generated in the path where the command was run)

### generate truststore
1. keytool -import -file C:\Users\natha\PycharmProjects\InDev\FreeTAKServerParent\FreeTAKServer\Certs\ServerCerts\localserver\server.crt -alias serverCert -keystore testTrustStore.p12

2. keytool -import -file C:\Users\natha\PycharmProjects\InDev\FreeTAKServerParent\FreeTAKServer\Certs\ServerCerts\testClient\testClient.crt -alias testClientCert -keystore testTrustStore.p12

## Installing SSL on a client
### ATAK
- Tap settings
- Manage server connections
- open network connections
- Add a new connection 
- assign a name and the IP of your server
- click on advanced options
- uncheck "use default SSL/TLS certificates"
- tap "import Truststore"
-  select your truststore file
- type the password provide to you
- Tap "Import client certificate"
- select your client certificate
- type the password
- type "OK"

### WinTAK
- go to  Settings
-Network preferences
- Manage Server Connections
- Add Stream 
- assign a Description, IP and port of your server
- select SSL as a protocol
-
- uncheck "use default SSL/TLS certificates"
- Click "install Certificate Authority"
-  select your Certificate Authority file
- type the password provide to you
- click  "Install client certificate"
- select your client certificate
- type the password
- click "OK"

