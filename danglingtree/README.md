# DanglingTree

> **Status:** In progress  
> **Platform:** Windows focused Hack The Box lab  
> **Administrator status:** Not claimed

DanglingTree is one of the Windows labs I worked on. My retained notes reach credential discovery and access to another account, but not the final privilege escalation.

## Initial work

I worked from Windows, PowerShell, and WSL.

The early work included:

* target connectivity
* local hostname entries
* Nmap scanning
* IIS web inspection

The web application depended on the correct hostnames, so name resolution mattered before deeper testing.

## Burp and web requests

I used Burp Suite to inspect request methods, parameters, cookies, authentication behavior, and the endpoints the browser was calling.

## SmarterMail

A SmarterMail related component became part of the investigation.

I spent time working out how it fit into the target and what information around the service could help with account access.

## Logs and credentials

My retained notes show that log or audit information exposed data that led to credentials.

Those credentials worked for a second account, which changed the problem from initial access to privilege escalation.

## Current status

I am not marking the box complete.

I do not have a retained administrator or root result that I can stand behind, so the public page stops at the second account.

## Security point

Logs can become an attack surface if they expose usernames, commands, secrets, or other operational details to users who should not see them.
