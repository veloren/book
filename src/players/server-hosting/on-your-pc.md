# Hosting a Server on Your Computer
If you want to play with your friends and do not have a dedicated server, follow these instructions to set one up on your computer. 

## Playing over LAN
> **Note**: _This will only work when everyone is connected to the same Local Area Network (generally that means the same WiFi network or router)._

1. [Start the server](#starting-the-server)
2. [Find your local IP address](#finding-your-local-ip-address) and share it with your friends. They will need to enter it in-game to join the server.
3. Have fun! :)

## Playing over the internet
> **Note**: _You will need access to your router and knowledge about port forwarding._

> **Tip**: _If you are unable to set up port forwarding, there exist programs such as [ZeroTier](https://www.zerotier.com/), [Netbird](https://netbird.io/) or [Hamachi](https://vpn.net/), which allow a limited amount of users to connect to a local server through the internet._

1. Forward port `14004` TCP and UDP on your router.
2. [Start the server](#starting-the-server)
3. [Find your public IP address](https://www.showmyipaddress.eu/) and share it with your friends. They will need to enter it in-game to join the server.
5. Have fun! :)

> **Note**: _If you need your computer's local IP address for port forwarding, refer to the [Finding your local IP address](#finding-your-local-ip-address) section below._

## Starting the server
### Using the server provided by Airshipper:  
   *This is a good option if everyone playing uses Airshipper.*
   1. [Find your game installation folder](airshipper.md#files).
   2. Go into `profiles/default`.
   3. Launch `veloren-server-cli[.exe]`.
### Using a custom server executable:  
   *This is a good option if you want to play an older release or a custom version.*
   1. Open the folder with extracted game files.
   2. Make sure you have the `assets` folder in the same place as the server executable.
   3. Launch `veloren-server-cli[.exe]`.

## Finding your local IP address
> **Tip**: _Generally local IPv4 addresses have the form of `192.168.xxx.xxx` or, more rarely, `10.xxx.xxx.xxx`. For IPv6 addresses, local ones generally start with `fe80:`_

### On Linux and MacOS
1. Open the Terminal.
2. Type `ip addr || ifconfig` and press enter.
3. You will see all of your computer's IP addresses, grouped by network card/interface.  
Interface names starting with `e` are generally ethernet while ones starting with `w` are generally wireless.
Lines starting with `inet` and `inet6` show IPv4 and IPv6 addresses respectively. If there are multiple addresses in one line, only the first is important.  
For example, `lo` is the loopback interface with a `127.0.0.1` IPv4 address and a `::1` IPv6 address.  
Likely, the first address which doesn't belong to the loopback interface is what you are looking for.

### On Windows
1. Open CMD (type `cmd.exe` into the start menu and press enter).
2. Type `ipconfig` and press enter.
3. You will see all of your computer's IP addresses, grouped by network card/interface.  
Lines starting with `IPv4 address` or `IPv6 address` show the respective address types.
Likely, the first address which isn't `127.0.0.1` or `::1` will be what you are looking for.