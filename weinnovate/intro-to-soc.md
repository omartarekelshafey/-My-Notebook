# intro to soc

P**eople**

الجزء ده بيتكلم عن إن أي SOC (Security Operations Center) مش هينجح من غير الناس اللي شغالين فيه.\
جواه:

* **Employees (الموظفين)**: عددهم، كفاءاتهم.
* **Roles & Hierarchy (الأدوار والتسلسل الوظيفي)**: مين بيعمل إيه، ليدر – محلل – محقق.
* **People Management (إدارة الموارد البشرية)**: التوظيف، توزيع الشغل، الحوافز.
* **Knowledge Management (إدارة المعرفة)**: إزاي بنخزن ونشارك المعلومات والخبرة داخل الفريق.
* **Training & Education (التدريب والتعليم)**: تدريب مستمر علشان يواكبوا الهجمات الجديدة والتقنيات.

***

#### 2- **Process (العمليات)**

ده الجزء اللي بيحط القواعد والإجراءات اللي الـ SOC بيمشي عليها.\
جواه:

* **SOC Management (إدارة مركز العمليات)**: الإدارة اليومية للمركز.
* **Operation & Facilities (التشغيل والبنية)**: المكان، الشفتات، الأدوات.
* **Reporting & Communication (التقارير والتواصل)**: إزاي نبلغ عن الحوادث ونوصلها للإدارة.
* **Detection Engineering (هندسة الاكتشاف)**: كتابة واختبار القواعد اللي تكشف الهجمات.
* **Use Case Management (إدارة حالات الاستخدام)**: تحديد السيناريوهات الأمنية اللي هنراقبها.

***

#### 3- **Services (الخدمات اللي بيقدمها الـ SOC)**

ده قلب الشغل الفعلي للـ SOC.

* **Security Monitoring (المراقبة الأمنية)**: متابعة الأحداث والتنبيهات لحظة بلحظة.
* **Incident Management (إدارة الحوادث)**: التعامل مع أي اختراق أو هجوم.
* **Digital Forensics (التحليل الجنائي الرقمي)**: التحقيق العميق بعد الهجوم لمعرفة التفاصيل.
* **Threat Hunting (صيد التهديدات)**: البحث الاستباقي عن أنشطة مشبوهة.
* **Threat Intelligence (معلومات التهديدات)**: الاستفادة من بيانات عن الهجمات اللي بتحصل في العالم.
* **Vulnerability Management (إدارة الثغرات)**: متابعة الثغرات وسدها.
* **Log Management (إدارة السجلات)**: جمع وتحليل اللوجات.

#### 4- **Technology (التكنولوجيا)**

الأدوات والمنصات اللي بيدير بيها الـ SOC شغله:

* **SIEM (Security Information and Event Management)**\
  ده الأساس اللي بيجمع اللوجات من كل الأنظمة (سيرفرات، شبكات، تطبيقات) ويعمل correlation علشان يطلع Alerts.
* **EDR (Endpoint Detection and Response)**\
  بيشتغل على الأجهزة (Endpoints) علشان يكشف ويرد على أي نشاط ضار أو اختراق.
* **NDR (Network Detection and Response)**\
  بيراقب الترافيك في الشبكة نفسها ويكشف أي سلوك غير طبيعي.
* **SOAR (Security Orchestration, Automation and Response)**\
  بيعمل أوتوميشن (Automation) للتعامل مع التنبيهات عشان يسرّع وقت الاستجابة ويقلل ضغط الشغل على المحللين.

***

#### 5- **Business (الأعمال)**

الـ SOC مش شغال لوحده، هو جزء من البزنس، فلازم يكون في توافق مع أهداف الشركة.\
جواه:

* **Drivers (المحركات/الدوافع)**\
  إيه اللي بيخلي الشركة تستثمر في الـ SOC (قوانين – هجمات متزايدة – متطلبات العملاء).
* **Customers (العملاء)**\
  سواء داخليين (أقسام الشركة) أو خارجيين (شركات تانية لو SOC مُدار).
* **Charter (الميثاق/التفويض)**\
  وثيقة بتحدد بالظبط مسئوليات الـ SOC، إيه اللي جوه نطاق عمله وإيه اللي برا.
