# Detecting Command Injection Attacks

## Command Injection — Summary

### **Definition**

Command injection occurs when untrusted user input is passed directly to an operating-system shell (or command interpreter) without proper validation or sanitization, allowing an attacker to execute arbitrary OS commands.

### **How it works (simple example)**

A web app builds a shell command like:\
`cp <filename> /tmp`\
If an attacker supplies a filename such as `letsdefend; ls; .txt`, the shell interprets `;` as a command separator and executes `ls` (and possibly other injected commands) with the web app’s user privileges.

### **How attackers exploit it**

They craft input that injects shell metacharacters (e.g., `;`, `&&`, `|`, backticks) or other payloads that alter the intended command flow and force execution of attacker-chosen commands.

### **Prevention / Best practices**

1. **Never trust user input** — validate and sanitize everything (filenames, parameters).
2. **Least privilege** — run web applications with the minimum required privileges.
3. **Isolate the app** — use containers, VMs, or sandboxes to limit blast radius.

