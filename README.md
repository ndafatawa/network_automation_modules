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

## 1️⃣ subprocess — Run Linux Commands from Python  
Used for:
- Ping sweeps
- OS commands
- Traceroutes
- Device discovery
- Parsing CLI utilities

📁 Folder: `subprocess_mastery/`

---

## 2️⃣ paramiko — SSH into network devices  
Used for:
- Sending configs (Arista, Cisco, FortiGate, JunOS)
- Gathering show outputs
- Backups

📁 Folder: `paramiko_ssh/`

---

## 3️⃣ os, sys, pathlib — File system control  
Used for:
- Directory creation
- Reading config files
- Working with paths
- CLI arguments

📁 Folder: `os_sys_pathlib/`

---

## 4️⃣ json, yaml, csv, re — Parsing data  
Used for:
- Device inventory
- Network models
- Parsing configs
- Rule extraction

📁 Folder: `parsing_and_data/`

---

## 5️⃣ ipaddress — IP logic  
Used for:
- Subnets
- Validation
- IP ranges
- Prefix calculations

📁 Folder: `ipaddress_module/`

---

## 6️⃣ concurrent.futures & multiprocessing  
Used for:
- Parallel SSH
- Parallel pings
- Faster network scanning

📁 Folder: `concurrency/`

---

## 7️⃣ argparse & logging  
Used for:
- Professional scripts
- Debug logs
- CLI automation tools

📁 Folder: `argparse_and_logging/`

---

# 🏁 Final Project  
**Discover subnet → SSH → Get hostname → Update /etc/hosts**

📁 `subprocess_mastery/final_project/`

---

#  Target Audience  
- Beginner → Intermediate Network Engineers  
- ACI / NX-OS / Arista / Juniper automation  
- Python learners  
- DevNet / Network+ automation students  

---

# ⚙ Requirements

Install dependencies:

```
pip install paramiko pyyaml
```

---
network-automation-python-core-modules/
│
├── README.md
│
├── subprocess_mastery/
│   ├── INTRODUCTION.md
│   ├── examples/
│   │   ├── ex01_run_ls.py
│   │   ├── ex02_capture_error.py
│   │   ├── ex03_devnull_ping.py
│   │   ├── ex04_shell_true_false.py
│   │   ├── ex05_timeout.py
│   │   ├── ex06_parse_ping_latency.py
│   │   ├── ex07_pipeline_demo.py
│   │   ├── ex08_ping_sweep.py
│   │   └── ex09_traceroute_parser.py
│   ├── final_project/
│   │   ├── discover_and_update_hosts.py
│   │   └── README.md
│   └── SOLUTIONS.md
│
├── paramiko_ssh/
│   ├── basics_ssh.md
│   ├── examples/
│   │   ├── simple_ssh_command.py
│   │   ├── ssh_send_config.py
│   │   ├── ssh_backup_show_run.py
│   │   └── ssh_parallel_devices.py
│   └── SOLUTIONS.md
│
├── os_sys_pathlib/
│   ├── os_basics.md
│   ├── pathlib_basics.md
│   └── examples/
│       ├── create_directories.py
│       ├── list_files.py
│       ├── env_variables.py
│       └── sys_arguments_demo.py
│
├── parsing_and_data/
│   ├── json_basics.md
│   ├── yaml_basics.md
│   ├── csv_basics.md
│   ├── regex_basics.md
│   └── examples/
│       ├── parse_json_inventory.py
│       ├── parse_yaml_devices.py
│       ├── parse_csv_vlans.py
│       └── regex_find_ip.py
│
├── ipaddress_module/
│   ├── ip_basics.md
│   └── examples/
│       ├── subnet_calculator.py
│       ├── validate_ip.py
│       └── generate_ip_range.py
│
├── concurrency/
│   ├── threading_basics.md
│   ├── futures_basics.md
│   ├── multiprocessing.md
│   └── examples/
│       ├── parallel_ping_sweep.py
│       ├── parallel_ssh_commands.py
│       └── cpu_parallel_demo.py
│
└── argparse_and_logging/
    ├── argparse_basics.md
    ├── logging_basics.md
    └── examples/
        ├── script_with_arguments.py
        └── logging_demo.py

# 👨‍💻 Author  Tawanda Ndafa
Created for deep learning and real-world network automation.
