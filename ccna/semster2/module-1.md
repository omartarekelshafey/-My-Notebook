# module 1

&#x20;Configure a Switch with\
Initial Settings
----------------

### Switch Boot Sequence

**step1**:اول حاجه ال POST(Power On Self-Test)بيشتغل&#x20;

**Step 2: Loading the Boot Loader**&#x20;

* ال (Timing): بتحصل فوراً بعد ما الجهاز يخلص فحص الهاردوير (After POST).
* ال (Location): السويتش بيحمل الـ Boot Loader من ال(ROM).
* ال (Function): هو برنامج صغير جداً ومهمته الأساسية التجهيز لتحميل نظام التشغيل.

**Step 3: Low-level CPU Initialization**&#x20;

* &#x20;الـ Boot Loader بيقوم بتهيئة المعالج (CPU) عشان يقدر يشتغل.
* ال (Operations): بيضبط  (CPU Registers) المسؤولة عن حاجات زي:
  1. الMemory Mapping: تحديد فين (RAM) ومكانها فين في الخريطة.
  2. الQuantity of Memory: التعرف على حجم الذاكرة المتاحة.
  3. الSpeed: تحديد السرعة اللي الذاكرة هتشتغل بيها.

**Step 4: The boot loader initializes the flash file system on the system board.**

**Step 5: Finally, the boot loader locates and loads a default IOS operating system**\
**software image into memory and gives control of the switch over to the IOS**

<div align="center"><figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>

### Switch LED Indicators

* **System LED (SYST):**
  * الوظيفة: أهم لمبة في السويتش، بتعرفك هل الجهاز واصل له كهرباء وشغال صح ولا لأ.
  * الحالة: لو منورة أخضر ثابت يبقى الجهاز تمام.&#x20;
* **Redundant Power Supply LED (RPS):**
  * الوظيفة: دي خاصة بـ "مزود الطاقة الاحتياطي" (لو عندك بطارية أو مصدر كهرباء إضافي).
  * الحالة: بتعرفك هل المصدر الاحتياطي ده واصل وشغال ولا لأ.

**2. Port Mode Indicators (مؤشرات أوضاع المنافذ)**

دول بقى بيحددوا "لمبة البورت" بتعبر عن إيه لما الزرار (Mode) يختارهم:

* Port Status LED (STAT) - (الوضع الافتراضي):
  * الوظيفة: لما تكون اللمبة دي منورة اخضر = البورت شغال Cable connected).
* **Port Duplex LED (DUPLX):**
* لما اللمبة دي تكون خضراء، ده مؤشر إن تم اختيار وضع الـ Duplex Mode
* في الحالة دي، تقدر تفهم حالة الـ Duplex لكل منفذ (Port) عن طريق الضوء الخاص بكل منفذ.
* **Port Speed LED (SPEED):**
  * لما اللمبة دي تكون خضراء، ده مؤشر إن تم اختيار وضع Speed Mode.
  * في الحالة دي، تقدر تفهم سرعة كل منفذ (Port) عن طريق الضوء الخاص بكل منفذ.
* **Power over Ethernet LED (PoE):**
  * الملاحظة: موجودة بس في السويتشات اللي بتدعم الـ PoE.
  * الوظيفة: بتوضح حالة "توزيع الكهرباء" على المنافذ؛ يعني لما تختار الوضع ده، لمبة البورت هتنور لو البورت ده بيغذي الجهاز المتوصل بيه بالكهرباء (زي كاميرات المراقبة أو تليفونات الـ IP).

**3. The Mode Button (زرار الوضع)**

* الوظيفة: هو الزرار المسؤول عن التنقل بين الأوضاع اللي فوق دي (STAT -> DUPLX -> SPEED -> PoE). كل دوسة بتنقل اللمبة للي تحتها عشان تغير وظيفة مؤشرات البورتات

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Switch Management Access

**Switch Management Access (الوصول لإدارة السويتش)**

عشان تجهز السويتش للإدارة والتحكم عن بعد (Remote Management)، لازم تمر بالخطوات دي:

**1. إعدادات العنوان (IP Configuration):**

* لازم السويتش يأخد IP Address و Subnet Mask.
* الهدف: عشان تقدر توصله وتكلمه من خلال الشبكة.

**2. إعداد البوابة الافتراضية (Default Gateway):**

* الشرط: لو عايز تدير السويتش من "شبكة خارجية" (Remote Network) مختلفة عن شبكة السويتش.
* التشابه: الخطوة دي بتتعمل بالظبط زي ما بتعمل إعدادات الـ IP لأي كمبيوتر (PC) عادي.

**3. واجهة السويتش الافتراضية (SVI - Switch Virtual Interface):**

* المكان: الـ IP مابيتحطش على "بورت حقيقي" (Physical Port).
* الطريقة: بيتم وضع الـ IP على واجهة وهمية اسمها SVI&#x20;

**4. الإعداد الأولي (Initial Configuration):**

* بما إن السويتش لسه مفيهوش IP في البداية، بنستخدم كابل الكونسول (Console Cable) لتوصيل كمبيوتر بالسويتش مباشرة لعمل الإعدادات الأولية دي.

## &#x20;Configure Switch Ports

### Duplex Communication

**Duplex Communication Types (أنواع الاتصال المزدوج)**

1\. Full-Duplex Communication (الاتصال مزدوج الاتجاه)

