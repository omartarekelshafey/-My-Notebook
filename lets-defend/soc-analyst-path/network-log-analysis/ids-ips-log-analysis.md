# IDS/IPS Log Analysis

### IDS vs IPS Concept

الـ Firewall  بيبص على البيانات من بره (IPs & Ports)  بس. أما الـ IDS/IPS فبيتميز بقدرته على فحص محتوى بالكامل (Deep Packet Inspection) ليعرف هل موجود  (Malware/Exploits) ولا لا .

#### الفرق بينهم

* نظام الـ IDS (Intrusion Detection System): يكتفي بـ  Detection
* نظام الـ IPS (Intrusion Prevention System): يقوم بـ Detection & Prevention

### Following information should be investigated in details when analyzing IDS/IPS logs

\- The direction of attack (inbound or outbound) should be checked.

\- The event severity level should be checked. Levels are usually set as low, medium, high, critical. High and critical levels indicate that activity is more important, quick action is required, and a false positive is less likely.

\- A different signature trigger state should be checked between the same source and target. Triggering different signatures means that the severity level of the event should be raised higher and a faster action should be taken. The event is resolved within the service level agreement (SLA) depending on its severity level in case of following situations like:

&#x20;       \- If a single signature is triggered,

&#x20;       \- there are no different requests from the relevant source,

&#x20;       \- there is no different accept in the firewall logs.

\- Is the port/service specified in the attack detail running on the target port? If it is running, the event level should be raised to the critical level, and the target system should be checked for infection. It should also be checked whether a response has been returned to the relevant system from the source. If the answer is no, blocking the attacking IP address as a precaution would be an appropriate action.

\- Is the action taken just detection or has it been blocked as well? If the attack is blocked and there are no other requests from the same IP address on the firewall, we can wait a little longer for taking the action. However, if the action taken for the attack is only a detection, then other similar requests should be reviewed and block action should be applied if the content of the requests coming from the IP address is not false positive.

### Attacks Detected by IDS/IPS

* &#x20;(Port & Vulnerability Scanning).
* &#x20;(Code Injection) , (Brute-Force).
* (DoS/DDoS).
* &#x20;(Trojan & Botnet activities).

