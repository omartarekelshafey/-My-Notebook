# Cyber Threat Intelligence (CTI)

## Introduction to CTI

Cyber Threat Intelligence (CTI) is one of the most important fields within Cybersecurity. It aims to collect data from multiple sources and analyze it in order to produce **Actionable Intelligence** that helps organizations prevent Cyber Attacks and reduce the damage they cause.

CTI focuses mainly on understanding the **Tactics, Techniques, and Procedures (TTPs)** used by attackers, and on turning Raw Data and IOCs into Information that is useful and tailored to each organization based on the nature of its business and the threats directed at it.

## CTI Lifecycle

### Planning and Direction

The Planning and Direction phase is the foundation for ensuring the success of the entire Intelligence cycle. In this phase, the objectives are defined, along with who the final consumer of the report will be, and which bodies or teams will make decisions based on it.

The planning phase includes answering key questions to define the Scope of the Intelligence:

- **Existence of a SOC team:** This determines whether the Intelligence will be technical and detailed for SOC Analysts, or high-level summaries directed at Managers.
- **History of previous attacks:** Helps determine the consumption rate of Intelligence and the frequency of pulling data from Internal and External Sources.
- **Nature of the targets:** If the organization itself is the target, focus is placed on External Attack Surface Management. If individuals are the target, focus shifts to Digital Risk Protection, to protect Credentials and against Phishing Risks.
- **Sector-based threats:** Coordinating with companies in the same industry to benefit from Industry-based Intelligence and share IOCs in order to counter shared attacks.

### Information Gathering

The data-gathering phase relies on multiple internal and external sources to obtain the latest threats:

- Hacker Forums, the Dark Web, and Bot Markets.
- Ransomware Blogs and Cybersecurity Blogs.
- Public Sandboxes and Public Research Reports.
- Channels such as Telegram, Discord, and ICQ, as well as social media platforms like Twitter, LinkedIn, and Facebook.
- Code and file repositories such as GitHub, GitLab, and Bitbucket.
- Exposed public storage buckets such as Amazon S3 and Azure Blob Buckets.
- Specialized search engines such as Shodan, BinaryEdge, and ZoomEye.
- IOC databases such as AlienVault OTX, Abuse.ch, and MalwareBazaar.
- Honeypot systems and internal security devices such as SIEM, IDS/IPS, and Firewalls.

### Processing

The Processing phase acts as the main filter, where data is cleansed of False Positives, and Ruleset and Correlation rules are applied to produce organized data that is ready for analysis.

### Analysis and Production

The Analysis phase relies on interpreting the data and turning it into Actionable CTI, then preparing reports in the format appropriate for the target audience, whether technical or managerial.

### Dissemination and Feedback

The Dissemination phase involves distributing the Intelligence to relevant parties through appropriate channels, while activating a Feedback loop to continuously improve the process and avoid mistakes — such as evaluating Subdomains separately from the Root Domain to reduce False Positives.

## Types of Cyber Threat Intelligence

![Types of CTI](images/image1.png)

The types of CTI differ based on the functional level and the specific needs of each team within the organization.

### Technical Cyber Threat Intelligence

This type is the output of technical analysis that relies primarily on IOCs.

Its importance lies in helping the organization build rulesets to protect against attacks. This is done through reports containing hashes of malicious IP addresses, phishing domains, and malicious files.

As shown in the image, this type is classified as **Low Level** and **Short-term Use**, since it focuses on a Specific IOC.

The teams that rely on this type are the SOC Staff and the Incident Responder.

### Tactical Cyber Threat Intelligence

This type focuses on understanding the TTPs (Tactics, Techniques, Procedures) used by attackers.

It aims to answer very important questions such as: what vulnerabilities does the attacker exploit? Which countries does the attacker operate in? What are the attacker's motivations and methods? This helps in taking preventive measures.

This type is considered **Low Level** but intended for **Long-term Use**.

The teams that rely on this type are IT Service Administrators and SOC Managers, who are responsible for leading the technical teams.

### Operational Cyber Threat Intelligence

There is a lot of confusion between this type and Tactical CTI because both are concerned with TTPs, but this type is used mainly in Threat Hunting operations.