* **Governance (الحوكمة)**\
  إزاي الـ SOC بيتوافق مع سياسات الشركة وأهدافها.
* **Privacy & Policy (الخصوصية والسياسات)**\
  التأكد إن شغل الـ SOC متوافق مع قوانين الخصوصية زي GDPR أو القوانين المحلية.



تمام 👌 خلينا ناخد **سيناريو واقعي لهجوم Ransomware** ونمشي فيه خطوة بخطوة ونشوف إزاي الأربع محاور (People – Process – Services – Technology – Business) بيشتغلوا مع بعض، وكل واحد دوره إيه داخل الـ SOC:

## example



### 🎯 السيناريو:

شركة اتعرضت لهجوم **Ransomware**، الموظف فتح إيميل Phishing فيه ملف خبيث، الملف بدأ ينفذ أوامر على الجهاز وينتشر في الشبكة.

***

### 1️⃣ **People (الناس)**

الـ SOC مش روبوت، هو قايم على البشر:

* **Employees**:\
  المحللين (Level 1) أول ناس يشوفوا التنبيه من الـ SIEM.
* **Roles & Hierarchy**:
  * **L1 Analyst**: يراجع التنبيه ويشوف إذا كان False Positive ولا حقيقي.
  * **L2 Analyst**: يبدأ تحليل أعمق (Logs، Malware behavior).
  * **Incident Responder**: يعزل الأجهزة المصابة ويتابع الإجراءات.
  * **SOC Manager**: يتابع الحادث على مستوى الإدارة ويتواصل مع باقي الأقسام.
* **Knowledge Management**:
  * فيه Runbooks وPlaybooks جاهزة بتشرح إيه الخطوات اللي لازم تتعمل في حالة Ransomware.
* **Training & Education**:
  * الموظفين مدربين إزاي يتعاملوا مع حوادث من النوع ده علشان يقللوا وقت الاستجابة.

📌 **الخلاصة:** الناس هنا هم اللي بيشغلوا كل حاجة، بيحللوا، بيردوا، وبينسقوا بين بعض.

***

### 2️⃣ **Process (العمليات)**

الـ Process هي القوانين والإجراءات اللي بتوجه الشغل:

* **SOC Management**:\
  منظمين الشفتات، فدايمًا في حد متابع اللوجات 24/7.
* **Reporting & Communication**:\
  L1 يكتب Report ويرفعه لـ L2 → Incident Response Team → SOC Manager → CISO.
* **Detection Engineering**:\
  كان فيه Rules معمولة قبل كده في الـ SIEM علشان تكشف سلوكيات Ransomware (زي إنشاء ملفات كتيرة بسرعة أو محاولة تشفير).
* **Use Case Management**:\
  عندهم Use Cases زي "Malware spreading" أو "Suspicious PowerShell execution"، اتفعلت وطلعت Alert.
* **Operation & Facilities**:\
  في غرفة SOC نفسها فيه شاشات Monitoring، تيم شغال، واتصالات مع الـ IT Team لعزل الأجهزة.

📌 **الخلاصة:** الـ Process بتضمن إن كل حاجة ماشية بخطوات منظمة ومحدش يشتغل بعشوائية.

***

### 3️⃣ **Services (الخدمات اللي بيقدمها الـ SOC)**

هنا بيبان شغل الـ SOC الحقيقي:

* **Security Monitoring**:\
  SIEM بيلم Logs ويكشف إن جهاز معين بيعمل اتصالات مشبوهة.
* **Incident Management**:\
  بيطبقوا Playbook خاصة بـ Ransomware → يعزلوا الأجهزة المصابة → يبلغوا الإدارة → يبدأوا Response Plan.
* **Digital Forensics**:\
  الفريق ياخد نسخة من الجهاز المصاب → يحللوا الـ Malware → يشوفوا إيه الـ Files اللي اتشفرّت.
* **Threat Hunting**:\
  قبل ما الهجوم يكمل، يبدأوا يدوروا في الشبكة: هل في أجهزة تانية مصابة؟ هل في Indicators of Compromise (IoCs) ظهرت في باقي الأجهزة؟
