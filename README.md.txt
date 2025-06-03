# 🏢 TryHackMe: Attacktive Directory

This repository contains my detailed write-up of the **"Attacktive Directory"** room on TryHackMe. This room focuses on **Active Directory enumeration and exploitation**, using common misconfigurations and techniques seen in real-world enterprise environments.

---

## 🧾 Room Info

- **Platform**: TryHackMe  
- **Room**: [Attacktive Directory](https://tryhackme.com/room/attacktivedirectory)  
- **Difficulty**: Medium  
- **Focus**: Active Directory, SMB enumeration, Kerberoasting, Privilege Escalation  
- **Status**: ✅ Completed

---

## 🛠️ Tools Used

- `nmap`
- `smbclient`
- `enum4linux`
- `rpcclient`
- `crackmapexec`
- `impacket` (`GetNPUsers.py`, `GetUserSPNs.py`)
- `john` or `hashcat`
- `evil-winrm`

---

## 🔍 1. Enumeration

### 🔎 Nmap Scan
```bash
nmap -sC -sV -T4 -p- 10.10.x.x
