# Visual Explanation: How subprocess Creates Child Processes

The following diagrams show **exactly what happens** when your Python code runs a Linux command.

---

## 1. Without Subprocess  
(You type commands manually)

```
+-------------------+
|   Your Terminal   |
+-------------------+
          |
          v
+-------------------+
| Linux Shell (bash)|
+-------------------+
          |
          v
+-------------------+
|   Command Output  |
+-------------------+
```

You type commands → shell runs them → you see output.

---

## 2. With subprocess.run()

```
+-------------------+
|   Python Script   |
+-------------------+
          |
          | subprocess.run(["ping", "8.8.8.8"])
          v
+---------------------------+
|   Child Process Created   |
|      (ping command)       |
+---------------------------+
          |
   stdout / stderr / returncode
          |
          v
+---------------------------+
| CompletedProcess Object   |
+---------------------------+
          |
          v
Python uses the results
```

### Meaning:
- Python launches a **child process**
- Linux executes the command
- Python **collects the result object**
- You can inspect:
  - stdout  
  - stderr  
  - returncode  

---

## 3. With subprocess.Popen() (Advanced)

```
+-------------------+
|   Python Script   |
+-------------------+
          |
          v
+---------------------------------+
|   Popen (child process handle)  |
+---------------------------------+
     |         |           |
     |         |           |
  stdin     stdout       stderr
     ^         |           |
     |         |           |
 Interact  Stream logs   Capture errors
 in real-   line-by-line
 time
```

Popen gives you **three live pipes** you can read and write.

---

# Additional Example Functions for Network Automation

Below are high-value functions commonly used by real network engineers.

---

# 1. Traceroute Parser

Runs traceroute and extracts hop IPs.

```python
import subprocess
import re

def traceroute_hosts(target):
    result = subprocess.run(
        ["traceroute", "-n", target],
        capture_output=True,
        text=True
    )
    hops = []
    for line in result.stdout.splitlines():
        match = re.search(r"^\s*\d+\s+(\d+\.\d+\.\d+\.\d+)", line)
        if match:
            hops.append(match.group(1))
    return hops

# Example
print(traceroute_hosts("8.8.8.8"))
```

### What this teaches:
- capturing stdout  
- parsing line-based output  
- using regex for clean extraction  

---

# 2. Search Logs Using grep (via shell=True)

```python
import subprocess

def grep_log(file_path, keyword):
    result = subprocess.run(
        f"grep -i '{keyword}' {file_path}",
        shell=True,
        capture_output=True,
        text=True
    )
    return result.stdout.strip()

# Example
print(grep_log("/var/log/syslog", "error"))
```

### What this teaches:
- When to use `shell=True`
- Running grep safely
- Returning filtered information

---

# 3. Extract Interface Information from `ip addr`

```python
import subprocess
import re

def get_interfaces():
    result = subprocess.run(
        ["ip", "addr"],
        capture_output=True,
        text=True
    )

    interfaces = []
    for line in result.stdout.splitlines():
        if re.match(r"^\d+:\s", line):
            name = line.split(":")[1].strip()
            interfaces.append(name)

    return interfaces

# Example
print(get_interfaces())
```

### What this teaches:
- parsing multiline stdout
- extracting interface names

---

# 4. Get IP Addresses of All Interfaces

```python
import subprocess
import re

def get_interface_ips():
    result = subprocess.run(
        ["ip", "-4", "addr"],
        capture_output=True,
        text=True
    )
    ips = re.findall(r"inet (\d+\.\d+\.\d+\.\d+)", result.stdout)
    return ips

# Example
print(get_interface_ips())
```

### What this teaches:
- regex IP extraction  
- processing raw Linux command output  

---

# 5. Advanced: Capture Real-Time Output (Popen)

```python
import subprocess

def follow_log(file):
    process = subprocess.Popen(
        ["tail", "-f", file],
        stdout=subprocess.PIPE,
        text=True
    )
    for line in process.stdout:
        print("LOG:", line.strip())

# Example: follow_log("/var/log/syslog")
```

### What this teaches:
- real-time streaming  
- using Popen for live output  
- reading from stdout pipe line-by-line  

---

# Summary of Additional Functions

| Function | Purpose |
|----------|----------|
| traceroute_hosts() | Extract hop IPs from traceroute |
| grep_log() | Search logs for keywords |
| get_interfaces() | List OS network interfaces |
| get_interface_ips() | Extract IPv4 addresses |
| follow_log() | Stream logs in real-time |



