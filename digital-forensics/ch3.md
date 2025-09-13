# CH3

## Forensic laboratory within  large facility

### &#x20;(Security)

* **Physical Security**: كاميرات، دخول  بصمة، وصعوبة دخول أي حد للمعمل.
* **Logical Security**: شبكة المعمل لازم تبقى _معزولة_ عن باقي الشركة، عشان أي Evidence ما يتلوثش أو يتعرض لهجوم.

***

### &#x20;(Evidence Protection)

* **tempest /RF Shielding / Faraday Bags**: تحمي الهاردات، الفلاشات، والموبايلات من أي موجات كهرومغناطيسية أو اتصالات.
* **Anti-Static Measures**: زي الـ Anti-static pads على الترابيزات والأرضية، تمنع الكهرباء الاستاتيكية تأثر على الأدلة.
* **Cabinets**
* trash container

***

### Technical equipment

* **Forensic Workstation**: جهاز قوي مخصص للفورنسيك، مفصول عن الإنترنت.
* **Internet Access PC**: جهاز تاني منفصل للبحث/تحميل أدوات.
* **Microscope**: للأدلة التالفة (زي هارد متكسر أو chip damage).
* **Forensic Tools/Software**: زي EnCase, FTK, Autopsy, X-Ways.

***

### lab types

* **Small Lab (بيتي/شركة صغيرة)**: جهاز أو جهازين، Faraday Bag، Anti-static pad، أدوات سوفتوير فورنسيك.
* **Medium Lab (شركة/Consulting Firm)**: أجهزة أكتر، Evidence Cabinet، غرفة مخصصة مع عزل حراري وكهرومغناطيسي.
* **Large Lab (شرطة / CERT / وزارة)**:
  * Forensic Workstations متعددة.
  * غرفة منفصلة لحفظ الأدلة (Evidence Room).
  * مكاتب للمحققين (Investigators).
  * Internet Lab منفصل.

### **Accreditation lab**

* مش أي معمل Forensics يتعمل يبقى معتمد (Accredited).
* في جهات عالمية بتدي **اعتماد رسمي (Accreditation)** للمعامل علشان تثبت إن المعمل ملتزم بالـ Standards والإجراءات.

👮‍♂️ الأمثلة:

* في أمريكا فيه **ANAB (ANSI National Accreditation Board)**.
* في بريطانيا فيه **UKAS**.
* في أوروبا فيه جهات مشابهة معتمدة من الـ **ILAC (International Laboratory Accreditation Cooperation)**.

## Small lab forensics

**ايه اللي هتحتاجه لو انت في شركه صغيره**

1. **Virtualization Layer**:
   * نزّل أي **Hypervisor** (زي VMware Workstation أو VirtualBox).
   * الهدف إنك تعزل شغل الـ Forensics عن جهازك الأساسي.
2. **اختيار الـ VM**:
   * ممكن تعمل VM بـ Windows أو Linux.
   * لو Linux: عندك توزيعات معمولة للـ Forensics زي **CAINE** او **Sans sift** وغيره او انك تحمل &#x20;
   * لو Windows: هتكوّن بنفسك "ترسانة الأدوات" اللي هتستخدمها.
3. **Write Blocker (مانع الكتابة)**:
   * مهم جدًا علشان أي Evidence توصله ما يتغيرش عليه أي حاجة.
   * النوع ده بالذات أساسي لإن حتى الـ OS ساعات بيكتب Metadata على الهارد من غير ما تحس.
   * عندك نوعين:
     * **Hardware Write Blocker**:
       * جهاز خارجي بيتوصل بين الهارد والـ Workstation.
       * بيخلي الداتا تمشي في اتجاه واحد (من الهارد → الكمبيوتر).
       * آمن جدًا ومفضل في التحقيقات الرسمية.
       * أمثلة: Tableau Forensic Blocker – WiebeTech Dock.
     * **Software Write Blocker**:
       * برنامج أو Driver بيخلي الـ Disk Read-Only.
       * أمثلة: `diskpart` (Windows)، أو `mount -o ro` (Linux)، أو OSFMount.
       * ميزة: رخيص وسهل.
       * عيب: أقل أمان من الـ Hardware لإن أي خطأ في Config ممكن يكتب على الدليل.