* المفهوم: يسمح للطرفين بإرسال واستقبال البيانات في نفس الوقت (Simultaneously).
* الاسم الآخر: يُعرف أيضاً بـ Bidirectional Communication.
* المتطلبات: يتطلب وجود Microsegmentation (تقسيم دقيق للشبكة).
* الكفاءة (Efficiency):
  * يوفر كفاءة 100% في الاتجاهين (إرسال واستقبال).
  * يضاعف النطاق الترددي المحتمل (Doubles the potential bandwidth).
  * في هذا الوضع، يتم تعطيل دائرة اكتشاف التصادم (Collision detection circuit) في كارت الشبكة لأن التصادم لا يحدث.

3\. Half-Duplex Communication (الاتصال نصف المزدوج)

* المفهوم: هو اتصال أحادي الاتجاه (Unidirectional)؛ البيانات تمر في اتجاه واحد فقط في المرة الواحدة.
* المشاكل: يسبب مشاكل في الأداء لأن البيانات لا تتدفق بحرية، وغالباً ما ينتج عنه تصادمات (Collisions).

4\. High-Speed Requirements (متطلبات السرعات العالية)

* تقنيات مثل Gigabit Ethernet وكروت الشبكة سرعة 10Gb تتطلب اتصالات من نوع Full-Duplex لكي تعمل.

### Configure Switch Ports at the Physical Layer

* Manual Configuration: يمكن ضبط منافذ السويتش يدوياً بأوامر محددة للسرعة (`speed`) ونمط الازدواج (`duplex`).
* Operating Modes:
  * عند سرعة 10/100 Mbps: المنافذ تعمل في وضع Half أو Full duplex.
  * عند سرعة 1000 Mbps (1 Gbps): المنافذ تعمل فقط في وضع Full-duplex.
* Best Practice:
  * يفضل استخدام Autonegotiation (التفاوض التلقائي) مع الأجهزة غير المعروفة أو المتغيرة.
  * يفضل استخدام Manual Settings (الإعداد اليدوي) مع الأجهزة المعروفة والثابتة مثل السيرفرات وأجهزة الشبكة لضمان الاستقرار.
* Troubleshooting Note: عدم تطابق الإعدادات (Mismatched settings) بين الطرفين يسبب مشاكل في الاتصال، وغالباً ما يحدث بسبب فشل التفاوض التلقائي.
* Fiber-Optic Ports: منافذ الفايبر تعمل دائماً بسرعة واحدة محددة مسبقاً وتكون دائماً Full-duplex.

**Auto-MDIX**

* Definition: هي خاصية تجعل السويتش يكتشف نوع الكابل المتوصل (Straight-through أو Crossover) ويقوم بضبط الاتصال تلقائياً ليعمل بنجاح.
* Without Auto-MDIX (بدون الخاصية): يجب الالتزام بأنواع الكابلات:
  * Straight-through: لتوصيل أجهزة مختلفة (سويتش مع راوتر/سيرفر/PC).
  * Crossover: لتوصيل أجهزة متشابهة (سويتش مع سويتش أو Repeater).
* Enabling the Feature: في السويتشات الحديثة، يتم تفعيل الخاصية بالأمر: `mdix auto`.
* Pre-requisite (شرط أساسي): لكي تعمل خاصية Auto-MDIX، يجب أن تكون إعدادات السرعة (Speed) والازدواج (Duplex) مضبوطة على Auto.

Default Settings: الوضع الافتراضي في سويتشات Cisco Catalyst (2960/3560) هو auto لكل من السرعة والـ duplex.

### Network Access Layer Issue

&#x20;(Error Types)

* Input Errors: إجمالي عدد الأخطاء في البيانات المستلمة (تشمل Runts, Giants, CRC, إلخ).
* Output Errors: إجمالي الأخطاء التي منعت إرسال البيانات للخارج.
* Runts: فريمات تم تجاهلها لأن حجمها صغير جداً (أقل من الحد الأدنى).
* Giants: فريمات تم تجاهلها لأن حجمها كبير جداً (تجاوزت الحد الأقصى).
* CRC: خطأ في الحسابات؛ المجموع المحسوب (Checksum) لا يطابق المرسل (دليل على تلف البيانات).
* Collisions: عدد الرسائل التي أعيد إرسالها بسبب حدوث تصادم.
* Late Collisions: تصادم يحدث متأخراً (بعد إرسال 512 بت من الفريم).

**Configure Switch Ports - Interface Input and Output Errors**

1\. Runt Frames (الفريمات الناقصة):

* التعريف: هي إطارات Ethernet حجمها أقل من 64-byte (وهو الحد الأدنى المسموح به).
* السبب: السبب المعتاد هو كارت شبكة تالف (Malfunctioning NIC)، وقد تحدث أيضاً بسبب التصادمات.

2\. Giants (الفريمات العملاقة):

* التعريف: هي إطارات Ethernet حجمها أكبر من 1518 bytes (وهو الحد الأقصى المسموح به).

3\. CRC errors (أخطاء فحص التكرار الدوري):

* المعنى: تشير غالباً إلى مشكلة في "الكابل" أو الوسط الناقل (Media error).
* الأسباب الشائعة:
  * تداخل كهربائي (Electrical interference/Noise).
  * وصلات مفككة أو تالفة (Loose or damaged connections).
  * استخدام نوع كابل خاطئ.
* الحل: إذا رأيت أخطاء CRC كثيرة، يجب فحص الكابل والبحث عن مصادر الشوشرة (Noise) وإزالتها.

1\. Collisions (التصادمات):

* في حالة Half-duplex: وجود التصادمات أمر طبيعي.
* في حالة Full-duplex: يجب ألا ترى أي تصادمات نهائياً (وجودها يعني مشكلة).

2\. Late Collisions (التصادمات المتأخرة):

* التعريف: تصادم يحدث بعد إرسال 512 bits من الفريم.
* السبب الأشهر: طول الكابل زائد عن الحد المسموح به (Excessive cable lengths).

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

