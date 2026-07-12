# Case/Alert Naming

## Importance of Naming Conventions

Having a unified and meaningful naming convention for records, tickets, or cases within an Incident Management System (IMS) is critical for operational efficiency. It ensures that SOC analysts can understand the basic nature of a ticket just by looking at its title. This practice supports:

* Retrospective Inquiries: Allowing analysts to search past records and find relevant historical data quickly.
* Statistical Extraction: Making it easy to generate metrics and run statistics across incidents during high-level investigations.

## Naming Formats

**The LetsDefend Standard**

The naming method utilized in LetsDefend "Case Management" follows a strict, structured template:

* `EventID: {Alert ID Number} - [{Alert Name}]`

This specific format allows analysts to immediately pull up or filter past alarm details using either the unique identification number or the specific name of the triggered rule.

## **Real-World Industry Variations**

In production enterprise environments, this approach is a standard industry practice. Depending on organizational policies, titles are often expanded to include additional contextual fields such as:

* Alert Category: Defining the classification of the threat (e.g., Brute Force, Phishing, Privilege Escalation).
* Event Source: Identifying the originating asset or system (e.g., Firewall, EDR, Active Directory).
* Description: Providing a brief, actionable summary of the anomalous behavior detected.