4. **Storage إضافي**:
   * لازم يكون معاك هاردات فاضية (2TB أو أكتر).
   * السبب: ممكن تحتاج تسحب Data ضخمة أو تعمل نسختين من نفس الدليل.
5. **Cloner/Docking Station**:
   * جهاز بي Clone هارد بالكامل Sector by Sector.
   * شرط أساسي: الـ Target disk لازم يكون نفس أو أكبر من الـ Source.
6. **Tools & Software**:
   * أدوات Acquisition (لسحب البيانات من Hard/USB/Email/Browser History).
   * أدوات Analysis (لتحليل الأدلة بعد السحب).
7. **SATA/PATA adapters**: دول علشان اوصل الهارد ديسك بالجهاز

## Needed Digital forensics OS Toolkit software

### Linux Distributions for Forensics

مبدئيًا، انت ممكن تستخدم أي **Live CD** سواء ويندوز أو لينكس.

#### Live CDs and Live USBs

الـ **Live CD/USB** دي نفس الأقراص أو الفلاشات اللي بنستخدمها عشان نعمل Boot للجهاز من غير ما ننزل عليه Operating System.\
الميزة إنها بتشغل الجهاز اللي عليه المشكلة من غير ما تلمس النظام الأساسي اللي عليه، فالأدلة بتفضل محفوظة زي ما هي.

#### example



* **SANS SIFT**:معمولة مخصوص للفورينزكس.
* **CAINE**: Live USB معمول للتحقيقات الرقمية.
* **Tsurugi Linux**: توزيعة قوية للتحقيقات وتحليل الأدلة.

الميزة في التوزيعات دي إن عليها كل التولز اللي محتاجها سواء للاكتساب (**Acquisition**) أو للتحليل (**Analysis**).

ولو مش عايز تعتمد على توزيعات جاهزة، تقدر تبني الـ Arsenal الخاص بيك وتختار الأدوات اللي هتحطها بنفسك.

***

### Forensics Tools

#### Acquisition Tools

* **FTK Imager**
* **RegRipper**
* **LiME**
* **TCPDump** و **Wireshark**
* **Foremost**
* **Autopsy**

#### Analysis Tools

* **FTK Imager**
* **RegRipper**
* **Autopsy**
* **Volatility**
* **log parser studio**&#x20;
* **exif viewer**

## Daubert Standard

الـ **Daubert Standard** هو معيار قانوني بيستخدم في بعض المحاكم الأمريكية (مش كل الولايات بتطبقه، لكنه واسع الانتشار).\
فكرته الأساسية إنه بيأمّن حاجة اسمها **Rule of Evidence** أو **Evidence Law**، يعني بيحط شروط معينة تخلي القاضي أو حتى مديرك يقدر يقول إن الأدلة اللي جبتها صالحة وموثوقة أو لأ.

الـ **Daubert Law** بيقول إن أي دليل لازم يتوافر فيه 4 شروط رئيسية:

***

### 1. Testing Methodology

لازم الأدلة اللي بتقدمها تكون مبنية على **منهجية اختبار واضحة ومكتوبة**.

* وأنت بتكتب التقرير بتاعك لازم تذكر بالتفصيل:
  * إزاي عملت الـ Extraction أو الـ Analysis.
  * أي Commands أو Tools استخدمتها.
  * إزاي وصلت للنتائج (زي استخراج Process Name من الميموري).
* الهدف إن مايبقاش فيه مجال للتشكيك في خطواتك قدام المحكمة.

***

### 2. Error Rate

مفيش أي أداة أو منهجية خالية تمامًا من الأخطاء، فلازم تذكر في التقرير **نسبة الخطأ (Error Rate)**.

* الشرط إن النسبة دي تكون في مستوى مقبول (**Acceptable Level**).
* مثال:
  * لو الأداة ليها Error Rate = 50% → الأدلة تعتبر غير صالحة.
  * الطبيعي في الديجيتال فورينزكس إن الأخطاء تكون أقل من 10%، وغالبًا أقل من 1% في بعض الحالات (زي استخراج بيانات من الميتاداتا).
