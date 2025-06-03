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

- **Explanation**:  
  - **Nmap Scan**: Scans the network to find out which ports and services are open on the target.
  - The IP address `10.10.x.x` should be replaced with the actual IP of the target.

---
📝 Final README.md (Copy-Paste This Into Your File)
markdown
Copy
Edit
# 🏢 TryHackMe: Attacktive Directory

This is my write-up and notes for the **Attacktive Directory** room on TryHackMe.  
This room focuses on Windows Active Directory and how attackers can enumerate and exploit it.

---

## 🔍 Initial Nmap Scan

I started by scanning the target with `nmap`:

```bash
nmap -sC -sV -oN initial.txt 10.10.x.x
Key Services Found:
Port 88 – Kerberos

Ports 135, 139, 445 – SMB

Port 389 – LDAP

These ports are common in Windows domain environments.

🗂️ SMB Enumeration
🔸 Using enum4linux
I used enum4linux to get usernames and group info:

bash
Copy
Edit
enum4linux -a 10.10.x.x
This gave me a list of domain users and groups.

🔸 Using rpcclient
I also used rpcclient to enumerate more user info.

Command:

bash
Copy
Edit
rpcclient -U "" 10.10.x.x
When asked for a password, I just pressed Enter for anonymous login.

Inside the prompt, I typed:

bash
Copy
Edit
enumdomusers
This listed domain users like:

pgsql
Copy
Edit
user:[svc-admin] rid:[0x457]
user:[backup] rid:[0x460]
These usernames are helpful for password attacks or Kerberoasting.

🔸 Using smbclient
I listed shared folders:

bash
Copy
Edit
smbclient -L \\\\10.10.x.x\\
Then I connected to the share:

bash
Copy
Edit
smbclient \\\\10.10.x.x\\<sharename>
This helped access public or misconfigured shares.

🧪 Next Steps (Privilege Escalation, Kerberoasting, etc.)
After enumeration, I continued with:

AS-REP Roasting (if no preauth needed)

Kerberoasting using GetUserSPNs.py

Password cracking using john or hashcat

evil-winrm for remote shell access

🧰 Tools Used
nmap

enum4linux

rpcclient

smbclient

Impacket

john / hashcat

evil-winrm

🧠 What I Learned
How to enumerate Active Directory using SMB and LDAP

How to identify potential usernames

How to access SMB shares

Introduction to Kerberoasting and privilege escalation in Windows

✍️ Author
Tanmoy Daw
GitHub: @tanmoydaw26

yaml
Copy
Edit

---

## ✅ What to Do Next:

1. Open your cloned folder (`tryhackme-attacktive-directory`)  
2. Open `README.md` using Notepad  
3. Paste the above content and **Save**  
4. Then open **Git Bash** in that folder and run:

```bash
git add README.md
git commit -m "Complete writeup for Attacktive Directory"
git push origin main
