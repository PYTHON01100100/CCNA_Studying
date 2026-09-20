# Networking Terminal Commands Reference

Quick reference for common network troubleshooting and diagnostic commands, useful for CCNA labs and real-world troubleshooting.

## Connectivity Testing

### ping
Tests basic reachability to a host using ICMP echo requests.
```
ping google.com
ping -c 4 8.8.8.8        # Linux/Mac: send 4 packets
ping -n 4 8.8.8.8         # Windows: send 4 packets
ping -t 8.8.8.8            # Windows: continuous ping
```

### traceroute / tracert
Shows the path (hop by hop) packets take to reach a destination.
```
traceroute google.com      # Linux/Mac
tracert google.com         # Windows
```

### MTR
Combines ping and traceroute into a continuous, real-time diagnostic tool.
```
mtr google.com              # Linux/Mac
mtr -r -c 10 google.com    # report mode, 10 cycles
```
Windows: not built-in, use WinMTR.

## IP Configuration

### ipconfig / ifconfig / ip
View and manage network interface configuration.
```
ipconfig /all               # Windows: full config
ipconfig /release            # Windows: release DHCP lease
ipconfig /renew              # Windows: renew DHCP lease
ipconfig /flushdns           # Windows: clear DNS cache

ifconfig                     # Linux/Mac (legacy)
ip addr show                 # Linux: modern equivalent
ip a                         # shorthand
```

## DNS Lookup

### nslookup
Query DNS records interactively or directly.
```
nslookup google.com
nslookup -type=MX google.com
```

### dig
More detailed DNS lookup tool (Linux/Mac, available on Windows via install).
```
dig google.com
dig google.com MX
dig +short google.com
dig -x 8.8.8.8               # reverse lookup
```

## Packet Capture

### tcpdump
Command-line packet capture and analysis (Linux/Mac).
```
tcpdump -i eth0
tcpdump -i eth0 port 80
tcpdump -i eth0 host 8.8.8.8
tcpdump -i eth0 -w capture.pcap   # write to file for Wireshark
```

## Port & Connection Status

### netstat
Displays active connections, listening ports, and routing info.
```
netstat -an                 # all connections, numeric
netstat -tulnp               # Linux: TCP/UDP listening ports with process
netstat -ano                # Windows: with process IDs
```

### route
View and manipulate the IP routing table.
```
route print                  # Windows
route -n                     # Linux: numeric routing table
ip route show                # Linux: modern equivalent
```

## Port Scanning

### nmap
Network exploration and port scanning tool. Use only against systems you own or are authorized to test.
```
nmap 192.168.1.1
nmap -sV 192.168.1.1          # service/version detection
nmap -p 1-65535 192.168.1.1   # scan all ports
nmap -sn 192.168.1.0/24       # ping sweep / host discovery
```

## Manual Port Testing

### telnet
Tests TCP connectivity to a specific port (also used for legacy remote access).
```
telnet 192.168.1.1 80
```

### nc (Netcat)
"Swiss army knife" for TCP/UDP connections — port testing, banner grabbing, simple file transfer, listeners.
```
nc -zv 192.168.1.1 80         # test if port is open
nc -l -p 4444                 # listen on port 4444
nc -u -zv 192.168.1.1 53      # UDP port test
```

## Quick Reference Table

| Task | Command |
|---|---|
| Test reachability | `ping` |
| Trace path to host | `traceroute` / `tracert` |
| Continuous path diagnostics | `mtr` |
| View/manage IP config | `ipconfig` / `ip addr` |
| DNS lookup | `nslookup` / `dig` |
| Capture packets | `tcpdump` |
| View connections/ports | `netstat` |
| View routing table | `route` / `ip route` |
| Scan ports/hosts | `nmap` |
| Test a specific port | `telnet` / `nc -zv` |
