# How I Work Through a Box

This is the process I use when I am working through an authorized Hack The Box machine.

It is not a checklist I follow blindly. The point is to keep myself from jumping between exploits without understanding what the target is doing.

## 1. Confirm the basics

Before troubleshooting an exploit, I check that the target is reachable and the HTB route is correct.

Typical checks:

```bash
ping -c 4 <TARGET>
ip addr
ip route
```

## 2. Enumerate services

I usually start with Nmap:

```bash
nmap -sC -sV <TARGET>
```

I care about the service, version, hostname requirements, certificate details, and anything that changes what I should test next.

## 3. Fix hostname issues early

If the target expects a virtual host, I add it locally and verify it before I spend time testing the wrong page.

## 4. Learn the normal request

Before changing input, I try the normal workflow.

That can mean submitting a harmless form, checking a cookie, sending a valid protocol request, or watching the request in Burp.

## 5. Follow controlled input

When source code or request details are available, I trace where input goes.

I pay the most attention when input reaches a shell command, SQL query, filesystem path, template, session decision, or privileged service.

## 6. Test one assumption at a time

If something fails, I check why before switching tools.

Questions I ask include:

* Did I get the expected cookie?
* Did the server redirect?
* Is the CSRF value correct?
* Did I hit the right virtual host?
* Is the service only listening on localhost?
* Is the input being parsed as text, a number, a path, or a command?

## 7. Enumerate again after access

A shell exposes a new attack surface.

Typical checks include:

```bash
whoami
id
hostname
pwd
ps aux
ss -lntp
systemctl
cat ~/.bash_history
```

I look for internal services, service accounts, writable files, unusual sockets, shell history, and anything running with more privilege than my current account.

## 8. Treat privilege escalation separately

Getting a shell is not the same as finishing the box.

I look at service ownership, filesystem permissions, local sockets, exposed credentials, shell history, and trust between local processes.

## 9. Record the reason, not just the command

For each useful finding I try to keep four things:

* what was vulnerable
* why it was vulnerable
* what access it gave me
* what would stop it

## 10. Keep public notes clean

I do not publish flags, passwords, private keys, session tokens, or reusable secrets.

The public writeups are there to show the process and the security issue, not every secret from the lab.
