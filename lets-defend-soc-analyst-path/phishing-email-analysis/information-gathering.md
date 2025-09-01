# Information Gathering

**Spoofing** is when attackers send emails that appear to come from a trusted source. This is possible because email systems don't always enforce authentication by default.

To prevent spoofing, several protocols are used:

* **SPF** (Sender Policy Framework)
* **DKIM** (DomainKeys Identified Mail)
* **DMARC** (Domain-based Message Authentication, Reporting & Conformance)

Tools like Mxtoolbox help check these records and determine if an email is spoofed. You can also verify the **SMTP IP address** using Whois to see if it belongs to a legitimate organization.

To analyze a phishing attack, multiple parameters should be checked through the mail gateway, such as:

**sender address ex** (info@letsdefend.io)

**SMTP IP address** ex (192.168.1.5)

**Domain base** ex @letsdefend.io

**Username variations** ex let's defend

**Email subject line**&#x20;

Other important data include the **number of emails**, **recipients’ addresses**, and **timestamps**. If the same recipients are being targeted repeatedly, it might indicate that their emails were leaked (possibly on platforms like PasteBin).

Attackers may gather email addresses using tools like **theHarvester** on Kali Linux. Publicly sharing personal emails online increases the risk of being targeted.

