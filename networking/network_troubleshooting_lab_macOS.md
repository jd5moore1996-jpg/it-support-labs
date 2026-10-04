# IT Support Lab: Basic Network Troubleshooting on macOS

## Objective
Practice common network troubleshooting commands and verify:
- Local IP configuration
- Default gateway connectivity
- Internet connectivity
- DNS resolution
- Network path to a remote destination

## Environment
- Operating System: macOS
- Connection Type: Wi-Fi
- Terminal: macOS Terminal

## Commands Used

### 1. Find the local IPv4 address
```bash
ipconfig getifaddr en0
```

Result:
```text
10.0.0.x
```

What I learned:
- This command shows the IPv4 address assigned to the active Wi-Fi interface.
- A 10.x.x.x address is a private IPv4 address used inside a local network.

### 2. Find the default gateway
```bash
route -n get default
```

Result:
```text
gateway: 10.0.0.1
```

What I learned:
- The default gateway is the router/device used to reach networks outside the local LAN.
- I can think of the default gateway as the “exit door” from the local network.

### 3. Test connectivity to the default gateway
```bash
ping 10.0.0.1
```

Result:
```text
24 packets transmitted
24 packets received
0.0% packet loss
```

What I learned:
- My Mac could successfully communicate with the local router.
- 0% packet loss indicated a successful local network connection.

### 4. Test internet connectivity by IP address
```bash
ping 8.8.8.8
```

Result:
```text
30 packets transmitted
30 packets received
0.0% packet loss
```

What I learned:
- Internet connectivity was working.
- Testing an IP address directly helps separate general connectivity problems from DNS problems.

### 5. Test DNS resolution
```bash
nslookup google.com
```

Result:
```text
google.com resolved successfully to multiple IP addresses.
```

What I learned:
- DNS translated a domain name into IP addresses successfully.
- If an IP-address ping works but domain names fail, DNS may be the problem.

### 6. Trace the network path
```bash
traceroute google.com
```

Result:
- Hop 1: Local router
- Intermediate hops: ISP/network infrastructure
- One hop did not reply (`* * *`)
- Final destination: Google
- Destination reached in 9 hops

What I learned:
- `traceroute` shows the routers/hops traffic crosses to reach a destination.
- Each millisecond value is a round-trip time measurement for a probe.
- A `* * *` hop does not always mean failure; some routers do not answer traceroute probes.
- A destination such as google.com can resolve to multiple IP addresses.

## Troubleshooting Logic Practiced
1. Check local IP configuration.
2. Verify the default gateway.
3. Ping the gateway to test local connectivity.
4. Ping a public IP to test internet connectivity.
5. Use `nslookup` to test DNS.
6. Use `traceroute` to inspect the path to the destination.

## Key Commands to Remember
| Command | Purpose |
|---|---|
| `ipconfig getifaddr en0` | Show Wi-Fi IPv4 address on macOS |
| `route -n get default` | Show the default gateway |
| `ping` | Test reachability |
| `nslookup` | Test DNS/name resolution |
| `traceroute` | Trace the path to a destination |

## Security Note
Exact public ISP hop addresses and hostnames were omitted from this write-up. When publishing labs publicly, avoid posting sensitive or unnecessary network details.

## Outcome
The local network, default gateway, internet connection, DNS resolution, and route to the remote destination all tested successfully.

## Skills Demonstrated
- Basic TCP/IP troubleshooting
- IPv4 addressing
- Default gateway identification
- ICMP connectivity testing
- DNS troubleshooting
- Route/path analysis
- macOS Terminal usage
