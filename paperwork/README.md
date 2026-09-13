# Paperwork

> **Status:** Completed: user and root  
> **Type:** Authorized Hack The Box penetration test  
> **Proof:** Full retained penetration test report

Paperwork is the strongest completed offensive security example in this repo because I have a full report for the entire path from reconnaissance to root.

## Verified attack path

```text
HTTP and source review
        |
        v
custom printer service
        |
        v
command injection
        |
        v
shell as lp
        |
        v
localhost JetDirect style service
        |
        v
arbitrary file write
        |
        v
SSH as archivist
        |
        v
privileged UNIX socket
        |
        v
root
```

## 1. Reconnaissance

The retained report shows that I validated the HTB VPN, scanned the target, and identified SSH and HTTP first.

The web application needed the correct hostname before the useful content appeared.

## 2. Source review

The site exposed backend source code.

That source showed a custom LPD style printer service on another port and made the input path visible.

I wrote a Python client to submit a normal print job first so I knew the protocol was working before changing the input.

## 3. Command injection

The printer service used job data inside a shell command with `shell=True`.

That let controlled input change the operating system command and gave me a reverse shell as the low privilege `lp` service account.

### Fix

Do not invoke a shell for simple logging. Use direct file operations or fixed argument execution with `shell=False`.

## 4. Internal service discovery

From the first shell I checked processes and localhost listeners.

That exposed another printer related service bound to localhost and running as the `archivist` user.

## 5. Arbitrary file write

The internal service accepted a PJL file download path.

The path handling allowed traversal outside the intended printer storage area.

Because the service ran as `archivist`, I could write a public SSH key into that user's authorized keys file and then log in over SSH.

### Fix

Canonicalize the path, restrict writes to one directory, reject traversal, and avoid running the service as a normal human user.

## 6. Privilege escalation

From the `archivist` shell I found a management UNIX socket used by a root owned process.

The process passed open file descriptors with `SCM_RIGHTS`. A lower privilege client could receive a descriptor for privileged data.

That exposed a root credential and completed the lab.

### Fix

Restrict the socket, verify peer credentials, and never pass privileged descriptors to an untrusted lower privilege process.

## Findings

| Finding | Result |
|---|---|
| Backend source disclosure | Revealed the hidden service and unsafe logic |
| Command injection | Code execution as `lp` |
| Path traversal and arbitrary file write | Stable access as `archivist` |
| Privileged file descriptor leak | Root credential disclosure |
| Weak trust between local services | Let the first foothold become a full compromise |

## Tools

Nmap, Firefox, Python, Ncat, OpenSSH, `ssh-keygen`, PowerShell, WSL, Bash, `ps`, `ss`, and systemd service inspection.

## Evidence checked

My retained Paperwork report explicitly records the HTB scope, the command injection, shell as `lp`, the internal service running as `archivist`, the SSH key write, the UNIX socket issue, and confirmed root access.

Flags, private keys, passwords, and reusable secrets stay out of the public repo.