* **Threat Intelligence**:\
  يراجعوا قواعد بيانات Threat Intel → يلاقوا إن الـ Hash بتاع الملف الخبيث معروف كـ Ransomware عائلة معينة.
* **Vulnerability Management**:\
  يشوفوا إذا كان المهاجم استغل ثغرة معروفة → يطلبوا من IT Team يعملوا Patch.
* **Log Management**:\
  يحللوا كل اللوجات (AD logs، Firewall logs، Endpoint logs) علشان يعرفوا مصدر الهجوم.

📌 **الخلاصة:** الخدمات دي هي اللي بتحول الهجوم من كارثة → لحدث يتم احتواؤه والسيطرة عليه.

***

### 4️⃣ **Technology (التكنولوجيا)**

الأدوات هنا بتسند التيم:

* **SIEM**: كشف الأنشطة الغريبة (PowerShell commands، File creation patterns).
* **EDR**: ظهر Alert إن الجهاز بيشفر ملفات، الـ EDR عزل الجهاز تلقائيًا (Containment).
* **NDR**: شاف اتصالات من الجهاز المصاب لسيرفر C2 (Command & Control).
* **SOAR**: عمل Automation → بعت Incident Ticket + نفذ Playbook لعزل الأجهزة المصابة أوتوماتيك.

📌 **الخلاصة:** التكنولوجيا بتسرّع الشغل، وتدي الفريق Visibility كاملة على اللي بيحصل.

***

### 5️⃣ **Business (الأعمال)**

* **Drivers**: الشركة عاملة SOC أصلًا علشان تحمي نفسها من خسائر زي دي.
* **Customers**: قسم الـ Finance مثلًا اتأثر لأن ملفاتهم اتشفرّت → SOC يتواصل معاهم.
* **Charter**: الحادث داخل نطاق مسئولية الـ SOC، فهما اللي بيقودوا الاستجابة.
* **Governance**: لازم يتأكدوا إنهم بيلتزموا بالقوانين المحلية لتقرير الحوادث.
* **Privacy & Policy**: الهجوم أثر على بيانات حساسة، فلازم يراعوا قوانين حماية البيانات (مثال GDPR).

📌 **الخلاصة:** البزنس بيضمن إن شغل الـ SOC aligned مع القوانين وأهداف الشركة مش بس الجانب الفني.

***

### 🔑 **النتيجة النهائية للسيناريو:**

* **People**: شافوا التنبيه، حللوه، واتبعوا Playbook.
* **Process**: وفرلهم خطوات منظمة علشان ما يضيعوش وقت.
* **Services**: نفذوا الاستجابة كاملة (Monitoring → Hunting → Forensics).
* **Technology**: وفرت Visibility + أوتوميشن.
* **Business**: ضمنوا التزام بالقوانين، وحافظوا على سمعة الشركة.

**وقولي لو كل واحد وقع ايه اللي يحصل**

### ️ طيب لو كل واحد وقع إيه اللي هيحصل؟

#### 1️⃣ **لو People وقعوا (الناس مش موجودة أو غير مدربة):**

* التكنولوجيا هتدي Alerts، لكن **مفيش حد يفهمها أو يحقق فيها**.
* SOAR ممكن يعمل Automation لحد ما، بس مش هيحلل ولا يقرر استراتيجيات.
* النتيجة → الـ SOC هيبقى شبه Automated Monitoring بس، ومش هيقدر يرد بذكاء على الهجمات.\
  📌 **أخطر حاجة تقع هي People.**

***

#### 2️⃣ **لو Process وقع (مفيش إجراءات أو Playbooks):**

* الفريق موجود والأدوات موجودة، لكن كل حادثة هيتعاملوا معاها بعشوائية.
* ممكن محلل يرد بسرعة، وممكن تاني يبطأ → مفيش Consistency.
* النتيجة → هجوم كبير زي Ransomware ممكن يضيع وقت كتير قبل ما يتم احتواؤه.\
  📌 **التأثير هنا Chaos (فوضى)، بس الناس والخبرة ممكن يعوضوا جزئيًا.**

***

#### 3️⃣ **لو Services وقعت (Monitoring/IR/Hunting مش شغالين):**

