# it security basics

A comprehensive conceptual overview of the key defensive protection areas within an organization.

## General Introduction

Protecting any infrastructure from cyberattacks, particularly ransomware attacks, does not rely on a single tool or a single measure. Instead, it relies on an integrated set of defensive controls covering different aspects of an organization's operations: from managing user privileges, through backups, internet browsing protection, asset inventory, network monitoring, patching, and phishing prevention, down to risk analysis.

Each of these areas complements the others, and there is no single magic solution that fits every organization — adaptation to the nature of each environment and gradual, step-by-step progress are required.

## Access Control

The goal of access control is to implement policies, processes, and technologies that ensure only authorized users are granted the least privileges necessary to perform their work (the principle of Least Privilege).

There is no one-size-fits-all solution here — organizations must adapt and progress gradually according to the nature of their own environment.

### Password & MFA

The lowest level of protection is implementing a strong password policy across the technical environment. In a Windows environment, this policy should be configured within the `Default Domain Policy` to ensure it applies to all domain-connected machines.

Whenever possible, stronger authentication mechanisms than traditional passwords should be used, such as biometrics, one-time passwords, and application tokens. Multi-factor authentication (MFA) — whether via SMS or an authenticator app — is highly recommended, starting with privileged users and gradually extending to all users.

### Zero Trust

This principle is based on identifying and disabling unused accounts, eliminating accounts shared between multiple people, removing unnecessary privileges, and enforcing strong password policies across the board without exception.

### Audit of Account Usage

User activity should be monitored and analyzed to detect any abnormal behavior, such as access attempts outside normal business hours or from unusual geographic locations.

As a general guideline, no more than 15% of accounts in the organization should hold `Domain Administrator` privileges, since exceeding this ratio means an unnecessary expansion of the scope of sensitive privileges.

## Backups

Backups are not a mechanism for directly fighting ransomware, but they represent the last line of defense when an attack occurs. A non-operational backup system following an attack could jeopardize the survival of the entire business.

### The 3-2-1 Rule

As a basic rule and the minimum expected for any infrastructure, the 3-2-1 rule states that you must have at least three copies of your data, store them on two different media, with one of these copies kept offsite.

* **Three copies:** The principle is to keep the data on the server plus two backup copies, to avoid a single failure disabling all backups at once.
* **Two different media:** This does not necessarily mean two different physical formats, such as a hard disk and an LTO tape. Rather, it means having the backup on two separate, unrelated points — it is possible to have two copies on hard disks as long as they are not stored in the same datacenter or linked via the same software RAID array.
* **At least one offsite backup:** Keep a backup stored outside the main building containing the essential data, to protect against risks such as fire or other disasters that could destroy the primary site entirely.

### The 3-2-1-1-0 Rule

This rule should be applied at least to the company's critical resources. It is identical to the basic 3-2-1 rule but adds two extra conditions: one offline copy, and zero errors during restoration.

* **One offline copy:** Keep a backup that is not connected to the network or any other IT infrastructure. The goal is to prevent an attacker from tampering with this copy even if they manage to fully compromise the network.
* **Zero errors during restoration:** Regularly test backups and confirm they can be restored without any errors. It would be unfortunate to discover, only after an actual restoration, that a file on the database server was in fact corrupted.

### Minimum Storage Time

It is important that backups allow restoration of data going back at least 30 days. This specific duration is chosen because the average time between an actual network intrusion and its detection by the company is approximately this length.

### Backup Tests

Once you have confirmed that data is being backed up according to best practices, it is equally important to ensure that restoration tests are tracked and documented, and that every server is restored at least once a year as part of this testing process.

## Internet Browsing Protection

This area aims to filter connections to unauthorized websites, suspicious domain names, and known malicious domains.

### DNS Filtering

Dangerous sites should be blocked and unwanted content filtered through firewalls. In addition to well-known “unprofessional” categories such as adult content, there is one category that is rarely blocked: URL shorteners.

This service is used extensively, especially in phishing attacks, because it hides the real destination of a link.

Once blocking has been configured, it is essential to regularly review the log of blocked sites that employees have attempted to visit, as this can reveal intrusion attempts or suspicious activity.

### Centralized Management of Browsers

Updating browser security settings can make it harder for malware to install itself on devices. For example, this can include reducing the ability to install plug-ins or disabling the automatic execution of certain types of content that may carry malicious code.

## Inventory

Protecting your infrastructure requires accurate knowledge of the devices connected to your network, the applications in use, who has access to them, and what security measures are applied to them.

### Inventory Content and Its Importance

As with all information security matters, you will need a complete and thorough inventory. At a minimum, this inventory should include:

* The hardware components of each workstation and server
* The software installed with its exact version
* The date of the last inventory report for each item

### End-of-Life Equipment

Thanks to the inventory, you become able to isolate all equipment, hardware and software, that has reached the end of its support lifecycle.

Equipment that no longer receives support is equipment that will no longer receive security patches. It is therefore necessary to fully exclude from the network any equipment that can no longer be maintained.

In cases of extreme necessity where continued use is unavoidable, formal risk acceptance must be documented by the Chief Information Security Officer (CISO) and recorded in the inventory. This analysis should be reviewed periodically, ideally every time a new vulnerability affecting this equipment is discovered.

