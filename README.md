# LAB 3 – PwntillDawn Walkthrough (10.150.150.12)

## Overview
This lab demonstrates a basic penetration testing process using Nmap and Metasploit to identify vulnerabilities, exploit them, and gain access to a target machine.

Target IP: 10.150.150.12

---

## Step 1: Network Scanning (Host Discovery)

### Command:
sudo nmap -sn 10.150.150.0/24

### Purpose:
This command is used to scan the entire subnet to identify which hosts are active.

### Explanation:
- `-sn` performs a ping scan only (no port scanning)
- It is fast and suitable for initial network discovery

### Output:
The result shows a list of active IP addresses. From the output, the target machine (10.150.150.12) is identified as alive.

---

## Step 2: Port Scanning & Service Enumeration

### Command:
nmap -sC -sV -Pn 10.150.150.12

### Purpose:
To identify open ports, running services, and potential vulnerabilities on the target system.

### Explanation:
- `-sC` runs default scripts to detect common vulnerabilities
- `-sV` detects the version of services
- `-Pn` skips host discovery and assumes the host is online

### Output Findings:
- Port 21 → FTP
- Port 22 → SSH
- Port 16992 → Intel AMT

The scan also reveals that FTP is running **vsftpd version 2.0.8**, which is outdated.

### Why this matters:
Outdated services often contain known vulnerabilities that attackers can exploit.

---

## Step 3: Search for Exploits

### Command:
msfconsole
search vsftpd

### Purpose:
To check whether there are known exploits available for the detected service.

### Explanation:
- `msfconsole` launches Metasploit Framework
- `search vsftpd` searches for related exploits

### Output:
An exploit named **vsftpd_234_backdoor** is found.

### Why this matters:
This confirms that the FTP service is vulnerable and can potentially be exploited.

---

## Step 4: Configure the Exploit

### Command:
use 1
show options
set RHOSTS 10.150.150.12

### Purpose:
To configure the exploit with the correct target details.

### Explanation:
- `use 1` selects the exploit module
- `show options` displays required parameters
- `set RHOSTS` sets the target IP address

### Output:
The exploit is successfully configured and ready to run.

---

## Step 5: Execute the Exploit

### Command:
run

### Purpose:
To execute the exploit against the target machine.

### Output:
If successful, a shell session will be opened.

### Meaning:
This indicates that access to the target system has been successfully obtained.

---

## Step 6: Verify Access & Retrieve the Flag

### Commands:
id
ls
cat FLAG1.txt

### Purpose:
To verify access privileges and retrieve the flag.

### Explanation:
- `id` shows the current user and privileges
- `ls` lists files in the directory
- `cat FLAG1.txt` displays the flag content

### Output:
- `id` confirms access to the system
- `ls` shows available files
- `cat` reveals the flag (final objective)

---

## Conclusion

In this lab, we successfully:
- Discovered active hosts using Nmap
- Identified open ports and services
- Detected a vulnerable FTP service
- Used Metasploit to exploit the vulnerability
- Gained shell access to the system
- Retrieved the flag

This shows how outdated services like vsftpd 2.0.8 can lead to system compromise.

---

## ⚠️ Disclaimer
This lab is conducted in a controlled environment for educational purposes only. Unauthorized access to systems is illegal.