* ده يعني إن الـ SOC مش بيقدم خدمات فعلية → شبه مش موجود.
* التكنولوجيا شغالة، بس **مفيش Value حقيقية بتوصل للبزنس**.
* النتيجة → هجمات تعدي بسهولة، الإدارة هتعتبر الـ SOC useless.\
  📌 **ده معناه شلل كامل في الوظيفة الأساسية للـ SOC.**

***

#### 4️⃣ **لو Technology وقعت (SIEM, EDR, NDR, SOAR):**

* الفريق هيبقى شغال manual: يجمع Logs بإيده، يعمل Hunting يدوي، يحقق في الأجهزة من غير Visibility.
* هيقدروا يردوا بس ببطء جدًا.
* النتيجة → ممكن ينجحوا في حوادث صغيرة، لكن هجوم ضخم هيعدي لأن مفيش سرعة أو أوتوميشن.\
  📌 **ده كارثي، بس الناس + العمليات ممكن ينقذوا الوضع مؤقتًا.**

***

#### 5️⃣ **لو Business وقع (مفيش Drivers/Charter/Policies):**

* الـ SOC يشتغل تقنيًا، لكن:
  * مفيش تمويل كافي → الأدوات تتعطل.
  * مفيش وضوح نطاق عمل → الفريق يتدخل في حاجات مش مسئوليته أو العكس.
  * مفيش حوكمة → ممكن يخالف قوانين (زي GDPR).
* النتيجة → البزنس يفقد الثقة في الـ SOC أو يقفله.\
  📌 **التأثير هنا بطيء وتدريجي، مش مباشر زي باقي الأعمدة.**

***

### 🔑 الخلاصة:

* **الأخطر لو وقع → People أو Services** → الـ SOC هيتشل فورًا.
* **Process & Technology** → لو وقعوا التأثير كبير جدًا، بس ممكن يتعوضوا مؤقتًا بالخبرة أو الشغل اليدوي.
* **Business** → أقلهم تأثير مباشر قصير المدى، لكنه بيهدم الـ SOC على المدى الطويل.



### 🔗 العلاقات بين الأعمدة:

#### 1️⃣ **People ↔ Process**

* الـ People محتاجين **Process** علشان يشتغلوا بشكل منظم (Playbooks, SOPs).
* والـ Process محتاجة **People** ينفذوها.\
  📌 مثال: في Incident Response، من غير Runbook (Process) المحلل ممكن يتلخبط. ومن غير محلل (People) الـ Runbook مش هيتنفذ.

***

### 2️⃣ People ↔ Technology

* الأدوات (Technology) لوحدها مش هتدي قيمة من غير ناس (People) يعرفوا يظبطوها، يفسروا نتايجها، ويبنوا Rules مناسبة.
* والناس (People) من غير أدوات (Technology) مش هيكون عندهم **Visibility** كفاية علشان يشوفوا الهجمات أو يحللوها.

***

#### 3️⃣ **People ↔ Services**

* الـ Services (Monitoring, Incident Response, Hunting) محتاجة ناس ينفذوها.
* والناس قيمتهم للشركة بتبان من خلال الـ Services اللي بيقدموها.\
  📌 مثال: Threat Hunting = نشاط بشري يعتمد على خيال المحلل + أدوات.

***

#### 4️⃣ **Process ↔ Services**

* الخدمات مبنية على خطوات Process محددة.
* لو مفيش Process → الـ Services هتتنفذ بشكل عشوائي.\
  📌 مثال: Incident Response Service لازم تمشي على Process: Detection → Containment → Eradication → Recovery.

***

#### 5️⃣ **Technology ↔ Services**

* كل Service معتمدة على Tool:
  * Monitoring → SIEM.
  * Incident Response → SOAR + EDR.
  * Forensics → أدوات تحليل.
* من غير Technology، الـ Services هتتباطأ جدًا أو تبقى شبه مستحيلة.

***

#### 6️⃣ **Business ↔ Services**

* الشركة بتموّل SOC علشان الـ Services دي تتحقق.
* ولو الـ Services مش واضحة → البزنس ممكن يوقف الدعم (فلوس/أدوات/توظيف).\
  📌 مثال: الإدارة مهتمة بخدمة Incident Management → لازم الـ SOC يثبت إنه بيمنع خسائر مالية.

