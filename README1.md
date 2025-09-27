# Fixing Connection Timeout Issues in MX Bikes

As far as I know, there are two main connection timeout issues in **MX Bikes**:

---

## 1. Connection Issues to the Master Server

If you receive a **"Connection Timeout"** as soon as you click *Race*, without ever seeing a list of servers, your game’s connection to the master server is not working.

> **TL;DR:** Restart your PC.

Communication between MX Bikes and the Master Server is straightforward and should not require any port forwards or firewall exceptions. However, the master server authenticates and keeps track of connections to it from MX Bikes.

If you experience this error, you’ve probably got a “dead” connection preventing your game from creating a new one.

### Solution: Restart your PC
- Simply restarting your PC usually resolves this issue, since it'll reset the connection to the master server.
- If you have multiple PCs running MX Bikes at home, try them one at a time.  
- If this doesn’t work, ensure your router/firewall allows **OUTBOUND and ESTABLISHED traffic** to `master.mx-bikes.com` on `54200/UDP`.

---

## 2. Connection Issues to Individual Servers

If you can retrieve the server list but get a **"Connection Timeout"** when trying to connect to certain servers, the connection between your game and that server isn’t working.

This requires opening ports and possibly adjusting firewall settings.

> **TL;DR:** Forward `54210/UDP` in your router to the IP of the PC running MX Bikes. Search the internet for *"Port forward _router name_"* for guidance.

### Solution 1: Open Port on the Server (Recommended)
By convention, the person **hosting the server** is expected to allow incoming connections from clients. Only one person (the host) needs to open ports, rather than every player.  

- Forward **INCOMING** traffic on the **server port** used by MX Bikes to the IP of the PC running the server.  
- By default, the port is `54210/UDP` (can be changed only when running a dedicated server).  
- The exact steps vary depending on your router. Search for *"port forward <router name>"* for guidance.

### Solution 2: Client-Side Port Forwarding
If the host hasn’t opened the port, players can still solve the issue by forwarding traffic to the **client port**. This works because the master server will ask the game server to initiate the connection to the client (which is a bit backwards, but it works).

- By default, this is `54210/UDP` (can be changed with the `-clientport` command-line option).  
- The steps are the same as Solution 1.

### Example Port Forward
- Router IP: `192.168.1.1`  
- PC IP (running MX Bikes): `192.168.1.10`  
- Client Port: `54210/UDP`  

In this setup, forward `54210/UDP` from `192.168.1.1` to `192.168.1.10`.

---

## Common Misconceptions

### This is PiBoSo's fault
It's really not. The necessity to forward ports comes from how online networking works, not from MX Bikes itself. Unlike most modern games, PiBoSo allows us to host servers ourselves, which gives players more flexibility and control but also means we have to handle some of the networking setup on our end.  

### “I can only connect to dedicated/rented servers”
This may seem true, but the real issue is that dedicated server hosts usually know how to open ports properly.

### “Dedicated servers must be rented”
False. You can host your own dedicated server by running MX Bikes with the `-dedicated` option.

### “No ping means I can’t connect”
Not true. While this may indicate the **server host hasn’t opened the server port**, you should still be able to conect by using Solution 2.

### Using Port Checkers
Port checkers typically work for TCP or mixed TCP/UDP services.  
MX Bikes uses **UDP only**, so port checkers won’t work. This is intentional due to the faster, stateless nature of UDP.

### “Local” Tab
The *Local* tab in MX Bikes means **LAN servers** (on your home network), not regional servers (EU, NA, etc.).

---

## Edge Cases

### CGNAT
Some ISPs use **Carrier-Grade NAT (CGNAT)**, which can prevent hosting or connecting in certain ways.  
If you’re behind CGNAT:
- Solution 2 won’t work.  
- Contact your ISP to ask for removal from CGNAT.

### Firewalls
Usually, Windows adds exceptions for MX Bikes automatically.  
If you use a third-party firewall, make sure to manually allow MX Bikes traffic according to the port reference below.


## Port Reference
- **Master server DNS:** `master.mx-bikes.com`
- **Master Server Port:** `54200/UDP`  
- **Client Port:** `54210/UDP` (changeable with `-clientport`)  
- **Server Port:** `54210/UDP` (changeable with `-dedicated`)  
