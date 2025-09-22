# Dynamic Analysis

**Checking URLs and files in an email:**

* URLs and files should always be verified for safety before running them, to prevent data theft or malware infection.
* They should be executed in **sandbox environments** to monitor system changes and determine if they are harmful.

**Methods and tools:**

* Online browsers like **Browserling** can be used to quickly check URLs.
  * **Advantage:** Protects against potential **zero-day vulnerabilities** in browsers, since the site isn’t opened on your own computer.
  * **Disadvantage:** If the website downloads a malicious file, you won’t be able to execute it, which may interrupt the analysis.
* Before visiting links, always check if the **URL contains sensitive information**.
  * Example: If the URL includes the user’s **email address** as a parameter, clicking it confirms to the attacker that the email account is valid, even without entering a password.
  * The attacker can then target verified users later using **social engineering attacks**.
  * Therefore, sensitive data (like email addresses) should be modified before accessing such sites.

**Sandbox environments:**

* Allow you to examine suspicious files and websites safely without infecting your system.
* Available both free and paid. Commonly used sandboxes:
  * **VMRay**
  * **JoeSandbox**
  * **AnyRun**
  * **Hybrid Analysis (Falcon Sandbox)**

**Key notes:**

* Malware may delay its execution to evade detection, so you need to wait before concluding a file is harmless.
* The absence of URLs or files in an email does not mean it is safe — attackers may embed malware inside **images** to bypass analysis tools.
