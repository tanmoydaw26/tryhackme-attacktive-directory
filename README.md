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

