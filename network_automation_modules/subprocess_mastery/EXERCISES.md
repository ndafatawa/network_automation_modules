# Subprocess Exercises (Complete Reference)

This file contains practical exercises demonstrating how to use the `subprocess` module for real network-automation tasks.  
Each function includes:

- What the function does  
- Why it’s useful in automation  
- Code  
- Expected output  

---

## Exercise 01 — Run `ls -l`

### **What this exercise teaches**
- How to execute a simple Linux command
- How to capture standard output
- How to print command output in Python

### **Code**
```python
def ex01_run_ls():
    result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
    print(result.stdout)
```

### **Expected Output**
(Your file list)

```
-rw-r--r-- 1 root root   200 Jan 10 10:10 config.yml
drwxr-xr-x 2 root root  4096 Jan 10 09:00 logs
```

---

## Exercise 02 — Capture an Error (stderr)

### **What this exercise teaches**
- How subprocess handles command failures
- The difference between stdout and stderr
- How to check error messages programmatically

### **Code**
```python
def ex02_capture_error():
    result = subprocess.run(
        ["ls", "/does/not/exist"],
        capture_output=True,
        text=True
    )
    print("STDERR:", result.stderr)
```

### **Expected Output**
```
STDERR: ls: cannot access '/does/not/exist': No such file or directory
```

---

## Exercise 03 — Ping Sweep (Silent Output)

### **What this exercise teaches**
- How to run ping without printing output
- Using DEVNULL to silence stdout and stderr
- Using returncode for reachability checks
- Host discovery in automation

### **Code**
```python
def ex03_ping_sweep():
    for i in range(1, 10):
        ip = f"192.168.10.{i}"
        result = subprocess.run(
            ["ping", "-c", "1", "-W", "1", ip],
            stdout=subprocess.DEVNULL,
            stderr=subprocess.DEVNULL
        )
        print(ip, "UP" if result.returncode == 0 else "DOWN")
```

### **Expected Output**
```
192.168.10.1 UP
192.168.10.2 DOWN
192.168.10.3 UP
...
```

---

## Exercise 04 — Parse Ping Latency

### **What this exercise teaches**
- How to capture ping output
- How to use regex to extract latency values
- How to parse Linux CLI output into Python values

### **Code**
```python
def ex04_latency_parser():
    result = subprocess.run(
        ["ping", "-c", "1", "8.8.8.8"],
        capture_output=True,
        text=True
    )
    match = re.search(r"time=(\d+\.\d+)", result.stdout)
    print("Latency:", match.group(1) if match else "N/A")
```

### **Expected Output**
```
Latency: 12.4
```

---

## Exercise 05 — Traceroute Parser

### **What this exercise teaches**
- Running multi-line CLI commands
- Capturing large stdout output
- Preparing for hop-by-hop analysis tasks

### **Code**
```python
def ex05_traceroute():
    result = subprocess.run(
        ["traceroute", "-n", "8.8.8.8"],
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
1  192.168.1.1  1.2 ms
2  10.10.10.1   5.3 ms
3  8.8.8.8     10.0 ms
```

---

## Exercise 06 — Pipeline Using `shell=True`

### **What this exercise teaches**
- When and why to use shell=True
- How to execute pipeline commands like `cmd1 | cmd2`
- How to capture filtered logs

### **Code**
```python
def ex06_pipeline_grep():
    result = subprocess.run(
        "dmesg | grep eth0",
        shell=True,
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
[   10.235000] eth0: Link is Up - 1000Mbps/Full
[   11.235000] eth0: NIC Link is Up
```

---

## Exercise 07 — Shell Expansion (wildcards)

### **What this exercise teaches**
- How wildcards (`*.py`) only work when `shell=True`
- How to list files using shell expansion
- Practical filtering of files in directories

### **Code**
```python
def ex07_shell_true_demo():
    result = subprocess.run(
        "ls -l *.py",
        shell=True,
        capture_output=True,
        text=True
    )
    print(result.stdout)
```

### **Expected Output**
```
-rw-r--r-- 1 root root 1200 ex01_run_ls.py
-rw-r--r-- 1 root root  890 ex02_capture_error.py
```

---

## Exercise 08 — Timeout Handling

### **What this exercise teaches**
- How to abort long-running commands
- How to catch `TimeoutExpired`
- Good for automation safety (prevent hanging scripts)

### **Code**
```python
def ex08_timeout():
    try:
        subprocess.run(["sleep", "10"], timeout=2)
    except subprocess.TimeoutExpired:
        print("Command timed out!")
```

### **Expected Output**
```
Command timed out!
```

---

# Summary of Skills Learned

| Skill | Example Exercise |
|-------|------------------|
| Running commands | ex01 |
| Handling errors | ex02 |
| Performing ping sweeps | ex03 |
| Parsing command output | ex04 |
| Handling multi-line results | ex05 |
| Using pipelines | ex06 |
| Using shell features | ex07 |
| Timeouts | ex08 |

You should practice each function until you can explain:

- What it does  
- Why it works  
- How it helps network automation  
- How to modify it for real environments  

