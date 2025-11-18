# Real Networking Examples (NX-OS, EOS, Junos)

These exercises show how network engineers use the `subprocess` module **in real automation pipelines**.

Most tasks involving network devices begin with:

- Reachability checks  
- DNS resolution checks  
- Interface state validation  
- Routing validation  
- ARP/MAC lookups  
- Traceroute path checks  
- Log filtering  

All of these can be automated using subprocess *before* SSH login or configuration changes.

---

# NX-OS Examples

Cisco NX-OS engineers frequently automate reachability, routing checks, MTU validation, and traceroute using Linux commands *before* connecting to the switch.

---

## Exercise NX01 — Check NX-OS Device Reachability Before SSH

### **What this teaches**
Avoid SSH delays by pre-validating reachability.

### **Code**
```python
def nx01_check_reachability(ip):
    result = subprocess.run(
        ["ping", "-c", "2", "-W", "1", ip],
        stdout=subprocess.DEVNULL,
        stderr=subprocess.DEVNULL
    )
    if result.returncode == 0:
        print(f"{ip} is reachable (NX-OS pre-check passed)")
    else:
        print(f"{ip} is unreachable (skip this device)")
```

### **Expected Output**
```
172.16.10.20 is reachable (NX-OS pre-check passed)
```

---

## Exercise NX02 — Validate MTU Path for VXLAN Fabric

Before pushing VXLAN configs, many engineers validate MTU.

### **Code**
```python
def nx02_validate_mtu(ip):
    result = subprocess.run(
        ["ping", "-M", "do", "-s", "8972", "-c", "2", ip],
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
ping: local error: Message too long
```
or:
```
8972 bytes from 172.16.10.20: icmp_seq=1 ttl=255 time=1.2 ms
```

---

## Exercise NX03 — Confirm Underlay Routing to Spine/Leaf Devices

### **Code**
```python
def nx03_check_route(ip):
    result = subprocess.run(
        ["ip", "route", "get", ip],
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
172.16.10.20 via 172.16.10.1 dev ens4 src 172.16.10.2
```

This shows:

- outgoing interface  
- next-hop  
- source IP  

---

# Arista EOS Examples

Arista automation often relies on validating reachability, connectivity to CVP/CloudVision, and LLDP/MLAG pre-checks.

---

## Exercise EOS01 — Check CVP Server Availability

### **Code**
```python
def eos01_check_cvp(ip):
    result = subprocess.run(
        ["ping", "-c", "1", ip],
        stdout=subprocess.DEVNULL,
        stderr=subprocess.DEVNULL
    )
    print("CVP reachable" if result.returncode == 0 else "CVP unreachable")
```

### **Expected Output**
```
CVP reachable
```

---

## Exercise EOS02 — LLDP Pre-Check (Before MLAG Bring-Up)

Network engineers validate LLDP between peers *before* MLAG configuration.

### **Code**
```python
def eos02_lldp_check(peer_ip):
    result = subprocess.run(
        ["lldpctl"],
        capture_output=True,
        text=True
    )

    if peer_ip in result.stdout:
        print(f"LLDP OK: Found {peer_ip}")
    else:
        print(f"LLDP FAIL: {peer_ip} not detected")
```

### **Expected Output**
```
LLDP OK: Found 172.16.10.5
```

---

## Exercise EOS03 — Validate MLAG Peer Reachability

### **Code**
```python
def eos03_check_mlag_peer(peer_ip):
    result = subprocess.run(
        ["ping", "-c", "1", peer_ip],
        stdout=subprocess.DEVNULL
    )
    print("MLAG peer reachable" if result.returncode == 0 else "MLAG peer unreachable")
```

---

# Juniper Junos Examples

Junos engineers often use subprocess to validate:

- BGP neighbor reachability  
- OSPF areas before routing policy changes  
- Path to routers  
- DNS resolution  

---

## Exercise JN01 — Check Junos Loopback Reachability (BGP Pre-Check)

### **Code**
```python
def jn01_check_bgp_peer(loopback_ip):
    result = subprocess.run(
        ["ping", "-c", "3", loopback_ip],
        stdout=subprocess.DEVNULL,
        stderr=subprocess.DEVNULL
    )
    print("BGP peer alive" if result.returncode == 0 else "BGP peer dead")
```

### **Expected Output**
```
BGP peer alive
```

---

## Exercise JN02 — Parse traceroute to Junos Device (Path Validation)

Often used before routing or firewall changes.

### **Code**
```python
def jn02_traceroute_to_device(ip):
    result = subprocess.run(
        ["traceroute", "-n", ip],
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
1  172.16.10.1   1.1 ms
2  10.1.1.1      5.3 ms
3  172.16.20.2   7.8 ms
```

---

## Exercise JN03 — Check Reverse DNS for Firewalls / Routers

Useful for NOC teams during automation.

### **Code**
```python
def jn03_reverse_dns(ip):
    result = subprocess.run(
        ["nslookup", ip],
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
Name: router1.adnoc.internal
Address: 172.16.20.2
```

---

# Summary of Real Networking Use Cases

| Vendor | Use Case | Subprocess Example |
|--------|----------|-------------------|
| Cisco NX-OS | VXLAN MTU validation | `ping -M do -s 8972` |
| Cisco NX-OS | Underlay routing check | `ip route get` |
| Arista EOS | LLDP discovery | `lldpctl` |
| Arista EOS | MLAG peer validation | `ping` |
| Junos | BGP peer reachability | `ping loopback` |
| Junos | Path validation | `traceroute` |
| All Vendors | DNS / reverse DNS | `nslookup` |

These are **actual pre-automation steps** used inside:

- configuration push pipelines  
- network provisioning tools  
- CI/CD network checks  
- health checks  
- auto-discovery scripts  
- pre-SSH automation  

