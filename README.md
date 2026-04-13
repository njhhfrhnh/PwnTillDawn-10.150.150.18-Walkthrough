# PwnTillDawn-10.150.150.18-Walkthrough
## Overview
This writeup documents the process of enumerating and exploiting the target machine `10.150.150.18` in a PwntillDawn lab. The objective is to identify vulnerabilities, gain access, and retrieve the flag.

---

## 1. Host Discovery

```bash
nmap -sn 10.150.150.0/24
Explanation
nmap → Network scanning tool
-sn → Ping scan (detects live hosts only, no port scan)
Purpose
Used to identify active machines in the network.
From the scan, the target 10.150.150.18 was discovered.