This type is distinguished by its narrower scope, since it can focus on a specific type of attack or a specific attacker, unlike Tactical CTI, which tends to be more automated.

This type is considered **High Level** and **Short-term Use**, since it provides information about a specific incoming attack.

The teams that rely on this type are the Security Manager, the Network Defender, and Threat Hunting personnel.

### Strategic Cyber Threat Intelligence

This type is designed specifically for top executives within the organization.

It is very useful for long-term tasks such as product purchasing, budgeting, and planning, and this is done through evaluating the outputs of Tactical CTI.

This type is classified as **High Level** and **Long-term Use**, since it provides important information about changing risks.

The teams that rely on this type are High Level Executives and Management.

## Determining the Attack Surface

### The Importance of Attack Surface in Threat Intelligence

Traditional Threat Intelligence models (Classical CTI) are no longer sufficient on their own. A new concept called External Attack Surface emerged to fill this gap. From here, the concept of **Extended Threat Intelligence (XTI)** emerged, which differs from regular CTI in that it builds an attack surface specific to the organization itself, in order to produce intelligence tailored to it, rather than just general information about threats.

The main benefit of building the attack surface is that the organization gains visibility over all its assets — whether it's a forgotten endpoint or an old subdomain nobody remembers. The ultimate goal: the organization knows everything precisely, and knows exactly which assets it is supposed to defend, because you can't protect something you don't even know exists.

### Determining the Attack Surface (Components)

When determining the Attack Surface, a set of integrated elements falls under it: Domains and Subdomains, Websites and Login Pages, CMS systems and Technologies Used on Websites, IP Addresses, IP Blocks and DNS Records, C-Level Employee Mails, Network Applications and Operating Systems, Bin Numbers and Swift Codes for banks, and finally SSL Certificates.

### Domains

The only piece of information available at the start is the main domain, and the CTI analyst is required to build the entity's entire structure starting from it. There are 3 main methods for reaching additional domains belonging to the organization.

**Method 1: host.io Tool**

The host.io tool provides four different viewpoints on the domain being investigated:

- **Co-Hosted:** shows all domains hosted on the same IP address as example.com.
- **Backlinks:** shows domains that have a link pointing to example.com.
- **Links to:** shows domains that example.com itself links to from within its own content.
- **Redirects:** shows domains that automatically redirect to example.com as soon as they are opened.

**Method 2: Reverse Whois**

When checking the whois data for the domain example.com, we notice that the Registrant Organization field contains the company's own name, 'EXAMPLECORP'. This name can be used as a search key: using the viewdns.info tool, we perform an operation called Reverse Whois, which searches for all domains registered under the same organization name or the same Registrant Mail. This may return a result containing hundreds of domains, which are considered candidates for belonging to the company, and after verifying each one, it is added to the inventory.

As an alternative tool, whoxy.com can be used, which follows the same Reverse Whois principle but splits results into four different search categories.

**Method 3: DNS Records Inspection**

By checking the DNS records of the main domain — whether through the `dig` command line tool or through an online tool like dnslytics.com — we obtain information about the Name Servers (NS) and Mail Servers (MX Records). The core idea here is that a shared nameserver belonging to a public hosting company may host thousands of domains unrelated to the organization, but if the nameserver is exclusively owned by the organization itself, then all domains hosted on it become strong candidates for ownership.

You'll notice that the nameserver ns2.example.com hosts 98 other domains. Doing a reverse lookup on the same nameserver using the same tool reveals domains such as otherbank1.es and realestate-portal.es, all of which share the same NS Records and Mail Servers — a strong indicator that they all belong to the same organizational infrastructure. After verification, they can be added to the inventory.

### Subdomains

After collecting the main domains, the next step is discovering the subdomains for each domain. There are four main tools that can be used for this purpose:

- **SecurityTrails:** can be used from the command line via the hacktrails tool, via the API, or directly from the visual interface. It produces high-quality results.
- **Sublist3r:** a command-line tool that gathers results from multiple sources simultaneously, such as Baidu, Yahoo, Google, Bing, Netcraft, DNSdumpster, VirusTotal, ThreatCrowd, SSL certificates, and PassiveDNS. The tool can succeed in finding hundreds of unique subdomains.
- **Assetfinder:** another tool that queries multiple sources to find subdomains.

### Websites

