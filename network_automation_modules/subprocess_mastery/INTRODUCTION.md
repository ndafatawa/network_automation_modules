# Introduction to the subprocess Module

The `subprocess` module allows Python to execute Linux commands the same way a user would type them in the terminal.

It acts as a bridge between:

- Python (automation logic)
- Linux shell (system capabilities)

---

# Why Network Engineers Must Learn subprocess

- Ping sweeps
- ARP table access
- Interface status checks (`ip link`)
- Routing table inspection (`ip route`)
- Grep-based filtering of system logs
- Traceroutes
- Searching log files
- Performing OS-level checks before automation
- Running native Linux tools that Python alone cannot replace

---

# How subprocess works internally

Example:

```python
result = subprocess.run(["ping", "-c", "1", "8.8.8.8"])
```

Python performs the following steps:

1. Creates a new child process  
2. Runs the command in the Linux shell  
3. Waits for the command to finish  
4. Collects:
   - stdout
   - stderr
   - returncode
5. Returns a `CompletedProcess` object

---

# Key Concepts

## returncode
- `0` → success  
- Non-zero → failure  

## stdout
Normal output from the command.  
You must explicitly capture it using `capture_output=True` or `stdout=subprocess.PIPE`.

## stderr
The error output stream, used to detect failures and errors.

## DEVNULL
A special sink that discards all output, used for silent operations such as ping sweeps.

Example:

```python
stdout=subprocess.DEVNULL
stderr=subprocess.DEVNULL
```

## shell=True
Runs the command inside a real shell (`/bin/sh`).

Use only when needed for:
- pipelines  
- wildcards  
- environment expansion  

Not recommended for untrusted input.

---

# Two Layers of Subprocess

## 1. subprocess.run() — High Level
Used for:
- simple commands
- capturing output
- silent execution
- timeouts

## 2. subprocess.Popen() — Low Level
Used for:
- real-time log streaming
- interactive commands
- implementing pipelines manually (`cmd1 | cmd2`)
- long-running commands

---

You must understand all of these concepts before moving on to the exercises.
