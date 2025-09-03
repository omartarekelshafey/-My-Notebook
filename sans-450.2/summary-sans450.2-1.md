# summary sans450.2

**SANS450.2**

Table of Contents

[**1. Network Architecture Intro** 3](summary-sans450.2-1.md#_Toc125840)

[**2. Traffic Capture and Analysis** 4](summary-sans450.2-1.md#_Toc125841)

[**3. Understanding DNS** 6](summary-sans450.2-1.md#_Toc125842)

[**4. DNS Analysis and Attacks** 9](summary-sans450.2-1.md#_Toc125843)

[**5. Understanding HTTP** 13](summary-sans450.2-1.md#_Toc125844)

[**6. HTTP(S) Analysis and Attacks** 16](summary-sans450.2-1.md#_Toc125845)

[**7. Understanding SMTP and Email** 21](summary-sans450.2-1.md#_Toc125846)

### 1. Network Architecture Intro <a href="#toc125840" id="toc125840"></a>

أي ديفندر لازم يكون فاهم Network Architecture بمعني انك تبقي فاهم الترافيك بيتحرك إزاي بين الأجهزة المختلفة كمان لازم تكون عارف النقاط اللي الترافيك بيعدي عليها، زي الفاير ورل او راوتر. لو حصل اي attack من خلال اللي انا عرفته ده اقدراجمع معلومات عن ال attack اللي حصل ووصل لحد فين

### Enterprise Routers

![](<../.gitbook/assets/0 (2).jpeg>)في الشركات بيكون في اكتر من بورت في الراوتر كل بورت بيكون لشبكه معينه وممكن تلاقي كمان اكتر من راوتر لانه الشبكه في الشركات بتتقسم لشبكات اكتر خلينا نتفق علي حاجه انه الراوتر في اساس مش معمول كا security device لكنه بيساعد في بعض الحاجات زي مثلا انه يديناnetwork flow ده بيكون عباره عن داتا الnetwork ops اوsecurity teams بياخدوها من الراوتر من خلال كده بيقدرو يكون عندهم visibility علي الترافيك ومميزات تانيه الراوتر يقدر يساعد بيها في السيكيورتي

### Enterprise Switches

مهمه السويتش الاساسيه انه من خلاله بقدر اشوف التحركات الخاصه بشبكه معينه من الداخلوكمان بتبعت نسخه من الترافيك لsensorsزي ids,ipsعلي شكل flow logاو packet capture

### ![](<../.gitbook/assets/1 (2).jpeg>)Visibility Points

ال **mirror port** بيشوف اللي جوه الشبكه فقط وبيستهلك من الcpu وممكن جزء من الترافيك يضيع منو اما **network tap** فا هو لو حاجه خارجه من السويتش هيشوفها غالي مش بيستهلك من الCpu بتاع السويتش مهتم بL1,L2 ومن خلال ده او ده بيتنسخ الترافيك ويبعته ل sensor

**Enterprise Firewalls**

الفايرول بيكون شغال علي L3,L4 بيكون معتمد علي IP,PORTمش بيقدر يحدد ال USERS AND APP

### Enterprise next-gen firewalls

في بقيnext gen firewall هنا ده بيقدر يكنترول منL2 TO L7 بيقدر يلحظ اي تصرفات غريبه يقدر يتحكم انهي

بروتوكول ومواقع ايه اللي تستخدم بغض النظر عن البورت بيقدر يمنع او يسمح عن طريق اليوزر نفسه مش عن طريقIP اوport

**How do firewalls do that?**

next gen firewall شغال عن طريق انه بيستخدم **Deep Packet Inspection (DPI)**&#x648;بيحتاج هاردوير عالي علشان يقدر يصنف ويفهم الترافيك علي حسب مثلا البروتوكول اوapp طب بيعرف ازاي بردو بناء علي الsignature بتاعت البروتوكول اوapp

**How does a next-generation firewall (NGFW) identify and authenticate users?**

بالنسبه للusers بيتعرف عليهم ازاي من خلال جهاز عادي بينزل برنامج علي كل جهاز في الشبكه علشان بيتعمل Authentication او من خلال حاجه عموميه علي النتورك زي ال AD تقدر تعملAuthentication لكل الشبكه

### The Future: Zero-Trust Architecture

اي شبكه لازم تتقسم علشان لو حصل اي هجوم سواء internal او external يتم نقدر نحجمه ولازم ابقي عارف صلاحيات كل واحد في كل تقسيمه ولازم كل جهاز او شخص موجود في شبكه يتعملهauthentication , authorization ولازم ابقي متابع حركة الترافيك سواء اللي جيه للنتور ك او اللي جوه النتورك نفسها

### Why Network Architecture Matters

لو انا عندي flat network اللي هي بتكون عباره عن شبكه واحده كل اجهزة وصله ببعضها بدون اي عائق مثلا زي الفاير ورل او راوتر فا بالتالي الattackerلو وصل لجهاز جوه كده يقدر يعمل lateral movement فا علشان كده ال segmentation مهم جدا لانه بيبطي ال attackعلشان الحق امنعه

### 2. Traffic Capture and Analysis <a href="#toc125841" id="toc125841"></a>

### Network Data Capture Formats

ال **flow log** بيكون جزء بسيط عن الترافيك اللي هو الlogs الخاصه ب **layer 3,4** ال source and dest ip و port وduration و size packet بتجمع من راوتر ,فايرورل , سويتش هنا بنستخدم علشان نجمعها net flow او مثلا ممكن j flow

او zeek بتجمع من خلال مثلا ال Layer 7 - application metadata only ديه بتكون ال **service log** ال

Suricata

اما ال **packet capture** ده بيكون كل ال layers مش بيكون جزء من الترافيك لا كل الترافيك

### Flow Log Opportunities

ايه الفايده من ال **flow log** بقدر اعرف من خلالها لو في اي up/down load كبير علي النتورك

الاحظ لو في اي ip خد وقت زياده عن لازم في ال connection من خلال معرفتي بال source and dest ip ممكن اعمل عليهم scan اعرف اذا كانو malicious ولا لا

### PCAP and Layer 7 Metadata Collection

![](<../.gitbook/assets/2 (2).jpeg>)**Mirror Port** و **Network Tap** بياخدوا نسخة من الترافيك ويبعتوه ل **PCAP Collector** أو**Sensor** **،** وظيفته إنه يحفظ الترافيك أو يطلع منه بيانات مهمة بسبب حجم الترافيك ممكن اسحب ال layer 7 metadata باستخدام arkime

### Creating Layer 7 Metadata with Zeek

![](<../.gitbook/assets/3 (2).jpeg>)لو في pcap كبير وعايزين نفسمه لfiles بنستخدم ال zeek هي بتقسم ال pcap لjson files كل file بيكون لبروتوكول معين مثلا

### Wire shark

![](<../.gitbook/assets/4 (2).jpeg>)**Packet list pane** هنا بيتم عرض الباكيتس اللي اتعملها capture

#### باخد من هنا Packet details pane

معلومات اكتر عن الباكيت

هنا بعرض **Packet bytes pane** ascii او hex الباكيت بس بشكل

### 3. Understanding DNS <a href="#toc125842" id="toc125842"></a>

**Why Do We Care About DNS?**

ما قبل **DNS** كا لازم تبقي حافظ كل ip بتاع كل موقع ال **DNS** عامل زي contact اللي عندك في تليفون انت عايز تتصل علي واحد صاحبك فا كتبت اسمه وطلعلك واتصلت علي الرقم انت مكنتش ملزم انه تبقي حافظ الرقم نفس الكلام في ال **DNS** عايز مثلا تخش علي تويتر فا بتكتب x.com وخلاص وتخش مش ملزم تبقي حافظ ال ip بتاع تويتر

### DNS Lookup Route

#### ال DNS شغال ازاي ؟

![](<../.gitbook/assets/5 (2).jpeg>)مثلا انا عايز اخش علي جوجل فا بخش اكتب google.com فا بروح اشوف ال (cache(Forwarding Server ملقتش ip جوجل فا بيروح بعدها ل **Recursive DNS Server** بيروح بعدها ل **Root nameservers** يسالو عن ip ملقتش ip

هيدلني اسال root name server هنا ك ال google.com معين يعني **name server**

يبقي .org لو حاجه .com name server اسال

nameserver .org طب ملقتش ال ip بس هيدلني اسال فين قالي اسال **google.com nameservers** سالتو عن ال ip خلاص عارفو جوجل فتح

### Common DNS Request Types

**.1 A/AAAA**

**.2 NS**

**.3 CNAME**

**.4 SOA**

**.5 NULL**

**.6 PTR**

**.7 MX**

**.8 TXT**

**.9 SRV**

**A/AAAA**

انا عايز افتح يوتيوب فا ببعت **A/AAAA Request** بيرد عليا بال ip بتاع يوتيوب A >>IPV4

,AAAA>>IPV6

داخل ال request بيكون في حاجه اسمها **Transaction ID** ده علشان اميز ال request والسيرفر لما بيرد علي ال

**Transaction ID** بيرد بنفس الrequest

![](<../.gitbook/assets/6 (2).jpeg>)

**PTR**

![](<../.gitbook/assets/7 (2).jpeg>)

هنا عكس ال A/AAAA انا بكتب ip السيرفر يرد عليا بالدومين المربوط بال ip ده

![](<../.gitbook/assets/8 (2).png>)

عادي انه يكون اكتر من ip مربوطين بنفس ال ip وعادي العكس انه اكتر من دومين يكونو مربوطين بنفس ال ip

**TXT**

انا عايز ابعت رساله txt ل dns او مثلا عايز txt record بتاع دومين معين ببعت query عادي بيكون فيها ال Transaction ID بيترد عليا عادي بس لازم يكون ال character limit بتاع ال txt يبقي 255

علشان اتاكد من كده بيبقي من خلال ال spf وليه استخدامات تانيه بستخدمه في انه بيكشف علي الدومين بتاع email اللي جايلي علشان اعرف هل هو من مصدر موثوق ولا لا

![](<../.gitbook/assets/9 (2).jpeg>)

#### CNAME ده علشان اربط اسمين ببعض بحيث انه دومين يبقي ليه اسمين عادي

![](<../.gitbook/assets/10 (2).jpeg>)

**MX**

انا عايز ابعت لايميل معين فا ببعت **MX** لدومين بتاع الميل يردو عليا بالميل بتاعهم ابدا ابعتلهم بقي عن طريق **SMTP** ال **MX** بيكون فيه ال **FQDN**

**SRV**

ديه بتساعد في اني بكون بدور علي سيرفيس معينه فا بدور عليها من خلال اسم وبرتوكول بتاعها

**NS**

ديه اللي بتحدد مين السيرفيرات اللي تحملrecords عن دومين بتتخزن اما في TLD

او dns server اساسي بتاع الدومين

### 4. DNS Analysis and Attacks <a href="#toc125843" id="toc125843"></a>

### DNS Traffic Flow and Analysis Considerations

ازاي وفين هعمل مونيتور علي **dns**

![](<../.gitbook/assets/11 (2).jpeg>)ال **dns** بيروح لاكتر من مكان بيروح ل **Root nameservers** و **TLD**

وغيره فا علشان كده انا لازم احدد هروح اعمل monitoringعلشان مثلا عملت مونيتور عند ال**caching server** انا مش عارف مين صاحب ال Request اصلي لانه اللي طلب من **caching server** هو **forwarding server**

واشوف انا عايز اشوف ال **log files** ولا **network extractions** هو انا ببص علي الاتنين علشان بيكملو بعض

هل انا بحفظ ال response

اه انا بحفظ ال response طب ليه بحفظو علشان اقدر اعمل passive dns وعلشان بردو لو حصل حاجه malicious من ip معين يبقي معايا ip ده فا اقدر اعلمه انه IOC واعمله بلوك

### Safely and Accurately Connecting Domain to IP

انا اقدر من خلال ال **ip** بقدر اوصل ل **domain** من خلال ال **dns logs** والعكس صحيح

طب هل في حاجاات تانيه تساعدني اوصل اه عادي من خلال ال **endpoint logs**

او من خلال **osint** ممكن اعرف منه ال **malicious ip** من خلال انه مثلا **attack**حصل في شركه معينه في الشركه كاتبه تقرير عن ال **attack** اللي حصل عليها و ذكرت ال **ip** اللي حصل منه ال **attack**

فا انا كده اخد الip واعمله بلوك

### Detection Technique in General

علشان أعمل detect لأي حاجة عامتا ، لازم أول حاجة أشوف الـ **logs** بتاعتها، وأبدأ أقسمها وأحللها عشان أطلع منها أكبر استفادة ممكنة. بعد كده،. بعد كده، أشوف إذا كان فيه تعديلات لازم أعملها في **rules**بتاعتي، سواء في الـIDS/IPS وغيره

### Detecting Requests for Malicious Sites Using TLDs

كلنا عارفين انه المواقع الموثوقه بتستخدم **tld مدفوعة** زي com . و .org وغيره

لكن بيكون في **free tld** ديه اللي في غالب بيستخدمها الattacker سعات بيستخدم ال **tld المدفوعة** فا انت المفروض تبقي مظبط ال **rules** علي **siem** انه في حاله التعامل مع **tld** غير متعارف عليه اديني **alert** ده في حاله انه **tld** مثلا مش مشهور استخدامه عامتا قليل يعني لكن في **tld** من كتر استخدامها في **attacks** اتعرفت فا في حاله جهاز في الشبكه رايح يتعامل معاها بيتم عمل بلوك

### Domain Reputation

لو عايز افحص دومين معين بقدر اعمل كده من خلال virustotal وغيره

بعرف منه تصنيف دومين ومدي خطورته وبناء علي معلومات ديه اعمل بلوك لدومين ده

طب لو لاقيت دومين هو مشكوك فيه وملوش تصنيف يا اعمله بلوك يا احط قبله تحذير انه خطر

واتابع الاجهزه علشان ممكن يكون في جهاز بيتعامل مع malicious domain كتير ممكن يكون مصاب ب malware ولا حاجه فا الحق اتعامل معاه

### Domain Age

في بعض الدويمنز بتتعمل مخصوص علشان تعمل attack معين فا علشان اعرف هل هو معمول من قريب علشان الattack ده بقدر اعرف من خلال مثلا whois

### Domain Randomness and Length

ال **attacker** بيعمل شويه حاجات تخليها تلغبطك بمعني انه يجيلك **false positive** يعني مثلا في جهاز مصاب عندك فا جهاز بيبعت لدومين بره مفيش اي **alert** بيجيلي طب ليه علشان لو دومين دلوقتي ال **tld** موثوق زي ال.com او ال length طويل او بيكون كلام عشوائي طب علشان اقفشه اعمل ايه اكشف علي الدومين اشوف هل كلام مكتوب منطقي واشوف ال **length** بتاع الدومين واعمل **rule** تحذرني لما يحصل حاجه

### Autonomous System Numbers (ASN)

كل **ORG** بيكون ليها **IP** او مجموعه من **IP** فا كل **ORG** ليها **ASN** ده بيكون مربوط بال **ip** علشان كل **org** تبقي **ip** بتاعتها معروفه بقدر اعرف ايه من كلام ده واحد بيحمل ملف بقدر اعرف هل اللي بيحمل فايل ده تبع المكان الصح للملف ولا لا بمعني تبع **org** موثوقه ولا لا واقدر اعرف اذا كانت **org** معينه ولا **botnet** مثلا

### DNS-Based Attacker Tricks

Now let's step through some common DNS-related scenarios

* Unauthorized DNS server use
* Malicious sites on shared hosting
* Modifying your DNS records
* DNS Tunneling
* Blockchain DNS
* IDNs

### Unauthorized DNS server use

ال attacker بعد ما اخترق واحد من اجهزة الشبكه بيحتاج يتواصل مع الدومين يعمل يعني C2 فا دلوقتي هو لو راح طلب عمل **request** ل **dns** بتاع الشبكه انه يروح لدومين بتاع ال attacker هيترفض فا يلجا ل **extrenal dns** وفي حاجه تانيه عندنا دلوقتي حاجه اسمها **(DOH(Dns Of Https** ده بيستخدم في firefox مثلا وغيره بنستخدمه علشان نشفر ال **request** باستخدام ال **tls** لان ال **https** بتستخدمه في التشفير فا كده dns request بيعدي كانه الترافيك تصفح عادي فا دلوقتي ال **attacker** ممكن يعمل كده ويستغل النقطه ديه

طب حل مشكله ديه ايه تمنع اي تعامل مع اي DNSخارجي غير DNS شبكه تفعل **TLS Inspection** علشان تفك التشفير بتاع الترافيك ممكن اعمل detect ازاي

او حاجه **malicious ip** اشوف لو مربوط ب **port53 UDP** من خلال اني ارقب **logs, alerts** اشوف ال

### Malicious sites on shared hosting

زي ما عرفنا انه ip ممكن يرتبط باكثر من دومين وممكن الدومين يرتبط باكتر كم ip فا كان في دومين مشبوه انا قفشته قدرت اجيب ال ip بتاعه فا انا من خلال ip اكتشفت انه مربوط بحاجات سليمه فا انا لوعملت بلوك ل ip ابقي عملت لدومينز المشبوه والسليمه فا الحل اني اعمل بلوك لدومين نفسو

### Modifying your DNS records

فيه حاجة اسمها**Domain Shadowing** ، وده بيحصل لما ال **attacker** يعرف يوصل ل **dns admain**فا يقدر يتعامل مع record ويضيف**A Record** جديد كأنه **Subdomain** ومن خلال كده بقي يقدر يلقط الترافيك الخاص بيا يعمل موقع فيك نسخه من الموقع بتاع الشركه يقدريبعته لموظفين طب امنع ازاي اقدر امنع من خلال **MFA** مثلا

### DNS Tunneling

الغرض منو هو اني اعمل **C2** او **Data** **exfiltration**

الفكره في انه **ال** **attacker** بيستخدم **ال** **dns** في انه يبعت ويستقبل **encoded** **data** عن طريق انه ممكن يحط **encoded data** ديه في **subdomain** ويستقبل علي نفس **subdomain**

وفي طريقتين **ل** **tunneling** ده ممكن من خلال انه **attacker** يبعت **request** **ل** **dns** **بتاع** **ال** **attacker** فا كده هو في الغالب هيتمنع لانه في شبكات بتمنع انه يتم التعامل مع **external** **dns** ديه ضعيفة او الطريقه تانيه من خلال **TLD** بمعني انه يبعت **request** ل **dns** **بتاع** **الشركه** عايز يروح

لدومين معين ال **dns**ميعرفش الاجابه فا يلف **cycle** العاديه بتاعته لحد **tld** فا يوصله لدومين ال **attacker**

detect ازاي بقي اعمل **tld** و **subdomain** اشوف **record** واشوف حجم **ال** **queries** اشوف ال

### Blockchain DNS

بكل بساطه الblock chain dns ملوش حاجه مسيطره عليه مثلا او في مركزيه فيه لا فا بالتالي صعب مراقبته والداتا اللي بتمر فيه مشفره

### IDNs

ال **dns** مش بيفهم غير انجليزي و ارقام فا علشان نحل موضوع ده بيحول الكلام اللي بلغه تانيه غير الانجليزي باستخدام حاجه اسمها **puny** **code**

الشكل اللي قدامنا ده شكل ال **puny** **code** ال **xn** ديه ثابته عامتا في بدايه دايما

**Yutube** ده الكلام اللي بالانجليزي

والجزء الاخير ده الشكل جديد لحرف اللي مكنش مكتوب بالانجليزي بعد ما اتعمله**encode** ال **puny** **code** بيساعدنا في قفش ال **phishing**

![](<../.gitbook/assets/12 (2).jpeg>)

### 5. Understanding HTTP <a href="#toc125844" id="toc125844"></a>

ال web server ده مهمته اني برفع عليه الموقع بتاعي علشان اشاركه مع الناس عن طريق http

### Decoding a URI

![](<../.gitbook/assets/13 (2).jpeg>)

### HTTP Methods: GET

**ال** **get** مهمتها انها بتجيب files من السيرفر طريقه ديه متنفعش غير لو انت بتطلب معلومات مش حساسه

طب ليه علشان الداتا اللي بتجاب ديه هتبان في ال **url**

### HTTP Methods: POST

مهمتها انها ترفع معلومات للسيرفر بس هنا بقي مش بتبان في **url** فا بستخدمها معلومات الحساسه لاني برفع المعلومات داخل الهيدر

### HTTP Request Headers

**HTTP transactions contain "key: value" headers:**

![](<../.gitbook/assets/14 (2).jpeg>)

ال **host** ده موقع اللي انت فتحته

ال **user** **agent** ده هنا فاتح من انهي **browser** وشغال من انهي **os**

ال **accept** هنا ده لما **browser** بيبعت للسيرفر بيقوله انه ديه **لغه** اللي انا بقبلها ده **نوع** **الملفات** اللي بقبلها ال **refere** هو جي منين بمعني انه انت فاتح تويتر فا دخلت علي لينك يكتب في **refere** انه انت جي من تويتر ال **cookie** معلومات عن اليوزر خلال السيشن

### Assessing HTTP Request Headers

ايه هي الحاجات المهمه في **request header**

**.1 Host**

.2 **User** **agent**

**.3 Path**

طب ليه دول؟

ال **host** علشان اعرف موقع اللي اطلب ال **user** **agent** علشان اعرف ال **browser** و **os**

ال **path** علشان اعرف هو عايز يفتح ايه في الموقع بمعني عايز يوصل ليه ال **content** عامعلشان اشوف لو في حاجه مشبوه

### HTTP Response Headers

**Server**: Webserver software and version number

**Date**: The date and time the message originated

**Content**-**Type**: Type of file being returned from server

Very useful for mass searching in SIEM

**Content**-**Length**: Length of body content in bytes

**Last**-**Modified**: When the resource was last changed

**Set**-**Cookie**: Tells the client to set the provided cookie

### ![](<../.gitbook/assets/15 (2).jpeg>)Most Common HTTP Response Codes

**1xx Informational: 2xx Successful:**

* 100 Continue • 200 OK
* 101 Switching Protocols

**3xx Redirection:**

* الموقع مكانه اتغير خالص Moved Permanently 103 موقع مكانه موجود في مكان تاني موقتاFound 203 •

**4xx Client Error: 5xx Server Error:**

* 401 Unauthorized • 500 Internal Server Error
* 403 Forbidden • 503 Service Unavailable
* 404 Not Found
* 407 Proxy Auth Required

### HTTP/2 =SPDY

#### one tcp connection بيخلي صفح سريعه

بيفصل الداتا فريم عن الهيدر والهيدر بيكون **binary**

موجود فيه كمان **server** **push** اللي هو سيرفر بيدي الbrowser حاجات اساسيه الموقع محتاجها يروح يبعتها علي طول من غير ما يطلبها البراوزر

### HTTP/3

**QUIC** (**Quick** **Udp** **Internet** **Connection**) بيشتغل فيه برتوكول اسمه

هنا بيتعامل مع **udp** فا بيكون الترافيك اسرع ومشفر كويس كمان هنا الترافيك عباره عن **tcp** /**tls**/**http2**

### 6. HTTP(S) Analysis and Attacks <a href="#toc125845" id="toc125845"></a>

ال **http** بيستخدم في اكتر من step من **cyber** **kill** **chain** زي مثلا في **C2** بيتم استخدام ال **GET\&POST**

### HTTP Analysis Methods

#### manual يا اما automated بعملو يا اما http ل analysis علشان اعمل

sand box او مثلا من خلال url scan او مثلا virus total ديه بتكون عن طريق مثلا auto method ال

ال man method بشوف ال request و ال Response وافحصهم افحص محتوي اللي رايح والمحتوي اللي بيتبعتلي Virus total عندهpolicies و standard فا ممكن انت تبعتله لينك يفحصه هو سليم بس ممكن ميقولش انه سليم علشان بس هو مخالف لاحد ال policies عنده وعادي العكس انه يكون مش سليم ويقول انه سليم

### URL Sandboxing

ايه هو **url** **sandboxing** هو طريقه من طرق **auto** **method** بتم من خلال حاجتين

اول حاجه انه لينك بيتفتح علي **virtual** **machine** فا بيتجرب عليه شويه حاجات وبيتم متابعه سلوك موقع علشان نعرف هو موثع مشبوه ولا لا تاني حاجه انه بفحص **html** **files** علشان اشوف الموقع سليم ولا لا

في حاجه كمان في **auto** **method** اللي هي اني ممكن اخد موقع اسكرين شوت وابعتها علشان تتفحص اسكرين شوت ديه وتقارنها بالموقع الاصلي وديه من حاجات ال بتمنع **phishing**

حاجه كمان مشرط انه دومين يبقي امن انه ال **url** هو ممكن يكون **malicious** **url** بس مربوط بدومين سليم مثلا تويتر **x.com** بس لاقيت معاها حاجات تانيه غريبه فا بالتالي باشك وابدا اعمل **analysis**

### Manual Header and Content Analysis

كل ده كان **auto** **method** دلوقتي هنكلم بقي عن ال **manual** **method**

في اكتر من طريقه في ال manual method زي

Header analysis: URLs, User-Agents, and more

GET/POST content analysis

File analysis

Anomalous behavior

Base64encoded content

Naked IP addresses

Repetitive beaconing

Other anomalies

### User-Agent Analysis

ال user agent . زي ما عارفنا انه احنا بنعرف منه os و browser

tools اوextensions عن طريق user agent ممكن يغيرو ال attacker فا دلوقتي في

ديه واحد من extensions اللي بتعمل كده

![](<../.gitbook/assets/16 (2).jpeg>)

دلوقتي هنا اهو انا هنا ويندوز وتمام

![](<../.gitbook/assets/17 (2).jpeg>)

linux يبقي user agent وعملت انه ال extension فا روحت شغلت

فا اتقلب علي طول ل linux زي ما في الصوره

![](<../.gitbook/assets/18 (2).jpeg>)

من الطرق اللي بقي بتكشف الحوار ده انه مثلا انا جايلي request مكتوب فيه انه ويندوز 10 جوجل كروم

فا كل os اوbrowser بيكون ليه حاجه خاصه تميزه زي مثلا ترتيب ال headers ,محتواها مثلا ال packet size فا من خلال كل ده بقدر اميز هل هو جوجل كروم فعلا ولا لا المعلومات مبعوته ديه تختلف عن اصليه يبقي كده في spoof

### Cookies

الكوكيز بتكون عباره عن معلومات اليوزر خلال السيشن بتاعته وهي كمان بتكون حاجه يعرف بيها نفسه

ممكن يستخدم في ال **C2**

### Base 64 encoding

هو عباره عن انه انا بغير صيغه كلام لصيغه تانيه

مثلا انا عايز احول حرف A بشوف هو بيساوي ايه في ascii code هتلاقي بيساوي 65

اللي هو في binary بيساوي 01000001 ده كده 8bit انا عايز احولو ل base 64 اللي هو 6 bit

فا باخد اول 6 bit من الشمال 010000 برحل الباقي للحرف اللي جانبو وفي نهايه بحول كل 6 bit لرقم dec وبعدها من خلال جدول base 64 بشوف رقم ده بيعادل ايه واكتب وكده اتعمل encode

مثال سريع علشان معلومه توصل عايز اعمل encode ل Hello

| Binary   | ASCII | حرف |
| -------- | ----- | --- |
| 01001000 | 72    | H   |
| 01100101 | 101   | e   |
| 01101100 | 108   | l   |
| 01101100 | 108   | l   |
| 01101111 | 111   | o   |

هناخد من 6bit من 8bit بتاع كل حرف وباقي يروح للحرف اللي بعده

ده كده بعد حولناه ل 6 bit

010010 000110 010101 101100 011011 000110 1111

هنحول كل 6 ل dec وبعدها نشوف كل dec بيقابل ايه في جدول بتاع base 64

| Base64 char | Decimal | Binary |
| ----------- | ------- | ------ |
| S           | 18      | 010010 |
| G           | 6       | 000110 |
| V           | 21      | 010101 |
| S           | 44      | 101100 |
| b           | 27      | 011011 |
| G           | 6       | 000110 |
| 8           | 15      | 1111   |

ده كده الناتج النهائي لتحويل كلمه hello

SGVsbG8=

### File Analysis\&Extraction

#### user agent,refer,host,method لو انا في ملف شاكك فيه بشوف ال

اعرف ال **behavior** بتاع الملف ارفعه مثلا علي **virus** **total** اشوف هل في حاجة مشابه للملف ده اترفعت قبل كده ولا لا

وممكن اجيب ملف من ال **Wireshark** واكشف عليه

في حاجه كمان انا ممكن من خلال متابعتي ل **get**,**post** اقدر اعرف هل في **c2**بيحصل ولا لا

### Exploit kits & Spotting

ده **attack tatics** عباره عن انه مثلا موقع زي تويتر او فيس بوك وغيره عليه اعلانات مثلا فا انا قدرت احط **malware**

جوه اعلانات ديه فا من تحميل اعلان ال **malware** وصلك او مثلا غير كده لما تحاول تخش علي موقع تروح تتحول لسيرفر بتاع ال **attacker** فا كده ال **request** راح ل **attacker** فا من خلال المعلومات اللي في ال **request** يعمل **malware** مخصوص ليك

طب ازاي اقفشه من خلال اني اتابع الدومينز و الهوستس اللي بتاعمل معاها واشوف هما بيعتولي ايه وكده

**HTTPS**

بيستعمل TLS لتشفير الداتا بيصعب مراقبه الترافيك شويه فا ممكن ال attacker يستغل النقطه ديه ويحط malware

### TLS Decryption

اني لو في شركه مثلا وعايز افتح يوتيوب مثلا فا بروح اعملhttp request فا بعدها جهاز فك التشفير يروح واخد الطلب ده قبل ما يوصل لسيرفر ويرد مكان سيرفر علي المتصفح اللي انا فاتح منه وكده معمول اتصال بين البراوزر وبين جهاز فك التشفير وبعدها جهاز فك التشفير يعمل اتصال بينه وبين سيرفر اليوتيوب من خلال انه يتعامل كانه البراوزر ويتعامل عادي بمعني انه من ناحيه بيكون البراوزر ومن ناحيه بيكون سيرفر وكده يقدر يشوف اللي داخل الشبكه واللي خارج منها ويقدر ياخد نسخها يبعتها لids مثلا

![](<../.gitbook/assets/19 (2).jpeg>)

ports,ip,certificate,traffic size اعمل ايه بعمل الطبيعي اني ابص علي decryption device طب لو انا معنديش

### JA3, JA3S, and JARM TLS Fingerprints

يعني ايه الكلام ده tls connection ل passive fingerprinting دول ja3,ja3s ال

معناه انه اي app مثلا بيجي يعمل tls connection مع اي سيرفر بيبعت حاجه اسمها client hello وديه زي ال syn كده في ال tcp connection فا السيرفر بيرد عليه ب server hello وديه زي ال ack في ال tcp connection بيتسحب منهم بقي ال ja3,ja3s علشان نعرف السيرفر او app سليم ولا لا

اما ال jram ده بيكون ال active fingerprinting بمعني انه بيبادر بارسال client hello فا سيرفر يرد عليه فا بناء علي الرد ده بقدر اعرف هل السيرفر ده سليم ولا

### 7. Understanding SMTP and Email <a href="#toc125846" id="toc125846"></a>

### Email Delivery Infrastructure, MTAs In Detail

![](<../.gitbook/assets/20 (2).jpeg>)

**MUA**>>> Message User Agent

**MTA**>>>Message Transfer Agent

ايميل بيبعت ازاي

ال **MUA** ده ال agent المسئول عن ارسال الايميلات من جهازك ل mail server بتاعك اللي هو **MTA**

ومن **MTA** بيروح يدورعلي **MX** **RECORD** بتاعت الدومين اللي عايز يبعتله بعد ما يلاقيه يبدا يبعت ل **MTA** اللي هناك عن طريق **SMTP**ومن **MTA** بيبعت ل **MUA** اللي مفروض توصله رساله

### SMTP Protocol

ال **SMTP** شغال ازاي

SRC MTA يعرف ال DEST MTA ده مهمته انه ال **EHLO** ال SRC MTA >>DEST بتبعت مين اللي هيبعت ايميل **MAIL** **FROM** ال MTA

ال **RCPT** مين اللي هيستقبل

### Email Headers

**Trace headers**

**Message headers**

**Body**

ال **TRACE HEADER** هنا مكتوب الايميل

عدي علي ايه علشان يوصل

to هنا بيكون فيه **MESSAGE HEADER** ال

/from /subject /content type بيكون attachment هنا بيعرض لو في **BODY** ال encode base 64

للايميل فا لازم تبقي عارف انه موضوع بشكل عكسي بمعني انه tracing لو عايز تعمل **Tracing an Email**

اخر حاجه اتعملت هي اللي بتكون ظاهره

### Interpreting A Received Header Line, Email spoofing

اللي بيستقبل الرساله بيشوف من خلال الheader جي من انهي دومين و ip بتاع دومين وجي من انهي mail exchange وكل ده علشان امنع ال **spoofing**

زمان ال **smtp** مكنش فيه حاجات تمنع ال **Spoofing** فا اتعمل بقي تلات حلول **SPF** ,**DKIM** ,**DMARC**

### Spoofed Email Injection

معناها انه انا ببعت لحد ايميل حد دخل في النص عمل inject لايميل او مثلا حد انتحل شخصيه حد فا بعتلي ايميل فيه attachment فا فتحتها فا لبست malicious file فا علشان نأمنا نفسنا بنستعمل

**SPF** >>>Sender Policy Framework ده علشان يتاكد انه مصدر ايميل

**DKIM**>>>Domain Keys Identified Mail لتاكد انه ايميل وهو بيبعت محصلوش حاجه **DMARC** >>>Domain-based Message Authentication, Reporting بيمنع التعديل علي بولسي

### SPF

عندنا مثلا ip 1.1.1.1 وفي ip 6.6.6.6 ده بتاع attacker

فا 1.1.1.1 عايز يبعت ل **MUA** معين فا ال **attacker** دلوقتي عايز يبعت بدل من ال 1.1.1.1 فا ال **dest** هترفض لانها محدده مين اللي هيبعتلها

#### auth result وكمان في dest بتاع email header بتظهر في SPF بتاعت ال result ال

وليها اشكال

زي **pass** ده كده تمام سليم

وفي **fail** ده مرفوض اصلا مش سليم

وفي **none** ده مش متحدد نوع معين

**fail** و **none** ده بين **soft** **fail** وفي **ال**

### DKIM

هنا هو معتمد علي DIGITAL SIGNTUARE بمعني انه ايميل بيتحط فيه SIGNTUARE

فا ال reciver بيشوف ال SIGNTUARE وبيتاكد منها لو تمام يبقي خلاص مفيش اي حاجه اتعدلت في ايميل

طب موضوع بيتم ازاي بردو من خلال انه ايميل بيتشفر ب private key فا علشان يتفك بيحتاج public key اللي بيكون مع الريسيفر

**One Final Problem: How Many "From" Addresses?**

في البريد بيكون مكتوب الشخص اللي بعت نقول مثلا محمد والشخص اللي استلم احمد بس من جوه الي عزيزي حسين فا ديه بردو موجوده في ايميلات

انه تكون ال from اللي ظاهره قدامك مثلا انه ايميل جي من الجامعة لكن هو في اساس في حته بتاعت ال mail from ايميل تابع ل attacker فا اللي بتعمل check لحل موضوع ده هي dmarc

### DMARC

هنا في **DMARC** لازم الدومين يكون مظبوط وال IP مظبوط +شروط **SPF** ,**DKIM** لانه ال DMARC هي دمج من الاتنين بيتاكد انه ال **RETRUN** **PATH** **=EMAIL**

**RFC5322>>FROM**

**RFC5321>>MAIL FORM**
