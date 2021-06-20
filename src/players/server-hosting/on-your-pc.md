# Hosting a Server on Your Computer
If you want to play with your friends and do not have a dedicated server, follow these instructions to set one up on your computer. 

> **Note**: _You will need access to your router and knowledge about port forwarding._

1. Forward port `14004` TCP and UDP on your router.
2. Start the server
    - Using the server provided by Airshipper:  
        *This is a good option if everyone playing uses Airshipper.*
        1. [Find your game installation folder](airshipper.md#files).
        2. Go into `profiles/default`.
        3. Launch `veloren-server-cli[.exe]`.
    - Using a custom server executable:  
        *This is a good option if you want to play an older release.*
        1. Open the folder with extracted game files.
        2. Make sure you have the `assets` folder in the same place as the server executable.
        3. Launch `veloren-server-cli[.exe]`.
3. [Find your public IP address](https://www.showmyipaddress.eu/) and share it with your friends.
4. Have fun! :)

> **Note**: If you want to play only via LAN, or need your computer's local IP address for port forwarding, refer to the Appendix A below.

## Appendix A: Finding your local IP address
- Some Linux Distros:
   1. Open the Terminal.
   2. Type `ip -br -4 addr | grep -v 'lo '` and press enter.
      > **Example output:**  
      > `wlp3s0 UP 192.168.100.13/24 192.168.100.14/24`  
   3. The first ip address after `UP`, without the part after the `/` is what you're looking for.  
   In the example that's `192.168.100.13`.
- MacOS / Other Linux Distros:
   1. Open the Terminal.
   2. Type `ifconfig | grep 'inet ' | grep -v 127.0.0.1` and press enter.
      > **Example output:**  
      > `inet 192.168.12.37  netmask 255.255.255.0  broadcast 192.168.1.255`  
   3. The first IP address after `inet` is what you're looking for.  
   In the example that's `192.168.12.37`.
- Windows:
   1. Open CMD (type `cmd.exe` into the start menu and press enter).
   2. Type `ipconfig | findstr IPv4` and press enter.
      > **Example output:**  
      > `IPv4 address. . . . . . . . . . . : 127.0.0.1`  
      > `IPv4 address. . . . . . . . . . . : 192.168.3.24`  
      > `IPv4 address. . . . . . . . . . . : 192.168.3.25`  
   3. Find the first address which isn't `127.0.0.1`.  
   In the example that's `192.168.3.24`.