***

#### 7️⃣ **Business ↔ People**

* لو الإدارة مش بتدعم التدريب أو التوظيف → الناس هتقل كفاءة.
* ولو الناس مش بتدي Value للبزنس → الإدارة هتعتبر SOC “cost center” مش “value center”.

***

#### 8️⃣ **Business ↔ Process**

* الحوكمة والسياسات (Policies) بتيجي من البزنس → ودي بتحدد الـ Process.

والـ Process بدورها تثبت إن الشركة ملتزمة بالقوانين (GDPR, ISO, PCI DSS).

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## إيه هو الهرم وليه مهم؟

اتقدّم من David J. Bianco. بيقسّم أنواع الـIndicators/Signals اللي بنعتمد عليها في الكشف إلى 6 طبقات (من تحت لفوق):

1. **Hash Values**
2. **IP Addresses**
3. **Domain Names**
4. **Network & Host Artifacts**
5. **Tools**
6. **Tactics, Techniques & Procedures (TTPs)**

هنشرح كل طبقة: معناها، أمثلة، ازاي المهاجم يتهرّب منها، وإنت تعمل إيه كمدافع.

***

### 🔻 1) Hash Values (MD5/SHA1/SHA256)

**يعني إيه؟** بصمة ملف معيّن.\
**سهل على المهاجم يتفاداها؟** جدًّا—يغيّر بايت/يعيد تجميع الكود → Hash جديد.\
**مصادرك:** AV/EDR detections، Malware sandbox.\
**اعمل إيه؟** استخدمها كـ **IOC قصير العمر** (block/contain سريع)، لكن ما تعتمدش عليها وحدها. اربطها بسياق: مين نزّل الملف؟ اتشغّل إزاي؟ اتوصّل بمين؟

**الخلاصة:** أقل وجع للمهاجم، أسهل عليك.

***

### 🔻 2) IP Addresses

**يعني إيه؟** عناوين C2، استضافة phishing، proxies.\
**تفادي المهاجم؟** سهل—IP rotation, cloud/VPS.\
**مصادرك:** Firewall/Proxy logs, Threat Intel feeds.\
**اعمل إيه؟** بلوك مؤقت + راقب الـASN/الـCloud Provider والـ/24 لما ينفع. استخدم reputation + geo + frequency.

**الخلاصة:** وجع بسيط للمهاجم، ما زال سهل يغيّر IP.

***

### 🔻 3) Domain Names

**يعني إيه؟** دومينات C2/Phishing/DGA.\
**تفادي المهاجم؟** متوسط—هيحجز دومين جديد أو DGA، بس ده بياخد فلوس/تنسيق.\
**مصادرك:** DNS logs (resolver, EDR DNS telemetry)، Passive DNS، TI.\
**اعمل إيه؟**

* راقب **features**: عمر الدومين، سجلّات DNS الغريبة، NXDomain bursts (DGA).
* استخدم blocklists ولكن اعمل **alerting على السلوك** (اتصالات كثيرة لدومينات جديدة/حديثة).

**الخلاصة:** وجع أعلى من IP، ولسه مش كافي لوحده.

***

### 🔺 4) Network & Host Artifacts

**يعني إيه؟** آثار سلوكية محددة:

* **Network:** User-Agent شاذ، URI pattern، TLS JA3/JA3S fingerprint.
* **Host:** Registry keys، Mutex names، service names، file paths، scheduled tasks، command-line patterns.\
  **تفادي المهاجم؟** أصعب—لازم يغيّر سلوك/بِنية التشغيل، مش مجرد IP.\
  **مصادرك:** EDR telemetry، Sysmon، NetFlow/PCAP، Proxy.\
  **اعمل إيه؟** ابني قواعد على **السلوك**:
* أمثلة ويندوز:
  * إنشاء Scheduled Task باسم مريب بعد PowerShell.
  * استعمال `vssadmin delete shadows` أو `wbadmin` (سلوك فدية).
  * إنشاء ملف في `%ProgramData%` متبوع بخدمة جديدة بنفس الاسم.