### Secure Boot

Secure Boot should be enabled on all compatible devices. This feature ensures that a device boots using only software approved by the manufacturer.

This feature has been available for over ten years, so it is unlikely that standard usage will encounter any issues after enabling it.

## Software List

To reduce the attack surface, it is important for the company to maintain a strict policy defining which software is authorized and which is forbidden.

### Allowed Software

Using tools such as GPO (Group Policy Object) or Intune allows you to provide users with a quickly accessible software library without granting them administrative rights on their machines.

This prevents users from having to download installation programs themselves, thereby limiting the risk of accidentally downloading a malicious program.

### Forbidden Software

Whether via Intune or AppLocker, it is necessary to block software classified as forbidden — either because its use is not legitimized within the work environment, or because the version in use is subject to a known vulnerability (CVE) that poses a risk to the organization.

Every use of a forbidden application should be immediately reported to the company's IT team.

## Security Hardening

Does your company rely on proven hardening guides to define the configuration of its devices?

These guidelines can cover different levels, such as:

* Workstation handover procedures with a prerequisite checklist
* Auditing the secure configuration of devices
* Generating an alert whenever a configuration change occurs

This hardening can be implemented in several ways, such as through Ansible, GPO, or Intune.

### Antivirus / EDR

You should ensure that the company deploys antivirus software, or even an EDR (Endpoint Detection and Response) system, across the entire fleet of devices, starting with the devices most critical and sensitive to the company's operations.

It is essential not to forget to set up an actual follow-up process for the alerts generated by these systems, since simply having the tool in place without monitoring its alerts does not deliver the intended benefit.

## Network Monitoring

This area aims to monitor an organization's incoming and outgoing internet traffic.

### PCAP

Use the SPAN ports of your network equipment to capture network activity. This capture allows you to detect abnormal behavior, such as an unusual increase in the use of a certain protocol or the appearance of abnormal destination addresses.

It also enables post-mortem analysis in the event of an actual compromise.

### Segmentation

Segmentation divides a single computer network into smaller parts. Network segmentation improves both network performance and security by reducing the attack surface and limiting the range of any potential attack.

The use of technologies such as VLAN and PVLAN allows different networks to be separated from one another.

Important questions to ask include:

* Are the administration interfaces of your network equipment accessible from an ordinary workstation belonging to a non-technical department, such as accounting?
* Is the remote office service available only on a dedicated, isolated network?

### Review of Blocked Flows

Once your corporate network is segmented and unauthorized flows are blocked, the next step is to set up a review process to identify the source of requests being blocked under the new policy.

The source could be a compromised workstation, an application that went unnoticed in the inventory, or another cause worth investigating.

### Alert Outside of Standard Use

Once all of the above is in place, you can generate alerts in the event of abnormal network usage.

Beyond the direct security benefit, these alerts can also help identify weak points within the organization — for example, when backup tools cause unexpected network saturation.

## Patching

This area aims to deploy patches for software and firmware as quickly as possible, enabling automatic updates whenever feasible.

### SLA for Patching According to CVE

A service-level agreement (SLA) is a contract between a service provider and its customers that documents the services the provider will furnish and defines the service standards the provider is obligated to meet.

The core question here is: has the company set a maximum update time limit for workstations, servers, and software?

If so, certain criteria should be taken into account when setting this time limit, such as:

* The vulnerability's CVSS score
* Whether the server to be patched is internet-facing or not
* Whether the flaw is known to be actively exploited in the wild, a 0-day

All of these factors should influence the priority and speed of the patching process.

## Phishing Prevention

Phishing attacks represent one of the largest initial attack vectors, alongside the exploitation of vulnerabilities in internet-facing servers.

### Antispam and Email Protection

Important questions to ask include:

* Do all emails received by employees pass through a spam filter?
* Does the antivirus software analyze email attachments?
* Is this configuration regularly reviewed and kept up to date in line with emerging threats?

### Analysis Procedure

When an employee receives an email and has doubts about it, they should have a clear way to contact a dedicated party to perform a technical analysis of that email, rather than acting purely on their own personal judgment.

### Phishing Drill

This kind of simulation is often perceived by staff as an actual attack while it is taking place.

It can be very worthwhile to conduct periodic simulation tests to ensure staff are genuinely prepared to handle real phishing attempts when they occur.

## Risk Analysis

This area aims to use risk assessments to prioritize the allocation of resources and security investments in a rational, evidence-based manner rather than through guesswork.

### Return to Service

Has the company conducted a study to determine which resources should be recovered first in the event of an incident or outage?

This analysis can also be used to estimate the impact of any service disruption and to identify the allowable downtime for each system without seriously affecting business continuity.

### Review of Risks on Connected Networks

Every connection to the company's network represents a potential risk, whether that connection originates from within one of the company's own entities or from an external partner.

It should always be kept in mind that any of these parties may not hold the same security requirements that your own organization applies.

Key questions worth asking include:

* Are your partners committed to the same level of security you maintain?
* Do you know how quickly they respond and update their systems when a new vulnerability is disclosed?
* Are they committed to not using default certificates on their VPNs?
* If they use online/cloud solutions, are you actually certain that their configuration aligns with your own security requirements?
