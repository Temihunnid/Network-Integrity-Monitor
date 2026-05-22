# Network-Integrity-Monitor
netwatch is a lightweight network integrity monitor that detects unauthorized changes across hosts and ports on IPs, hostnames, or CIDR subnets.

# steps by steps process 
create a file and write a python code that will help Detects unauthorized changes in your network: new devices, port shifts, missing hosts and name it netwatch.

NETWATCH — BEGINNER'S CODE EXPLANATION Understanding the code, line by line (simply)

Think of netwatch like a security guard for your network.
The first time it works, it takes a photo of everyone on
the network and remembers them. Every time after that, it
checks if anyone new showed up, someone left, or if something
about them changed.

----------------------------------------------------------------
SECTION 1 — IMPORTS (Lines 1–17)
----------------------------------------------------------------
``` import argparse
    import hashlib
    import json
    import os
    import socket
    import subprocess
    import sys
    import time
    from concurrent.futures import ThreadPoolExecutor, as_completed
    from datetime import datetime
    from pathlib import Path
 ```

# What is this?
These are "imports" — they are built-in Python toolboxes that we borrow to avoid writing everything from scratch.

What each one does (simply):

argparse   → Lets users type commands like "init", "check",
                 "update" in the terminal. It reads what the
                 user typed and understands it.

hashlib    → A tool that creates a unique fingerprint
                 (called a hash) from any data. Like a
                 human fingerprint — no two are the same.
                 We use SHA-256, a very secure type of hash.

json       → Lets us save and read data in a neat format
                 (like a structured notepad). This is how
                 baselines are stored on disk.

socket     → Lets the script "knock" on ports of other
                 computers to see if they are open or closed.
                 Like knocking on a door to see if someone
                 answers.

subprocess → Lets Python run other terminal commands.
                 We use this to run the "ping" command.

sys        → Gives us control over the script itself.
                 For example, sys.exit() stops the script
                 when something goes wrong.

ThreadPoolExecutor → Lets us scan many computers AT THE
                 SAME TIME instead of one by one. Like having
                 64 helpers knocking on doors simultaneously.

datetime   → Gives us the current date and time, so we
                 can record WHEN the baseline was created.

Path       → Makes it easier to work with file paths and
                 folders on any operating system.


# SECTION 2 — CONFIGURATION (Lines 20–32)

```BASELINE_DIR = Path.home() / ".netwatch" / "baselines"
    COMMON_PORTS = [21, 22, 23, 25, 53, 80, 110, 143, 443,
                    445, 3306, 3389, 5432, 6379, 8080, 8443]

    RESET  = "\033[0m"
    RED    = "\033[91m"
    GREEN  = "\033[92m"
    YELLOW = "\033[93m"
    CYAN   = "\033[96m"
    BOLD   = "\033[1m"
    DIM    = "\033[2m"
```

What is this?
    These are settings that control how the tool behaves.

BASELINE_DIR:
    This is the folder where netwatch saves its "photos"
    (baseline files). On Kali it will be:
        /root/.netwatch/baselines/
    The dot (.) at the start makes it a hidden folder.

COMMON_PORTS:
    A list of popular port numbers that the tool checks
    by default. Each number represents a "door" on a
    computer that a specific service uses.

Port 22   → SSH (remote login)

Port 80   → HTTP (websites)

Port 443  → HTTPS (secure websites)

Port 3306 → MySQL (database)

Port 3389 → RDP (Windows remote desktop) and more.

Color codes (RED, GREEN, etc.):

These are special codes that make the terminal output

colorful. For example, RED text for warnings and

GREEN text for success messages. They are not actual

colors — they are escape characters the terminal understands.


# SECTION 3 — HELPER FUNCTIONS (Lines 35–65)

```def baseline_path(target):
    def load_baseline(target):
    def save_baseline(target, data):
    def fingerprint(data):
    def ts():
```
What is a "function"?
A function is a mini-program inside the main program.
You give it something, it does a job, and gives
something back. Think of it like a vending machine —
you put in money (input), it gives you a snack (output).

baseline_path(target):
Takes a target like "192.168.1.0/24" and converts it into a safe filename like "192-168-1-0_24.json".Slashes and dots are replaced because filenames can'tcontain those characters.

load_baseline(target):
Opens the saved baseline file for a target and reads it into Python so we can compare it later. If no file exists yet, it returns nothing (None).

save_baseline(target, data):
Saves the current scan results into a JSON file. This is the "photo" the security guard takes.

fingerprint(data):
Takes all the scan data, converts it to text, then runs SHA-256 hashing on it to create a unique code.

Example:
Data:  {"192.168.1.1": {"ports": [22, 80]}}
Hash:  a3f5c8d2e1b9...  (long unique string)

If even ONE character in the data changes, the hash will be completely different. This is how we know if someone tampered with the baseline file itself.

ts():
    Short for "timestamp". Simply returns the current
    date and time as a readable string.
    Example output: "2026-05-22 14:30:00"


# SECTION 4 — NETWORK SCANNING FUNCTIONS 

    def ping(ip):
    def resolve(ip):
    def scan_port(ip, port):
    def scan_host(ip, ports):
    def expand_cidr(cidr):
    def do_scan(targets, ports, workers):
    ```







move the file to /usr/local/bin/
``` bash
sudo mv netwatch /usr/local/bin/
```

exicute the file
``` bash
chmod +x netwatch
 ```

run the file using a designated ip address
```bash
netwatch (ip adder)
 ```


