Fixing Connection Timeout Issues in MX Bikes

As far as I know, there are two main connection timeout issues in MX Bikes:

1. Connection Issues to the Master Server

If you receive a "Connection Timeout" as soon as you click Race, without ever seeing a list of servers, your game’s connection to the master server is not working.

TL;DR: Restart your PC (and router if needed).

Communication between MX Bikes and the Master Server is straightforward and should not require any port forwards or firewall exceptions. However, the master server authenticates and keeps track of connections to it from MX Bikes.

If you experience this error, you’ve probably got a “dead” connection preventing your game from creating a new one.

Solution: Restart your PC

Simply restarting your PC usually resolves this issue, since it'll reset the connection to the master server.

If restarting the PC alone doesn’t help, restart your router as well.

If you have multiple PCs running MX Bikes at home, try them one at a time.

If this still doesn’t work, ensure your router/firewall allows OUTBOUND and ESTABLISHED traffic to master.mx-bikes.com on 54200/UDP.

2. Connection Issues to Individual Servers

If you can retrieve the server list but get a "Connection Timeout" when trying to connect to certain servers, the connection between your game and that server isn’t working.

This requires opening ports and possibly adjusting firewall settings.

TL;DR: Forward 54210/UDP in your router to the PC running MX Bikes. Search the internet for "Port forward router name" for guidance.

Solution 1: Open Port on the Server (Recommended)

By convention, the person hosting the server is expected to allow incoming connections from clients. Only the host needs to open ports, rather than every player.

Forward INCOMING traffic on the server port used by MX Bikes to the IP of the PC running the server.

By default, the port is 54210/UDP (can be changed only when running a dedicated server).

The exact steps vary depending on your router. Search for "port forward <router name>" for detailed instructions.

Solution 2: Client-Side Port Forwarding

If the host hasn’t opened the port, players can still solve the issue by forwarding traffic to the client port. This works because the master server will ask the game server to initiate the connection to the client (a bit backwards, but it works).

By default, this is 54210/UDP (can be changed with the -clientport command-line option).

The steps are the same as Solution 1.

Example Port Forward

Router IP: 192.168.1.1

PC IP (running MX Bikes): 192.168.1.10

Client Port: 54210/UDP

In this setup, forward 54210/UDP from 192.168.1.1 to 192.168.1.10.
