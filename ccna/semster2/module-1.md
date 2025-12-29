# module 1

1.1 Configure a Switch with\
Initial Settings
----------------

### Switch Boot Sequence

**step1**:اول حاجه ال POST(Power On Self-Test)بيشتغل&#x20;

**Step 2: Loading the Boot Loader (تحميل برنامج الإقلاع)**

* الوقت (Timing): بتحصل فوراً بعد ما الجهاز يخلص فحص الهاردوير (After POST).
* المكان (Location): السويتش بيحمل برنامج الـ Boot Loader من الذاكرة الدائمة (ROM).
* الوظيفة (Function): هو برنامج صغير جداً ومهمته الأساسية التجهيز لتحميل نظام التشغيل.

**Step 3: Low-level CPU Initialization (تهيئة المعالج)**

* الدور (Action): الـ Boot Loader بيقوم بتهيئة المعالج (CPU) عشان يقدر يشتغل.
* العمليات (Operations): بيضبط "سجلات المعالج" (CPU Registers) المسؤولة عن حاجات حيوية زي:
  1. Memory Mapping: تحديد فين الذاكرة الفعلية (RAM) ومكانها فين في الخريطة.
  2. Quantity of Memory: التعرف على حجم الذاكرة المتاحة.
  3. Speed: تحديد السرعة اللي الذاكرة هتشتغل بيها.

**Step 4: The boot loader initializes the flash file system on the system board.**

**Step 5: Finally, the boot loader locates and loads a default IOS operating system**\
**software image into memory and gives control of the switch over to the IOS**

<div align="center"><figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure></div>

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

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

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
* الطريقة: بيتم وضع الـ IP على واجهة وهمية اسمها SVI (وغالباً بتكون VLAN interface).

**4. الإعداد الأولي (Initial Configuration):**

* بما إن السويتش لسه مفيهوش IP في البداية، بنستخدم كابل الكونسول (Console Cable) لتوصيل كمبيوتر بالسويتش مباشرة لعمل الإعدادات الأولية دي.

## 1.2 Configure Switch Ports

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



