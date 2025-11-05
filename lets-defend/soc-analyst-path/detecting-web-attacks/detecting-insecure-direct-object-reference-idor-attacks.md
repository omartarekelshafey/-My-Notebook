# Detecting Insecure Direct Object Reference (IDOR) Attacks

## What is IDOR?

Insecure Direct Object Reference (IDOR) is a type of access-control vulnerability that happens when an application uses user-supplied identifiers (like IDs, filenames, or keys) to fetch objects but fails to check whether the requesting user is actually authorized to access that object. An attacker who can change those identifiers may read, modify, or delete data that belongs to other users.&#x20;

IDOR, or "Broken Access Control", is the number one web application vulnerability listed in the 2021 OWASP.\
Broken Access Control (which includes IDOR issues) was ranked as the top risk in the OWASP Top 10 for 2021 because many applications fail to enforce proper authorization checks across object access. (

## How IDOR Works

IDOR is not primarily about input sanitization: it’s about missing or incorrect authorization checks. The attacker modifies parameters in the request (for example changing `id=1` to `id=2`) to point to resources they should not access. If the server returns the resource without verifying permissions, the attacker gains unauthorized access.&#x20;

## **How Attackers Take Advantage of IDOR Attacks**

What an attacker can do is limited by the scope of an IDOR vulnerability. However, the most common areas are usually pages where a user's information is received. If an attacker were to exploit an IDOR vulnerability, they could:

* Steal personal information
* Access unauthorized documents&#x20;
* Take unauthorized actions (such as deleting, modifying)

## How to Prevent IDOR

Always check that the person making the request is authorized to provide a secure environment without an IDOR vulnerability.

In addition, unnecessary parameters should be removed and only the minimum number of parameters should be taken from the user. If we think about the previous example, we don't need to get the "id" parameter. Instead of getting the "id" parameter from the user, we can use the session information to identify the person who made the request.