* أمثلة شبكة:
  * نفس UA ثابت لعدة أجهزة نحو نفس الـC2، URI بطول/نمط ثابت، JA3 fingerprint معروف لأداة.

**الخلاصة:** هنا بتبدأ توجّع المهاجم بجد.

***

### 🔺 5) Tools

**يعني إيه؟** أدوات الهجوم نفسها: Cobalt Strike/Sliver, Rclone, Mimikatz, AnyDesk/ScreenConnect (abuse), SharpHound…\
**تفادي المهاجم؟** صعب—يحتاج يبدّل toolset أو يطوّر واحد جديد/يعدّل بشدة.\
**مصادرك:** EDR (process lineage, module loads, strings), YARA, memory forensics.\
**اعمل إيه؟**

* قواعد لاكتشاف **سمات الأداة** (beaconing pattern، named pipes، default malleable profiles، DLL export names، parent-child غريب).
* YARA على الذاكرة/الملفات، كمان **behavior** للأدوات الشرعية المُساء استخدامها (AnyDesk unattended install مفاجئ، ScreenConnect MSI drop + service).

**الخلاصة:** وجع كبير للمهاجم لأن تغيير الأدوات مكلف.

***

### 🔺 6) TTPs (MITRE ATT\&CK)

**يعني إيه؟** **طريقة اللعب نفسها**: كيف يتحرك/يثبّت/يجمع/ي exfil.\
أمثلة:

* T1059 (Command & Scripting: PowerShell)،
* T1047 (WMI)،
* T1021.002 (SMB lateral movement)،
* T1003 (Credential Dumping)،
* T1486 (Data Encrypted for Impact).\
  **تفادي المهاجم؟** مؤلم جدًا—لازم يغيّر **التكتيك** بالكامل، وده بيأثر على خطته وزمنه وكُلفته.\
  **مصادرك:** ATT\&CK mapping، EDR + SIEM behavioral analytics، Hunt notebooks.\
  **اعمل إيه؟** ابنِ **use cases** سلوكية عامة:
* “Parent = Office → Child = Powershell + AMSI bypass strings”
* “lsass.exe access + comsvcs.dll MiniDump”
* “大量 إنشاء ملفات + حذف ظلال النسخ + تعطيل AV”
* “RDP enabled suddenly + new local admin + lateral SMB copy + service creation”.

**الخلاصة:** أعلى وجع للمهاجم، وأعلى قيمة دفاعية ليك—even لو غيّر IP/Hash/Domain.

***

### ملخص سريع (مين بيتألم ومين بيتعب)

| الطبقة    | سهولة تغييرها للمهاجم | وجع المهاجم لو منعتها | مجهودك كمدافع | العمر الافتراضي |
| --------- | --------------------- | --------------------- | ------------- | --------------- |
| Hash      | سهل جدًا              | ضعيف                  | قليل          | قصير جدًا       |
| IP        | سهل                   | ضعيف–متوسط            | قليل          | قصير            |
| Domain    | متوسط                 | متوسط                 | متوسط         | متوسط           |
| Artifacts | أصعب                  | عالي                  | متوسط–عالي    | أطول نسبيًا     |
| Tools     | صعب                   | عالي جدًا             | عالي          | أطول            |
| TTPs      | صعب جدًا              | **أعلى**              | **أعلى**      | الأطول والأعم   |

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>





#### ✨ **الأسئلة الأساسية المكتوبة:**

1. **The true power of logs?**
   * يعني: إيه القوة الحقيقية للـ Logs؟
   * القوة مش في الكمّ، لكن في **المعلومة اللي بتديك إجابة شاملة عن الحادثة**.
2. **Where does it come from?**
   * القوة دي بتيجي من **قدرة الـ Logs إنها تجاوبك على أسئلة التحقيق والتحليل**.
3. **What does logs answer?**
   * الـ Logs بتجاوب على أهم أسئلة في أي Incident أو Event.
4. **What is 5W’s?**
   * دي الخلاصة: إن الـ Logs بتجاوب على **5 أسئلة أساسية** عشان تفهم أي حادثة:

***

#### 🟢 **الـ 5W’s (مبينين في الدائرة):**

1. **Who** → مين عمل الـ action؟
   * مثال: الـ user account، الـ process، الـ IP.