After compiling a large list of domains and subdomains, this does not mean that every one of them represents a live website. To confirm this, HTTP/HTTPS requests must be sent to every item in the list, to find out which ones actually respond. The `httpx` tool does exactly this job — it scans the entire list and returns only the links that responded, such as http://calendar.example.com, https://drag.example.com, and https://admon.lb.example.com. As an alternative to httpx, the `httprobe` tool can be used, which performs the same function.

### Login Pages

Discovering which sites in the list actually contain a login page is a harder challenge than simply checking the response, because it requires understanding the page content, not just its availability. Manually going through every site to classify it consumes a lot of time and effort, so it's recommended to write a simple Python script using the `requests` and `BeautifulSoup` libraries, which sends a request to each site and analyzes the response content to answer inferential questions such as: does the word 'Login' or its equivalent in any language appear on the page? Are there form tags? Are there words like 'Username' or 'Password' as a placeholder?

### Technologies Used on Websites

These are the methods and techniques used to detect the infrastructure and systems that run websites.

First, we use Browser Extensions such as Wappalyzer, Whatruns, and BuiltWith — these are tools installed on the browser that perform analysis and produce detailed information about the technologies used, such as the CMS, databases, web servers, and JavaScript frameworks.

Second, there are Online Scanning Tools such as whatcms.org, which offer a quick method that doesn't require installing any software — you simply enter the URL, and the tool displays basic information such as the programming language and web server on a single results page.

Third, we perform Manual Inspection of the Source Code — a manual method where you view the code and look for the file paths and directories belonging to the CMS, or the themes and libraries inside the script tags.

Fourth, we perform Response Headers Analysis using the browser's Developer Console to inspect the response headers returned by the server, which often leak direct information about the hosting environment, such as the `server` header and the `x-powered-by` header, which reveal the web server and backend programming language.

### IP Addresses

IP addresses are among the most important assets of an organization. Serious risks arise when the open ports on these addresses are not monitored regularly, or when outdated services continue running on these ports without updates. That's why monitoring these ports and services, and detecting the associated risks in a timely manner, is vital for the security of any network.

A list of IP addresses can be built by analyzing the domains and subdomains previously collected — either by gathering their A records, or by sending a request and analyzing the resulting resolve process. In addition, to discover all the active IP addresses within blocks belonging to the organization, requests can be sent to all addresses in the range, selecting only the active ones.

### IP Blocks

IP blocks often contain addresses actually owned by the organization, making them one of the highest-risk assets, and monitoring them is critically important. These ranges can be discovered by observing recurring patterns in the IP addresses that appeared from the domains, and checking the whois data for consecutive addresses to confirm actual ownership by the organization.

As a secondary method, you can search using a special search parameter called `org` on the Shodan search engine. For example, a search formatted as `org:"Example Corp"` shows all IP addresses whose organization field contains the word "Example Corp." This can return hundreds of results.

### DNS Records

Continuously monitoring DNS records is very important for detecting any unknown or unauthorized changes, which could indicate suspicious activity or a potential breach. You can use Google's online `dig` tool, or sites like dnslytics.com, or simply the `dig` command from the command line.

### Network Applications and Operating Systems

One of the most important steps in tracking vulnerabilities, whether actively or passively, is inventorying all the applications and operating systems within the organization. All the methods mentioned previously in the IP address section apply here as well. In addition, discovered services can be collected by querying the organization's IP addresses through the Shodan tool, or they can be detected through active scanning. Detections of Network applications and operating systems can be made based on the responses to requests sent to the open ports of the IP addresses previously identified in our asset list.

### Bin Numbers and Swift Codes

Bin numbers and Swift codes are among the most important assets to monitor specifically in the banking sector, especially regarding the detection of stolen credit cards — something that directly concerns fraud teams within banks. Specialized public databases are used to discover the Bin numbers belonging to a specific organization, the most famous being bincheck.io, freebinchecker.com, and bintable.com, where results can be filtered by country and bank name to obtain a list of Bin numbers belonging to that bank.

As for Swift codes, there are specialized sites such as wise.com, bank.codes, and theswiftcodes.com, where you can look up the Swift code for any bank by its name. For example, you might find the code belonging to 'EXAMPLE CORP BANKING', which is EXCPUS33, along with additional details such as the bank's address, city, and country.

