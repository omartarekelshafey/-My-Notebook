# Static Analysis

* Email programs support **HTML** to make messages look attractive, but attackers exploit this to hide malicious URLs behind buttons or seemingly harmless text.
* A user may see a safe-looking link, but the real destination appears when hovering over the link.

<div align="left"><figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>

* In most **phishing attacks**, attackers register a new domain and use it within a few days. If the domain in the email is very new → it’s a strong phishing indicator.
*   We can use **VirusTotal** to analyze URLs in emails:

    * If the link/file has been analyzed before, VirusTotal shows old results instead of re-scanning.
    * This can be an advantage (faster results) and a disadvantage (results may be outdated).
    * For example, a domain scanned 9 months ago may appear harmless, but a fresh scan could reveal it as malicious.
    * Attackers sometimes check their domains on VirusTotal themselves to see the detection rate before launching an attack.

    <div align="left"><figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>
* **Static file analysis** in emails can provide insights into the file’s capabilities, but it is time-consuming. **Dynamic analysis** often provides quicker results.
* **Cisco Talos Intelligence** can be used to check the reputation of the **SMTP IP** that sent the email:
  * If the IP is blacklisted, it likely indicates the attack was carried out from a compromised server.
* The SMTP IP can also be checked on **VirusTotal** and **AbuseIPDB** to determine if it has a history of malicious activity.

<div align="left"><figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure></div>

