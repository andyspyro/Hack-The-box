# CrossFitTwo

> **Status:** Enumeration and web analysis  
> **Platform:** OpenBSD  
> **Root status:** Not claimed

I did not finish CrossFitTwo, but I kept the enumeration work because it shows how I mapped the target before trying to force an exploit.

## Service enumeration

Nmap showed an unusual service on TCP 8953 that appeared related to Unbound control.

The certificate details helped confirm what the service was.

## Web stack

The HTTP responses identified OpenBSD httpd and PHP.

I also found a protected endpoint returning HTTP 403. That was useful because it confirmed the route existed even though I did not have the required access condition.

## Virtual hosts

The target served more than one hostname.

I added the required local name resolution and reached an employee site with a login page and password reset form.

## Password reset enumeration

I used curl to inspect how the password reset request was built.

The application returned a different response when the account existed.

I then used ffuf to automate the check and filtered out the normal "Unknown email address" response.

My retained screenshot shows that ffuf workflow against the password reset endpoint.

## Security issue

Different reset responses allow account enumeration.

A safer reset flow should return the same generic message whether the account exists or not. Rate limiting and monitoring would also help.

## Current status

I can support the enumeration, virtual host work, and password reset account enumeration.

I do not have retained proof of a completed compromise, so I leave the machine at this stage.