### SSL Certificates

SSL certificates are among the most important factors for securing the connection between the user and the website, so it's important to precisely verify the existence of a valid certificate on every discovered domain and add it to the asset list. These certificates can be collected manually, but since this process is time-consuming, it's preferable to use specialized tools to speed it up, the most famous being Censys and crt.sh. Both tools allow searching for all issued certificates containing the target domain name, example.com, while displaying details such as the Issuer and the issuance and expiration dates.

## Gathering Threat Intelligence

One of the most important things while gathering data about cyber threats is searching across many sources — not just a few — trying to search as widely as possible.

### Shodan

Shodan is a web-based search engine, and one of the most famous engines of its kind. It allows users to search for internet-connected systems using specific search filters. Searches can be performed for a particular organization, or even for an entire country, on a global level.

Shodan is distinguished by a very flexible structure that can be shaped in any direction the researcher wants. For example, it can be used to reveal all systems belonging to a specific country or organization that have port 21 (FTP) open and accessible on the internet. A lot of data can be accessed immediately through the direct search interface on the site, but sometimes it's necessary to pull data via Shodan's API, especially since manually gathering intelligence only through the interface isn't practical at scale. Shodan provides full API documentation explaining how to retrieve data programmatically.

### Resources Providing IOCs

Collecting IP addresses, domains, hashes, and C2s belonging to threats is one of the most important ways to protect against potential attacks. Collecting artifacts belonging to threat actors allows these malicious entities to be discovered.

**Hacker Forums**

Hacker Forums are among the most important places for gathering intelligence. Threat actors usually participate first in forums while preparing for an attack. By analyzing their activity on these forums, you can find answers to critically important questions such as the direction of the attack, the specific targets, the methods that will be used in the attack, and even identifying who is behind the attack.

**Ransomware Blogs**

Ransomware Blogs are among the sources that gained significant popularity with the start of the COVID-19 pandemic. Ransomware groups began publishing the data of victims who refused to pay on these blogs.

These blogs answer some important questions such as: who is being targeted, and what are the motives?

Among the most famous ransomware groups: Lockbit, Conti, Revil, Hive, and Babuk. To access these ransomware groups' blogs, the Tor browser must be installed first, since links to these blogs are usually `.onion` addresses, an extension that isn't accessible via a normal browser.

**Black Markets**

Black Markets are used to sell credit cards, stealer logs, and RDP accesses.

The data collected from here, on its own, has limited value and won't produce an actionable output by itself. But if we've already built a complete attack surface, and the data collected here matches any data present in our attack surface, then it produces an actionable result.

**Chatters**

Communication platforms, or Chatters, in their various forms (whether text, voice, or video) are a very important source in Threat Intelligence, because threat actors rely on them to exchange sensitive data or plan and prepare attacks. Therefore, continuous monitoring of these applications — such as Telegram, ICQ, IRC, and Discord — is important.

**Code Repositories**

Code Repositories such as GitHub, GitLab, and Bitbucket are an environment full of sensitive, forgotten data, because individuals or companies often forget important information such as database login info, configuration files, and API keys.

**File Share Websites**

File Share Websites are heavily used by attackers to share files.

Sometimes confidential documents belonging to companies or countries are leaked on these sites after a breach occurs.

Monitoring these sites is a very important step in Threat Intelligence, in order to detect any leak as quickly as possible.

The most famous sites that allow anonymous file uploads are Anonfiles, Mediafire, Uploadfiles, WeTransfer, and File.io.

Extracting data from these sites can be done in two ways:

1. Guessing the unique keys of files and sending them to the application's server — a costly method that requires significant processing power.
2. Using a Dork through a script to pull files that browsers have indexed — an easier method that is much cheaper.

**Public Buckets**

Cloud-based applications, such as Buckets, are used by companies and individuals to store data, and they're supposed to be locked down to authorized users only.

Unfortunately, these environments are often left open to the public, which causes the exposure of confidential and sensitive data, making them an important source for Threat Intelligence.

**Honeypots**

Honeypot systems are one of the most effective ways to trap attackers.

The idea behind them is that they are systems full of security vulnerabilities and not connected to any sensitive server, so they act as a trap that attracts attackers.