2. **What** → إيه اللي حصل بالظبط؟
   * مثال: تم login، تم إنشاء ملف، تم حذف خدمة.
3. **Where** → فين حصل الحدث؟
   * مثال: السيرفر، الـ endpoint، الـ subnet، الـ geo-location.
4. **When** → إمتى حصل؟
   * Timestamp، duration، frequency.
5. **Why** → ليه حصل؟ (أصعب واحدة)
   * مش موجودة دايمًا بشكل مباشر في اللوج، لكن ممكن تستنتجها من باقي الـ context.
   * مثال: login failed كتير → محاولة brute force.

***

#### 🎯 **الخلاصة:**

* **القوة الحقيقية للـ Logs** = إنها بتخليك تجيب إجابة كاملة عن أي Incident عن طريق الـ **5W’s**.
* أي Log كويس لازم يوفرلك على الأقل **Who + What + Where + When**، ومع التحليل تقدر تستنتج **Why**.
* ده أساس أي تحقيق Forensics أو Incident Response أو حتى SIEM Rule.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Siem Architecture  Components

تمام ✅ خلينا نشرح **SIEM Architecture Components** خطوة بخطوة، وكأننا ماشيين بالـ Logs من أول ما تتجمع لحد ما تتحول لمعلومة مفيدة للـ SOC Analyst:

***

### SIEM Architecture Components

#### **Collection (التجميع)**

* أول خطوة: الـ **SIEM** لازم ياخد Logs من مصادر مختلفة زي:
  * Firewalls
  * IDS/IPS
  * Servers
  * Applications
  * Endpoints
* الهدف: **Centralization** (تجميع كل الأحداث في مكان واحد).
* مثال: السيرفرات والفايروول يبعثوا Syslog للـ SIEM.

***

#### **Parsing (تحليل الخام)**

* الـ Logs عادةً بتكون نصوص غير منظمة (Raw Logs).
* Parsing يعني: **استخراج الحقول المهمة** من الـ Log.
*   مثال:

    ```
    Jan 10 10:00:01 firewall01 Deny TCP 192.168.1.10 → 8.8.8.8 Port 443
    ```

    بعد الـ Parsing:

    * Action = Deny
    * Protocol = TCP
    * Source IP = 192.168.1.10
    * Destination IP = 8.8.8.8
    * Destination Port = 443

***

#### **Normalization (توحيد الشكل)**

* كل جهاز بيطلع Logs بشكل مختلف.
* الهدف: **توحيد صيغة الحقول** بحيث الـ SIEM يعرف يقارن الأحداث ببعض.
* مثال:
  * Firewall يقول `src_ip`
  * Server يقول `client_address`
  * SIEM يوحدهم باسم `Source IP`.

***

#### **Aggregation (التجميع/التلخيص)**

* بدل ما نسجل كل Log لوحده → الـ SIEM يعمل **Group** للأحداث المتشابهة.
* الهدف: تقليل الحجم + التركيز على الـ Pattern.
* مثال:
  * لو 1000 محاولة Login فاشلة من نفس الـ IP في دقيقة → يتجمعوا كـ "Failed Logins from 192.168.1.50 (1000 times)".

***

### &#x20;Correlation (الربط)

* **الوظيفة:** ربط أحداث مختلفة ببعض عشان تكشف Attack Scenario.
* **الفكرة:** مش مجرد تكرار نفس الحاجة، لكن أحداث متنوعة مرتبطة ببعض بتدل على هجوم.
*   **مثال:**

    1. User عمل Login ناجح من روسيا.
    2. نفس User بعد دقيقتين بيعمل Data Download ضخم من السيرفر.
    3. نفس الـ User قبلها كان فيه 50 فشل Login.

    الـ SIEM يربط الـ Events دي مع بعض = Suspicious Behavior → ممكن يكون Account Compromise.

***

### What types of events should be logged?

***

### &#x20;أنواع الـ Events اللي لازم تتسجل (Logging)

**Failures / Errors**&#x20;

* دي بتسجل الأخطاء اللي بتحصل عشان نعرف سبب المشكلة.
* مثال:
  * فشل في الـ Login.
  * Application وقع.
  * File مش لاقيه (file not found).

