# Orion

> **Status:** In progress  
> **Platform:** Hack The Box  
> **Verified target detail:** Craft CMS 5.6.16

Orion turned into more of an exploit troubleshooting exercise than a "run the PoC and get a shell" box.

## What I verified

My retained HTB screenshot shows:

* Orion in Guided Mode
* Craft CMS version 5.6.16
* a Python file named `craftcms_final_payload.py`
* the guided objective involving the Adam user

Another retained screenshot shows the MySQL database password task completed. I am not publishing that credential.

## Public exploit troubleshooting

I found public Craft CMS RCE material and worked through why the script did not behave exactly as expected against the target.

I checked session state, cookies, CSRF values, redirects, and request flow instead of treating the script like a black box.

## Python work

I worked with Python and `requests.Session` while adjusting the request flow around Craft session handling and exploit state.

The useful part for me was reading the exploit code and checking each assumption against the real HTTP response.

## Current status

I recovered the database credential required by the guided task.

I do not have retained proof of the final user flag or root access, so the machine stays marked **in progress**.

## What I am not claiming

I am not calling Orion completed.

I am also not publishing the recovered credential, session values, or flags.