* مين اللي بيحدد المقبول؟ الخبير اللي تعينه المحكمة، أو المعايير المتعارف عليها في المجال.

***

### 3. Peer Review

أي دليل لازم يكون اتعمله **مراجعة من زميل/خبير تاني (Peer Review)**.

* يعني ماينفعش أنت اللي تعمل الـ Acquisition والـ Analysis وبعدين تراجع نفسك.
* لازم فيه مراجعة مستقلة من شخص مؤهل عشان الأدلة تكون موثوقة.

***

### 4. General Acceptance in the Community

الأداة أو المنهجية اللي استخدمتها لازم تكون **مقبولة ومعروفة في مجتمع الديجيتال فورينزكس**.

* وده بيبان من خلال:
  * الأبحاث الأكاديمية المنشورة (Academic Papers).
  * الدوريات العلمية (Journals).
  * شهادات مهنية مشهورة (Certifications).
  * اعتراف الخبراء في المجال.
* أي تقنية مستخدمة بشكل واسع ومعروفة  تعتبر **مقبولة** طبقًا للـ Daubert Law.

***

## Things to Consider While Working in Digital Forensics

### Authorization (Authority)

لازم يبقى معاك إذن رسمي علشان تشتغل:

* إذن من النيابة.
* أو أمر مباشر من مديرك.
* أو ممكن يبقى Job Role + Tasking واضح بالـ Scope والمدة.
* في حالة إنك شغال في Consulting ، بيبقى عندك عقد (Contract) محدد فيه الـ Scope والمدة الزمنية.

الفكرة إن وجود سلطة قانونية أو إدارية معاك بيحميك من الوقوع في انتهاك خصوصية الأشخاص.

***

### Stick to the Scope

* لازم تلتزم بالـ Scope المكتوب في الإذن أو العقد.
* أي خروج برا الـ Scope بدون إذن جديد ممكن يبوّظ القضية.
* في المحاكم، المحامي ممكن يستخدم أي خطأ إجرائي ضدك ويبرّئ المجرم.

***

### Data Handling and Acquisition

* لازم تحدد مكان تحليل البيانات: هل ينفع تطلع بره مكان الحادث ولا لأ؟
* في بعض القضايا (Live Forensics) لازم تشتغل في الموقع وما تخرجش الداتا بره.
* في الشركات: لو الـ Policy بتقول البيانات ما تخرجش بره الشركة، يبقى لازم تلتزم.
* قانونيًا: بيانات المواطنين لا يجوز تخرج خارج حدود البلد&#x20;

***

### Documentation

* لازم تسجل كل خطوة عملتها بالوقت والتاريخ.
* أي Command أو Tool استخدمتها يتحط كـ Artifact.
* وجود ورقة أو Note Taker معاك مهم جدًا علشان التوثيق.

***

### Authority vs. Power

* معاك Authority (إذن أو عقد) بس مش معاك Power مطلق.
* لازم تستأذن قبل ما تاخد جهاز من موظف أو تعمل أي Action.
* في المستوى القضائي لازم ده يبقى متوثق في مذكرة أو محضر.

***

### Clean Desk Policy

* ممنوع تسيب الأدوات أو الـ Evidence مكشوفة.
* لازم تقفل عليهم في Safe أو Drawer قبل ما تتحرك.
* الأفضل تشتغل في Secure Facility (أوضة مقفولة ومحكمة).

***

### Working Under Pressure

* الشغل هيبقى في ظروف صعبة ومع ناس مش تقنية (قاضي، وكيل نيابة، ظابط، مدير).
* لازم تبقى هادي جدًا وتفكر قبل ما ترد.
* لو الوقت مش كافي، اكتبه بوضوح في التقرير إن المدة غير كافية لإثبات/نفي نقطة معينة.
* الكومينيكيشن لازم يبقى Clear جدًا.
* في الأسئلة القانونية أو الرسمية، الردود لازم تكون Short Answer (جملة قصيرة وخمس أو ست كلمات).