What's useful for Threat Intelligence is collecting IOCs, such as attackers' IP addresses, and using them to protect our real systems.

## Using Threat Intelligence

After the data is interpreted relative to the attack surface, it turns into ready-to-use threat intelligence. This intelligence can be used in 3 main areas:

- External Attack Surface Management (EASM)
- Digital Risk Protection (DRP)
- Cyber Threat Intelligence (CTI)

### External Attack Surface Management (EASM)

EASM is part of XTI, and its job is managing the organization's external (outward) assets. The attack surface we build is the foundation of EASM, and this section discusses how to monitor these assets and how they're fed by the intelligence we collect.

Continuous monitoring of assets is important to detect unknown or forgotten assets, such as adding a new domain or removing a domain that's no longer in use from the asset list. Any security vulnerability on these assets poses a risk to the organization.

**EASM Alerts & Actions Table**

| Alert | Meaning | Action |
|---|---|---|
| New Digital Asset(s) Detected | A new asset (domain/subdomain) has appeared and been added to the monitoring list | Confirm the asset actually belongs to the company, and that it was created by an authorized user |
| Domain Information Change Detected | A change occurred in the whois data of a domain already in the asset list | Compare the old data with the new data and confirm the change came from an authorized party |
| DNS Information Change Detected | A change occurred in the DNS records of a domain you already have | Compare the old records with the new ones and confirm there's no suspicious activity |
| DNS Zone Transfer Detected | A change occurred in the DNS Zone Transfer status of one of your domains | Review the DNS records and confirm whether a zone transfer actually happened or not |
| Internal IP Address Detected | An internal IP appeared in an A record for a domain/subdomain instead of a public one | Contact the DNS administrator, investigate the cause, and change the IP if it's not necessary for it to stay as is |
| Critical Open Port Detected | A critical port appears open on a monitored IP (source such as Shodan) | Verify the port, close it or filter it if not actually in use, and if it is in use, update the service running on it |
| SMTP Open Relay Detected | Your mail server is running with an open relay | Verify the mail server status by contacting the person responsible for it |
| SPF/DMARC Record Not Found | A domain in the asset list is missing an SPF or DMARC record | Contact the mail server admin so these records get configured correctly |
| SSL Certificate Revoked/Expired | An SSL certificate for one of the domains has expired or been revoked | Renew the certificate quickly, since its absence means unencrypted transmission |
| Suspicious Website Redirection | One of your domains is redirecting to a site not in the asset list | Verify the redirection immediately and notify the responsible team, as it could be a sign of compromise |
| Subdomain Takeover Detected | Someone was able to take control of a subdomain belonging to you | Identify the DNS record where the takeover occurred and notify the responsible team immediately |
| Website Status Code Changed | The status code returned by the website has changed | Determine the root cause of the issue and apply a fix quickly to avoid service downtime |
| Vulnerability Detected | There's a match between a vulnerability in the data and your assets (apps, SSL, IPs, etc.) | If the source is a CVE with product/version details, accuracy is very high — apply the fix immediately. If the source is Shodan, for example, accuracy is somewhat lower |

### Digital Risk Protection (DRP)

DRP represents the part that makes up the largest share of an organization's intelligence, since it comes after all the data collected from every source has been mapped to the attack surface following interpretation.

The topics covered by DRP: brand reputation protection, Deep & Dark Web threats, fraud protection for banks, the impact of potential supply chain risks, threats to the web surface, and protection of senior executives (VIPs).

**DRP Alerts & Actions Table**

