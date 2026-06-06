# CTF Writeups

Documented writeups from CTF platforms, vulnerable machines and local lab exercises.

## Purpose

This repository contains notes, methodology and technical walkthroughs from legal and authorized training environments.

The goal is to document the learning process, keep evidence organized and build repeatable methodology for enumeration, exploitation, privilege escalation and defensive analysis.

## Structure

```text
ctf-writeups/
├── dockerlabs/
├── portswigger/
├── vulnhub/
├── tryhackme/
├── hackthebox/
├── local-labs/
└── templates/
```

## Platforms

- `dockerlabs`: local vulnerable machines based on Docker.
- `portswigger`: PortSwigger Web Security Academy labs.
- `vulnhub`: downloadable VulnHub machines.
- `tryhackme`: TryHackMe rooms and labs.
- `hackthebox`: Hack The Box machines and challenges.
- `local-labs`: personal local vulnerable labs.

## Templates

Available templates:

- `templates/ctf_dockerlabs_full_template.md`  
  Full writeup template for DockerLabs, CTF machines and local vulnerable labs.

Use this template when documenting a new machine or lab under:

```text
ctf-writeups/dockerlabs/<machine-name>/
ctf-writeups/vulnhub/<machine-name>/
ctf-writeups/tryhackme/<room-name>/
ctf-writeups/hackthebox/<machine-name>/
ctf-writeups/local-labs/<lab-name>/
```

## Writeup folder format

Each machine or lab should use this structure when possible:

```text
machine-name/
├── README.md
├── nmap/
├── web/
├── fuzzing/
├── exploit/
├── payloads/
├── privesc/
├── loot-redacted/
├── screenshots/
└── notes.md
```

## Writeup sections

Each writeup should include:

```text
# Machine / Lab Name

## Summary
Brief description of the machine, platform and objective.

## Scope
Authorized lab environment only.

## Target
Platform, difficulty, target IP, date and status.

## Enumeration
Nmap results, service discovery and initial findings.

## Web Analysis
Technologies, directories, parameters, forms and interesting behavior.

## Fuzzing
Gobuster, FFUF or other content discovery results.

## Exploitation
Vulnerability, vector, commands used and result.

## Privilege Escalation
Local enumeration, misconfiguration and escalation path.

## Payloads
Payloads observed or used, sanitized if needed.

## Evidence
Relevant command outputs, screenshots and notes.

## Defensive Notes
How the issue could be detected, mitigated or hardened.

## Lessons Learned
Technical takeaways from the lab.

## Disclaimer
Educational and authorized lab use only.
```

## Rules

- Authorized labs only.
- No real credentials.
- No active third-party targets.
- No unauthorized systems.
- No tokens, cookies, API keys or private keys.
- No dumps, leaks or sensitive data.
- No flags or secrets unless redacted.
- No malware binaries.
- No unnecessary weaponization.
- Defensive notes should be included whenever possible.

## Recommended commands

### Workspace

```bash
mkdir -p nmap web fuzzing exploit payloads privesc loot-redacted screenshots
```

### Ping

```bash
ping -c 4 <TARGET_IP>
```

### Nmap all ports

```bash
nmap -p- --open --min-rate 5000 -n -Pn <TARGET_IP> -oN nmap/all_ports.txt
```

### Nmap services

```bash
nmap -sC -sV -p <PORTS> <TARGET_IP> -oN nmap/services.txt
```

### Web headers

```bash
curl -i http://<TARGET_IP>/
```

### Web fingerprint

```bash
whatweb http://<TARGET_IP>/
```

### Gobuster

```bash
gobuster dir -u http://<TARGET_IP>/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -x php,txt,html,bak -o fuzzing/gobuster_common.txt
```

### FFUF

```bash
ffuf -u http://<TARGET_IP>/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt -mc all -o fuzzing/ffuf_common.md -of md
```

### FFUF with size filter

```bash
ffuf -u http://<TARGET_IP>/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt -fs <SIZE> -mc all -o fuzzing/ffuf_filtered.md -of md
```

## Focus

- Enumeration
- Web exploitation
- Service analysis
- Payload understanding
- Privilege escalation
- Linux basics
- Windows basics
- Reporting methodology
- Defensive thinking

## Publishing checklist

Before publishing a writeup:

- [ ] Scope is clear.
- [ ] No real credentials are included.
- [ ] No tokens or cookies are included.
- [ ] No sensitive screenshots are included.
- [ ] Flags are redacted if needed.
- [ ] Target is a legal lab or CTF.
- [ ] Commands are documented.
- [ ] Evidence is organized.
- [ ] Defensive notes are included.
- [ ] Lessons learned are included.

## Disclaimer

This repository is for educational, defensive and authorized lab use only.

Do not use any material from this repository against systems you do not own or do not have explicit permission to test.

**Menos humo, más evidencia.**
