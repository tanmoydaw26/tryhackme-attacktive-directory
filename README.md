# 🏢 TryHackMe: Attacktive Directory

This repository contains my detailed write-up and notes for the **Attacktive Directory** room on TryHackMe.

This room focuses on hands-on Windows Active Directory enumeration and exploitation, exploring common misconfigurations and techniques seen in real-world enterprise environments.

---

## 🧾 Room Info

- **Platform:** TryHackMe  
- **Room:** Attacktive Directory  
- **Difficulty:** Medium  
- **Focus:** Active Directory, SMB enumeration, Kerberoasting, Privilege Escalation  
- **Status:** ✅ Completed

---

## 🛠️ Tools Used

- `nmap`
- `smbclient`
- `enum4linux`
- `rpcclient`
- `crackmapexec`
- `impacket` (GetNPUsers.py, GetUserSPNs.py)
- `john` or `hashcat`
- `evil-winrm`

---

## 🔍 1. Enumeration

### 🔎 Nmap Scan

```bash
nmap -sC -sV -T4 -p- 10.10.x.x
```
- **Explanation**:  
  - Scans the network to find out which ports and services are open on the target.
  - Replace `10.10.x.x` with the actual IP address of the target.

**Key Services Found:**
- **Port 88** – Kerberos  
- **Ports 135, 139, 445** – SMB  
- **Port 389** – LDAP  
These ports are common in Windows domain environments.

---

### 🗂️ SMB Enumeration

#### 🔸 Using enum4linux

```bash
enum4linux -a 10.10.x.x
```
- Retrieves a list of domain users and groups.

#### 🔸 Using rpcclient

```bash
rpcclient -U "" 10.10.x.x
```
- On the password prompt, just press Enter for anonymous login.
- Inside the rpcclient prompt, run:

```bash
enumdomusers
```
- Lists domain users, e.g.:
  ```
  user:[svc-admin] rid:[0x457]
  user:[backup] rid:[0x460]
  ```
- These usernames are useful for password attacks or Kerberoasting.

#### 🔸 Using smbclient

```bash
smbclient -L \\\\10.10.x.x\\
```
- Lists all available shared folders.

To connect to a share:
```bash
smbclient \\\\10.10.x.x\\<sharename>
```
- Allows access to public or misconfigured shares.

---

## 🧪 Next Steps (Privilege Escalation, Kerberoasting, etc.)

- **AS-REP Roasting** (if no preauth is required)
- **Kerberoasting** using GetUserSPNs.py
- **Password Cracking** using john or hashcat
- **Remote Shell Access** with evil-winrm

---

## 🧰 Tools Used

- nmap
- enum4linux
- rpcclient
- smbclient
- Impacket
- john / hashcat
- evil-winrm

---

## 🧠 What I Learned

- How to enumerate Active Directory using SMB and LDAP
- How to identify potential usernames
- How to access SMB shares
- Introduction to Kerberoasting and privilege escalation in Windows

---

## ✍️ Author

**Tanmoy Daw**  
GitHub: [@tanmoydaw26](https://github.com/tanmoydaw26)

---

> _Feel free to fork or star this repo if you found it useful!_
