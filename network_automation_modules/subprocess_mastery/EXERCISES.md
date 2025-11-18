import subprocess
import re

def ex01_run_ls():
    result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
    print(result.stdout)

def ex02_capture_error():
    result = subprocess.run(
        ["ls", "/does/not/exist"],
        capture_output=True,
        text=True
    )
    print("STDERR:", result.stderr)

def ex03_ping_sweep():
    for i in range(1, 10):
        ip = f"192.168.10.{i}"
        result = subprocess.run(
            ["ping", "-c", "1", "-W", "1", ip],
            stdout=subprocess.DEVNULL,
            stderr=subprocess.DEVNULL
        )
        print(ip, "UP" if result.returncode == 0 else "DOWN")

def ex04_latency_parser():
    result = subprocess.run(["ping", "-c", "1", "8.8.8.8"], capture_output=True, text=True)
    match = re.search(r"time=(\d+\.\d+)", result.stdout)
    print("Latency:", match.group(1) if match else "N/A")

def ex05_traceroute():
    result = subprocess.run(["traceroute", "-n", "8.8.8.8"], capture_output=True, text=True)
    print(result.stdout)

def ex06_pipeline_grep():
    result = subprocess.run("dmesg | grep eth0", shell=True, capture_output=True, text=True)
    print(result.stdout)

def ex07_shell_true_demo():
    result = subprocess.run("ls -l *.py", shell=True, capture_output=True, text=True)
    print(result.stdout)

def ex08_timeout():
    try:
        subprocess.run(["sleep", "10"], timeout=2)
    except subprocess.TimeoutExpired:
        print("Command timed out!")
