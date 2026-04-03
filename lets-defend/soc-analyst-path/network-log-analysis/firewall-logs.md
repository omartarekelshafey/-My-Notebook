# firewall logs

الـ Firewall هو اللي بيتحكم في الـ Incoming والـ Outgoing Traffic بناءً على الـ security Policies.

***

### Introduction to Next-Generation Firewalls (NGFW)

الـ Firewalls اتطورت جداً ومابقتش مجرد Packet Filtering عند الـ OSI Layer 3 بس، ودلوقتي عندنا الـ NGFW اللي بتتميز بالآتي:

* الـ Application Inspection: بتقدر تفحص الـ Traffic لحد الـ OSI Layer 7.
* الـ Application Awareness: الـ NGFW بيقدر يتعرف على تطبيقات معينة زي HTTP, SSH, أو DNS.
* التحكم الـ Granular: بدل ما تقفل Port 22 بس، الـ NGFW يقدر يكتشف ويقفل الـ SSH Communication حتى لو شغال على Non-standard Port.

### Anatomy of a Firewall Traffic Log

لما تيجي تعمل Log Analysis، لازم تكون فاهم الـ Fields الأساسية اللي بتظهرلك في الـ Traffic Log.

#### Sample Traffic Log

date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1653131198230012501 tz="+0300" logid="0000000013" type="traffic" subtype="forward" level="notice" vd="root" srcip=172.14.14.26 srcname="CNL" srcport=50495 srcintf="ACC-LAN" srcintfrole="lan" dstip=142.250.186.142 dstport=443 dstintf="Wan" dstintfrole="wan" srccountry="Reserved" dstcountry="United States" sessionid=445180938 proto=6 action="accept" policyid=284 policytype="policy" poluuid="8ec32778-a70a-51ec-9265-8fdf896d07f1" service="HTTPS" trandisp="snat" transip=89.145.185.195 transport=50495 duration=72 sentbyte=2518 rcvdbyte=49503 sentpkt=13 rcvdpkt=42

#### Key Log Fields Explained

* **date**= Date
* **time**= Time
* **devname**= Hostname
* **devid**= Device ID
* **eventtime**= 1653131198230012501
* **tz**= time zone
* **logid**= Log ID
* **type**= Log Type (traffic, utm, event, etc.)
* **subtype**= Sub Log Type (Forward, vpn, webfilter, virus, ips, system, etc.)
* **level**= log level
* **srcip**= Source IP Address
* **srcname**= Source Hostname
* **srcport**= Source Port
* **srcintf**= Name of the Source Interface
* **srcintfrole**= Role of the Source Interface
* **dstip**= Destination IP Address
* **dstport**= Destination Port
* **dstintf**= Name of the Destination Interface
* **dstintfrole**= Role of the Destination Interface
* **srccountry**= Source IP information (Country)
* **dstcountry**= Destination IP information (Country)
* **action**= info on the action taken (drop, deny, accept, etc.)
* **service**= service information
* **transip**= NAT IP info (internal output of the private source address)
* **transport**= NAT port info
* **duration**= time elapsed
* **sentbyte**= size of the packets sent (byte)
* **rcvdbyte**= size of the packets received (byte)
* **sentpkt**= number of the packets sent
* **rcvdpkt**= number of the packets received

### Understanding Firewall Actions

الـ Action field هو اللي بيقولك الـ Traffic ده حصل فيه إيه بالظبط، ودي أشهر الحالات:

* الـ Action accept: معناه إن الـ Packet عدت بنجاح.
* الـ Action deny: الـ Traffic اتقفل، والـ Firewall بعت Notification للـ Source IP.
* الـ Action drop: الـ Traffic اتقفل بس من غير ما يبعت أي Notification للمصدر (كأنه مش موجود).
* الـ Action close: معناه إن الـ Communication انتهى بشكل طبيعي من الطرفين.
* الـ Action client-rst: الـ Client هو اللي قطع الاتصال.
* الـ Action server-rst: الـ Server هو اللي قطع الاتصال.
