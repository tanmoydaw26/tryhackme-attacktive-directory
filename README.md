# 🏢 TryHackMe: Attacktive Directory

This repository contains my detailed write-up and steps for completing the **"Attacktive Directory"** room on TryHackMe. The goal of this room is to teach techniques for **Active Directory enumeration**, **Kerberoasting**, and **privilege escalation** within a Windows environment.

---

## 🧾 Room Information

- **Platform**: TryHackMe  
- **Room**: [Attacktive Directory](https://tryhackme.com/room/attacktivedirectory)  
- **Difficulty**: Medium  
- **Focus**: Active Directory, SMB enumeration, Kerberoasting, Privilege Escalation  
- **Status**: ✅ Completed

---

## 🛠️ Tools Used

Here is a list of the tools I used throughout the room:

- **Nmap** - For network scanning
- **Enum4linux** - For SMB enumeration
- **rpcclient** - To interact with Windows RPC service
- **CrackMapExec** - For further SMB enumeration and network interaction
- **Impacket's GetNPUsers.py and GetUserSPNs.py** - For Kerberoasting (extracting service account credentials)
- **John the Ripper** or **Hashcat** - For cracking the hashes obtained during enumeration
- **Evil-WinRM** - To interact with the target system after obtaining valid credentials

---

## 🔍 1. Enumeration

### Initial Nmap Scan

The first step was to scan the target machine for open ports and services. I used Nmap for this:

```bash
nmap -sC -sV -T4 -p- 10.10.x.x
