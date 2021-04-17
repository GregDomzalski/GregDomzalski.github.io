# FreeNAS: Setting up Minecraft Server inside of an IOCage Jail

Tutorial originally followed was from here: https://www.ricalo.com/blog/minecraft-server-freenas/

## Creating a jail

Connect to the FreeNAS console and select "Jails" from the left hand navigation.

Click "Add" on the top right of the Jail screen.

This brings you to the Jail creation wizard.

For step 1 (Name Jail and Choose FreeBSD Release), use the following options:

- Name: "minecraft" (You can use whatever name you want.)
- Jail type: Default (Clone Jail)
- Release: 11.4-RELEASE (use the latest release version you have)

For step 2 (Configure Networking), use the following options:

- DHCP Autoconfigure IPv4: Unchecked
- NAT: Unchecked
- VNET: Check
- IPv4 Interface: VNET0
- IPv4 Address: (whatever makes sense)
- IPv4 Netmask: 24
- IPv4 Default Router: (Your router IP)
- Autoconfigure IPv6: Check

Confirm the options and create the jail.

## Installing Minecraft Java server

Find the java server file from the Minecraft website.

Open a shell to the jail.

```shell
pkg update
pkg install --yes curl
pkg install --yes openjdk8

mkdir -p /root/minecraft
cd /root/minecraft
curl -O https://pathtodownload/
java -jar /root/minecraft/server.jar
```
