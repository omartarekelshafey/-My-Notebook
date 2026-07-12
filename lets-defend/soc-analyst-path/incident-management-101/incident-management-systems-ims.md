# Incident Management Systems (IMS)

## Incident Management System (IMS)

**An Incident Management System (IMS)** is an integrated software platform designed to enable security operations center (SOC) teams to organize, track, log, and manage the entire lifecycle of security incidents from initial detection to final resolution and post-incident analysis.

**Core Capabilities of an IMS:**

* Centralization: It acts as a single pane of glass that aggregates alerts from various security controls (like SIEM, EDR, and NDR), preventing analyst fatigue across multiple consoles.
* Ticketing & Lifecycle Tracking: It converts incoming security alerts into trackable cases or tickets, establishing explicit severity levels and ownership.
* Workflow Automation (Playbooks): It provides step-by-step guided procedures (Playbooks) tailored to specific attack types, ensuring standard operating procedures are followed during containment and eradication.
* Collaboration & Auditing: It allows security analysts to collaborate, share digital evidence, log investigation notes, and maintain an immutable audit trail for compliance.
* Metrics & Reporting: It tracks key performance indicators (KPIs) such as Mean Time to Detect (MTTD) and Mean Time to Respond (MTTR) to measure and optimize the efficiency of the security posture

## How an IMS Works

The platform coordinates multiple security components into a structured investigative workflow:

* Data Entry: To initiate a record on the IMS platform, security data must first be fed into it. This data flow can directly originate from a SIEM or other deployed security products.
* Case Creation: Once the data flow is established, a ticket or case is created on the IMS. For example, inside the LetsDefend Monitoring page, clicking the "Create Case" button on an alert in the "Investigation Channel" generates a new record inside the IMS (Case Management).
* Threat Intelligence Integration: If the IMS is integrated with Threat Intelligence platforms, the data within the case is enriched automatically, allowing for rapid response. For instance, if a suspicious domain like "letsdefend.io" is tied to an incident, the system automatically queries its reputation and presents it to the analyst. Without this integration, the SOC analyst must manually query open-source platforms like VirusTotal.
* SOAR Coordination: Security Orchestration, Automation, and Response (SOAR) products offer deep integration with other infrastructure controls like Firewalls, IPS, WAF, Proxies, and Email Security products. If an analyst verifies that a domain is harmful and needs to prevent access across the enterprise, they can utilize SOAR to instantly block the domain via the corporate proxy.
* Incident Closure: After data transmission, threat intelligence enrichment, and remediation actions are successfully executed across the coordinated platforms, the alert is closed by the analyst.