| Alert | Meaning | Action |
|---|---|---|
| Potential Phishing Domain Detected | A new domain resembling yours has appeared (from a new registration or a new SSL certificate) | Examine the domain in a safe environment; if it's impersonating your content, contact the registrar and the ISP to take it down immediately |
| Rogue Mobile Application Detected | A fake app impersonating your official app has appeared on pirated APK sites | Analyze the APK in a safe environment; if malicious, take swift removal action |
| IP Address Reputation | Your IP has entered a blacklist, or appeared in a malicious feed or torrent activity | If blacklisted, investigate the cause and have it removed. If it appears in an IOC feed or torrent activity, this is more serious as it could indicate a breach, requiring immediate investigation |
| Impersonating Social Media Account Detected | A social media account is impersonating your company's name | Review the account; if it's being used for fraud or a smear campaign, contact the platform to have it shut down |
| Botnet Detected at Black Market | A device belonging to your domain/IP has appeared in botnet data on black markets | If the device belongs to a customer, apply a password reset. If it belongs to an employee, isolate it from the network immediately and conduct a forensic investigation |
| Suspicious Content Detected at Deep & Dark Web | A post on a forum or dark market mentions your company | Analyze the content carefully and take appropriate action before the attack happens or escalates |
| Suspicious Content Detected at IM Platforms | Your company is mentioned in conversations on Telegram, ICQ, or IRC | Analyze the conversation and determine its context; if there's a real threat, act quickly |
| Stolen Credit Card Detected | A stolen bank card number matched data from a bank within your intelligence | Notify the fraud team immediately so they can cancel the card |
| Data Leak Detected on Code Repository | Sensitive data (IP, domain, database login credentials) found somewhere like GitHub or an S3 bucket | If the repo belongs to you, delete the data immediately. If it doesn't, request a takedown |
| Company Related Information Detected on Malware Analysis Services | A malicious file referencing your company appeared in a public sandbox | Analyze the file and determine whether it's targeting you directly or being used for a smear campaign, and take the necessary action |
| Employee and VIP Credential Detected | Login credentials for an employee or a VIP you monitor have leaked | Apply an immediate password reset for the affected users |

### Cyber Threat Intelligence (CTI)

CTI is considered part of XTI — the new generation of threat intelligence. Through it, we can track what's happening in the cyber world in general: current malicious campaigns, trends among ransomware groups, or offensive IP addresses around the world.

Since relying on CTI alone can be difficult for protecting an organization, it needs to be supported with corporate feeds to reach the best possible intelligence. When we integrate CTI feeds with tools like SIEM, SOAR, and EDR, we can protect the organization comprehensively.

## LAB TIME

Now we'll solve a lab on **BTLO**.

Here's the scenario and information we start with:

> Authorities are looking for a hacker who is planning to sell a powerful device and the delivery is going to be in an undisclosed but crowded location. It is important to find out what the product is and obtain more information about this hacker.
>
> **Product:** Wifi hacking device
>
> **Key word for finding the exact name of the product:** It is related to a fruit
>
> **Info known about the hacker**
>
> Profile name: jllerenac
>
> Additional Info: He is known for being a good hacker and also a good developer. He has the location info stored somewhere.

### 1) What is the name of the WiFi hacking device?

Based on the information we have — that the device name is related to a fruit — we do a Google search to find out.

![WiFi Pineapple search result](images/image2.png)

As shown clearly here, the name of the hacking device is **WiFi Pineapple**.

### 2) What is the name of the website containing the information on the delivery location?

Now we need to find out which website contains information about the delivery location.

Based on the information we have — that the hacker's name is `jllerenac` — we search for him on Google.

![Search results for jllerenac](images/image3.png)
![Social media accounts found](images/image4.png)

After searching, we found several accounts belonging to him: on Twitter, GitHub, and LinkedIn.

![Hacker's GitHub account](images/image5.png)

We started with his GitHub account.

We looked through his repos for anything related to selling a WiFi Pineapple.

At first we didn't find anything useful, so we started looking through pull requests and commits.

![Commits found in an unowned repo](images/image6.png)

Here we found that he made commits in a repo that isn't listed among his own repos.

![Repository contents](images/image7.png)

We opened the repo shown in the image and found only one folder.

![Folder contents](images/image8.png)

We opened the folder and found only one file.

![File contents](images/image9.png)

We opened the file and found coordinates in it, but they needed to be decoded.

So the website containing the delivery location information is **GitHub**.

### 3) What is the name of the file containing the location information?

As we saw in the previous steps, we reached the coordinates through a repo that isn't listed under the hacker's own account. The file name, as shown clearly in the images, is `ecounter.txt`.

### 4) Enter the coordinates of the meeting

Now we need to get the correct delivery coordinates after decoding the coordinates found in the file.

These were the coordinates:

**40.735971558530885, -73.99116596577247**

### 5) Where is the delivery going to be?

![Delivery location result](images/image10.png)