***

&#x20;**Analytics / Usage Logs**&#x20;

* دي بتساعدنا نفهم إزاي الـ System بيتستخدم وأداءه عامل إزاي.
* مثال:
  * أكتر API مستخدم.
  * وقت استجابة الـ API.
  * الـ User عمل إيه (download, delete, login…).

***

&#x20;**System & Security Logs**&#x20;

* دي الـ Logs الأساسية اللي بتيجي من الـ OS والـ Services:
  * **Application Log** → أخطاء أو معلومات من البرامج.
  * **Security Log** → أي نشاط أمني (login, logout, policy changes).
  * **System Log** → مشاكل في الـ OS أو الـ Drivers.
  * **DNS Log** → استعلامات الـ DNS.
  * **Directory Service Log** → أحداث Active Directory.
  * **File Replication Log** → مشاكل في AD Replication.

***

&#x20;**الخلاصة**:\
نسجل كل حاجة ليها قيمة فعلية:

* Errors عشان نحل مشاكل.
* Usage عشان نتابع الأداء.
* Security/System Events عشان نأمن ونفهم البنية التحتية.

***

### &#x20;إزاي الأجهزة بتبعت الـ Logs للـ SIEM؟

عشان الـ SIEM يشتغل، لازم كل جهاز (Server, Firewall, Switch, Endpoint…) يبعت له الـ Logs بتاعته.\
ده بيتم بطريقتين أساسيين:

***

#### **Log Shippers**&#x20;

* دي Tools بتتسطب على الجهاز أو السيرفر عشان **تجمع الـ Logs وتعالجها وتبعتها للـ SIEM**.
* بتعمل:
  * **Collect** → تجمع الـ Logs من ملفات أو Event Viewer.
  * **Parse / Format** → تظبط شكل الـ Logs (JSON, key=value…).
  * **Ship** → تبعتها للـ SIEM.

🛠️ أمثلة مشهورة:

* **Filebeat** (من Elastic).
* **Fluentd**.
* **NXLog**.

***

#### &#x20;**Protocols** 📡

فيه بروتوكولات (طرق تواصل) بتسمح للأجهزة تبعت الـ Logs مباشرة:

* **Syslog** (أشهر بروتوكول):
  * بيشتغل على TCP/UDP.
  * معظم الـ Firewalls, Routers, Linux servers بيستخدموه.
  * بيبعت Logs بشكل Text عادي.
* **Windows Event Forwarding (WEF)**:
  * مخصوص للـ Windows Environments.
  * بيجمع الـ Windows Event Logs من أجهزة كتير ويبعتها لمكان مركزي (Collector).
  * من هناك ممكن تبعت للـ SIEM.
* **API / Agent-based**:
  * بعض الأجهزة أو الـ Cloud Services بتستخدم API تبعت Logs للـ SIEM.
  * مثال: AWS CloudTrail بيبعت الـ Logs عبر API.
* **Custom Connectors**:
  * SIEM Vendors (زي Splunk, QRadar, ArcSight) بيعملوا Connectors جاهزة للمنتجات المختلفة (زي Cisco ASA, Palo Alto).

***

#### &#x20;الحاجات الأساسية اللي أي Log لازم يحتويها:

**Timestamp (الوقت والتاريخ)**

* لازم نعرف الحدث حصل إمتى بالظبط (مع Timezone لو أمكن).

**Source Information (المصدر)**

* الـ IP Address / Hostname للجهاز أو الـ User اللي عمل الـ Action.

**Destination Information (لو فيه تواصل)**

* الـ IP / Port / Hostname اللي رايح له الترافيك.

&#x20;**Event / Action Description**

* نوع الحدث: Login, Logout, File Access, Command Execution, Network Connection…

**User / Account Information**&#x20;

* الـ Username أو الـ User ID اللي نفّذ العملية.

**Status / Result**

* نجح ولا فشل (Success / Fail / Error Code).

&#x20;**Process / Application Details**

* اسم البرنامج أو الـ Service اللي أصدر الـ Log.
* أحيانًا كمان PID (Process ID).

&#x20;**Device / Log Source Type**

* هل جاي من Firewall؟ Server؟ Endpoint؟ Application؟

