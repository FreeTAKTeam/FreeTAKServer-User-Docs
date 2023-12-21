---
status: ood
---

## FTS Infrastructure
![image](https://user-images.githubusercontent.com/60719165/183449678-e2c153e3-0eea-4cd9-bc69-63b4adb10491.png)

TAK Infrastructure thoughts: Give some thought to how you are going to deploy FTS server.

1. **Cloud** - A Digital Ocean (DO) or other virtually hosted server will allow the quickest deployment and is scalable to as many users as you wish
2. **LAN** - An RPi server located on your home/office LAN may require additional complexities for non-LAN TAK clients to access your server, e.g. dynamic
DNS services (<https://noip.com>) and NAT port forwarding.
3. **VPN** - An RPi server running as a ZeroTier (or other SD-WAN) client will mostly circumvent the need for the complexities listed above and allow any TAK
client on the ZeroTier network to access the RPi server regardless of internet connection method (broadband, cellular data, etc.)
4. **Edge** - An RPi server running on an ad hoc or local infrastructure LAN configuration – Can be setup completely off-grid and without reliance on a
functioning internet, but will suffer significant limitations in range for TAK clients to connect.
5. **Hybrid off-grid** – A DO installed server or RPi with one or more of the TAK clients connected as a "bridge" to an off-grid mesh network such as Meshtastic
LoRa. This configuration will allow any off-grid Meshtastic clients to have their communications reach all "internet-connected" TAK clients via a
TAK client who is simultaneously connected to both the internet and mesh sides of the network.

## Network 101
FreeTAKServer is a server application designed for use for Tactical Assault Kit (TAK) clients.
Like many server applications,
FreeTAKServer requires a **public IP** address in order to be accessible from outside the local network.

A public IP address is a globally unique IP address that is assigned to a device by an internet service provider (ISP).
Devices on the internet use public IP addresses to communicate with each other, and public IP addresses are necessary for devices to be accessible from outside the local network.

Without a public IP address, FreeTAKServer would only be visible within the local network.
This means that devices outside the local network, such as those on the internet, would not be able to access or communicate with the server.
In order for FreeTAKServer to be accessible from outside the local network,
**it must have a public IP address that is routable on the internet**.

One way to make FreeTAKServer accessible from outside the local network is to configure port forwarding on the router that connects the local network to the internet.
This allows incoming traffic on a specific port to be forwarded to the FreeTAKServer, making it accessible from the internet using the public IP address of the router.
Another option is to use a Virtual Private Network (VPN) to connect to the local network, which can allow remote devices to access FreeTAKServer as if they were on the local network with a private IP address.

| Private IP Address Block      | CIDR Notation  |
|-------------------------------|----------------|
| 10.0.0.0 - 10.255.255.255     | 10.0.0.0/8     |
| 172.16.0.0 - 172.31.255.255   | 172.16.0.0/12  |  
| 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 |

A 192.168.X.X IP address is part of the range of IP addresses that have been reserved for private networks according to the Internet Assigned Numbers Authority (IANA) standard.
The 192.168.X.X range falls within the private IP address space defined by the RFC 1918.

Private IP addresses are used for local area networks (LANs) and are
**not routable over the public internet**.
They can be used by anyone without the need to register or pay for them. Private IP addresses are typically assigned by your home router using Network Address Translation (NAT), which allows multiple devices on a LAN to share a single public IP address.

In the case of a 192.168.X.X address,
it would typically be assigned to a device on a private network,
such as a home or office LAN.
This device would not be directly accessible from the internet,
as the 192.168.X.X address is not publicly routable.

Using private IP addresses like 192.168.X.X may help improve network security by keeping internal devices hidden from external networks,
while still allowing them to communicate with each other within the private network.

When you connect to the internet,
your device is assigned a public IP address that can be seen by other devices on the internet.
This public IP address is used to route traffic between your device and other devices on the internet.
However, devices on the internet cannot directly access or see the private IP addresses used on your local network,
such as a 19.X.X.X address.

## Ports
![image](https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs/assets/60719165/2293abf0-b5af-42e4-a7e2-4df208df3eaf)

A complete FTS installation includes several components that need to have access to the 'internet'.
They will typically share the same IP but have different ports that need to be open on the firewall.

 * 5000: Required for the Web UI
 * 8080: Required for HTTP
 * 8443: Required for HTTPS 
 * 8087: required for TCP COTS
 * 8089: required for SSL COTS
 * 9000: Required for Federation
 * 9997: required for the Video Server (MediaMTX)
 * 64738: required for the Voice Server (Murmur)
 * 1880: required for the Integration server (NodeRed)
