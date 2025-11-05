# Detecting Command Injection Attacks

## **Definition**

Command injection occurs when untrusted user input is passed directly to an operating-system shell (or command interpreter) without proper validation or sanitization, allowing an attacker to execute arbitrary OS commands.

## **How it works (simple example)**

A web app builds a shell command like:\
`cp <filename> /tmp`\
If an attacker supplies a filename such as `letsdefend; ls; .txt`, the shell interprets `;` as a command separator and executes `ls` (and possibly other injected commands) with the web app’s user privileges.

## **How attackers exploit it**

They craft input that injects shell metacharacters (e.g., `;`, `&&`, `|`, backticks) or other payloads that alter the intended command flow and force execution of attacker-chosen commands.

## **Prevention / Best practices**

1. **Never trust user input** — validate and sanitize everything (filenames, parameters).
2. **Least privilege** — run web applications with the minimum required privileges.
3. **Isolate the app** — use containers, VMs, or sandboxes to limit blast radius.



## **Detecting Command Injection Attacks**

### **Impact & Detection Overview:**

Command injection is a highly critical vulnerability. If exploited without being detected, it can cause major financial and reputational damage to the affected organization.

### **How to Detect Command Injection Attacks:**

* **Check every part of the web request:** Vulnerabilities may appear anywhere — in URLs, headers, query strings, POST bodies, file names, or cookies.
* **Search for terminal-related keywords or symbols:** Look for command names or shell operators like `dir`, `ls`, `cp`, `cat`, `type`, `;`, `&&`, `` ` ``, and `|`.
* **Recognize common payloads:** Attackers often use reverse shell payloads or stagers. Knowing these patterns helps detect and respond faster

#### Detection Example

Example HTTP request:

```
GET / HTTP/1.1
Host: yourcompany.com
User-Agent: () { :;}; echo "NS:" $(</etc/passwd)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close
```

In this request, the suspicious part is in the **User-Agent** header. Instead of normal browser information, it contains a **Bash payload** using the pattern `() { :;};`, followed by a command that reads the `/etc/passwd` file and sends it back with the prefix `NS:`.\
This request was captured during the exploitation of the **Shellshock** vulnerability.

***

## What is Shellshock?

**Shellshock** is a group of severe vulnerabilities discovered in **Bash** in 2014 (notably **CVE-2014-6271** and related ones).\
It occurs because Bash incorrectly interprets certain environment variables that look like function definitions.\
When such a variable contains extra commands after the function, Bash executes them unintentionally, leading to **remote code execution**.

Because Bash is widely used on Unix/Linux systems, this vulnerability had a huge global impact.

\
