# Introduction to the subprocess Module

The `subprocess` module allows Python to execute Linux commands the same way a user would enter them in the terminal.

It is the bridge between:
- Python (automation logic)
- Linux shell (system capabilities)

---

# Why Network Engineers Must Learn subprocess

✔ Ping sweeps  
✔ ARP table access  
✔ Interface status queries (`ip link`)  
✔ Linux routing table (`ip route`)  
✔ Grep-based filtering  
✔ Traceroutes  
✔ Searching logs  
✔ OS-level checks before automation  
✔ Running tools Python cannot replicate

---

# How subprocess works internally

When you call:

```python
result = subprocess.run(["ping", "-c", "1", "8.8.8.8"])
```

Python does the following:

1. Spawns a new process (child)
2. Executes the command in the OS
3. Waits for it to finish
4. Captures:
   - stdout
   - stderr
   - returncode
5. Returns a CompletedProcess object

---

# Key Concepts

## returncode
- 0 → SUCCESS  
- Non-zero → FAILURE  

## stdout
Normal output of the command  
Optional: must enable capture_output or PIPE

## stderr
Error output  
Used to detect failures

## DEVNULL
Throw away all output  
Used in ping sweeps

## shell=True
Executes the command in a real Linux shell  
Needed for pipelines or wildcards  
Use carefully (security concerns)

---

# Two Layers

## 1. subprocess.run() — Easy
Use for:
- normal commands
- capturing output
- silent execution
- timeout handling

## 2. subprocess.Popen() — Advanced
Use for:
- real-time logs
- interactive processes
- pipelines like `cmd1 | cmd2`

---

You must master these concepts before doing the exercises.
