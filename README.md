# Network Automation Python Core Modules 

This repository teaches the **essential Python modules** that every network automation engineer must master.

It includes:
- Full explanations
- Hands-on exercises
- Real-world automation scripts
- Final projects
- Ready-to-run examples

---

#  Modules Covered

## 1 subprocess — Run Linux Commands from Python  
Used for:
- Ping sweeps
- OS commands
- Traceroutes
- Device discovery
- Parsing CLI utilities

 Folder: `subprocess_mastery/`

---

## 2 paramiko — SSH into network devices  
Used for:
- Sending configs (Arista, Cisco, FortiGate, JunOS)
- Gathering show outputs
- Backups

 Folder: `paramiko_ssh/`

---

## 3 os, sys, pathlib — File system control  
Used for:
- Directory creation
- Reading config files
- Working with paths
- CLI arguments

 Folder: `os_sys_pathlib/`

---

## 4 json, yaml, csv, re — Parsing data  
Used for:
- Device inventory
- Network models
- Parsing configs
- Rule extraction

 Folder: `parsing_and_data/`

---

## 5 ipaddress — IP logic  
Used for:
- Subnets
- Validation
- IP ranges
- Prefix calculations

 Folder: `ipaddress_module/`

---

## 6 concurrent.futures & multiprocessing  
Used for:
- Parallel SSH
- Parallel pings
- Faster network scanning

 Folder: `concurrency/`

---

## 7 argparse & logging  
Used for:
- Professional scripts
- Debug logs
- CLI automation tools

 Folder: `argparse_and_logging/`

---

#  Final Project  
**Discover subnet → SSH → Get hostname → Update /etc/hosts**

 `subprocess_mastery/final_project/`

---

# ⚙ Requirements

Install dependencies:

```
pip install paramiko pyyaml
```

---
