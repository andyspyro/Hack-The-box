# Valentine

> **Status:** User access obtained  
> **Verified account:** `hype`  
> **Root status:** Not claimed

Valentine gave me practice with an older Linux target, SSH key handling, compatibility issues, Bash history, and tmux.

## SSH access

I recovered an SSH key during the lab.

The key needed restrictive local permissions before OpenSSH would use it:

```bash
chmod 600 <key-file>
```

The target was also old enough that I had to account for RSA compatibility on the client side.

My retained screenshot shows a successful SSH session as:

```text
hype@Valentine:~$
```

## Local enumeration

After login I checked the home directory and Bash history.

The retained history includes tmux commands, which gave me a clear privilege escalation lead to investigate.

## Heartbleed context

The machine involves the Heartbleed vulnerability and leaked TLS process memory as part of the lab path.

I keep the public notes focused on the parts I personally retained and verified rather than reproducing secret material from the exercise.

## Current status

I can support user access as `hype` and the tmux lead.

I do not have enough retained evidence to claim a confirmed root shell, so I do not mark the machine completed.
