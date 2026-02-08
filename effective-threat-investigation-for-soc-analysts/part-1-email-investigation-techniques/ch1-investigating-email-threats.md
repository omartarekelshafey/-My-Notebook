# CH1 Investigating Email Threats

## Top infection vectors

#### **Initial Access**

بعد ما المهاجم بيخلص مرحلة الاستطلاع (Reconnaissance) وتجهيز الأدوات (Weaponization)، بيبدأ يدور على أنسب طريقة يدخل بيها لبيئة الضحية. المرحلة دي بنسميها initial access، ودي أهم النقط اللي بتشرحها:

***

#### **Common Techniques**

المهاجمين عندهم طرق كتير عشان يثبتوا رجلهم جوه الشبكة، ومن أهمها:

* تقنية Phishing Emails: وهي إرسال رسائل بريد إلكتروني احتيالية بتستهدف المستخدمين.
* استغلال Public-facing Applications: عن طريق تتبع الثغرات في البرامج المتاحة بشكل مباشر على الإنترنت.
* أسلوب Drive-by Compromise: استدراج الضحية لزيارة موقع إلكتروني تم اختراقه مسبقاً.
* سرقة Valid Credentials: الحصول على بيانات دخول حقيقية زي حسابات الـ VPN أو الـ RDP.

Why do attackers prefer phishing emails to gain initial\
access?
-------

في أسباب كتير بتخلي الـ Phishing هو الخيار المفضل للـ Attackers للوصول للـ Initial Access، ومنها:

**1. Easy Reconnaissance**

خلال مرحلة الـ Reconnaissance Phase، بيقدر المهاجم يجمع الـ Email addresses بسهولة من مصادر كتير زي:

* منصات Social media: وبالأخص موقع LinkedIn.
* إعلانات Job postings: اللي بتنشر إيميلات التواصل.
* قواعد Data leaks: المتاحة على الـ Dark Web.
* أرشيف Wayback Machine: زي موقع Archive.org.
* منصات Marketing platforms: زي موقع ZoomInfo.com.

**2. Simple Weaponization**

تجهيز الـ Weaponized attachment مش عملية صعبة، والمهاجمين بيستخدموا طرق زي:

* رفع Malware: على Cloud platforms شرعية وتبادل الـ Download link.
* استخدام VBA macros: لدمج أكواد خبيثة جوه الـ Documents.
* إرسال Malware executable: في شكل ملف Compressed format.

**3. Human Vulnerability**

بيعتمد الـ Attacker بشكل أساسي على نقص الـ Security awareness عند الـ Users، لإن أغلبهم مش مدرب كفاية إنه يتعامل مع الattacks  .

## Email threat types

استخدام خدمات البريد الإلكتروني بيعرض المؤسسة لتهديدات متنوعة مش بس الـ Phishing. المهاجمين بيستخدموا الـ Email لأغراض تانية زي الـ Blackmailing، والـ Information leakage، والـ Lateral movement.

***

#### **Spearphishing Attachments**

تعتبر الـ Spearphishing Attachments وسيلة لاستهداف أشخاص محددين بملفات ملغمة للحصول على الـ Initial Access أو الـ Credentials.

**Common Attachment Types**

بيختار المهاجم نوع الملف بناءً على بيئة الضحية، وأشهر الأنواع هي:

* ال Microsoft Office documents: زي الـ Word والـ Excel، وبتعتمد على الـ VBA macros.
* ال PDF files: بتستغل ثغرات الـ PDF reader أو بتنفذ كود JavaScript.
* ال Compressed files: زي الـ .zip أو .rar لإخفاء الـ Malware.
* ال ISO images: بتستخدم لتخطي الـ File filters وبرامج الـ Antivirus.
* ال HTML files: بتستخدم لمحاكاة صفحات الـ Login لسرقة الحسابات.

***

#### **Spearphishing Link**

بتعتمد الـ Spearphishing Link على إرسال رابط خبيث بدلاً من ملف، وليها غرضين أساسيين:

* عملية Credential harvesting: توجيه الضحية لموقع مزيف لسرقة بيانات الدخول&#x20;
* تحميل Malware: استضافة الملفات الخبيثة على  OneDrive أو Dropbox ومحاوله ان victim  ينزل ال malware عنده ويشغله

***

* #### **Blackmail Email**

بيُعرف الـ Blackmail email أحياناً بـ Sextortion، وفيه بيدعي المهاجم إنه اخترق جهاز الضحية وسرب بيانات حساسة، وبيطلب فدية بالـ Bitcoin.

**Proof of Infection Methods**

الattack  بيستخدم طرق عشان يقنع الvictim  إن الاختراق حقيقي:

* ائل Screenshots: عرض صور لبيانات  الvictim تم الحصول عليها من الـ Infostealer أو شرائها من الـ Dark web.
* تقنية Email spoofing: تزوير عنوان المرسل ليظهر وكأن الضحية بعت الإيميل لنفسه، وده بيوحي إن الحساب مخترق فعلياً.

***

#### **Business Email Compromise (BEC)**

تعتبر الـ Business Email Compromise أو اختصاراً BEC واحدة من أخطر أنواع الـ Email scams اللي بتستهدف المؤسسات، لأنها مش بتعتمد على ملفات خبيثة قد ما بتعتمد على الـ Deception والتلاعب النفسي.

**Definition and Impact**

هجوم الـ BEC بيستهدف بشكل محدد الـ Individuals اللي ليهم صلاحيات مالية، زي الـ Executives أو الـ Finance employees، بهدف دفعهم لتنفيذ Fraudulent financial transactions. الهجوم ده بيسبب خسائر مالية ضخمة جداً للشركات (Significant financial losses).

***

**Core Techniques in BEC**

عشان المهاجم ينجح في عملية الـ Business Email Compromise، لازم يكسر حاجز الشك عند الضحية. بيعتمد في ده على طريقتين أساسيتين هما الأخطر في المرحلة دي:

***

**1. Email Thread Hijacking**

تعتبر الـ Email Thread Hijacking تقنية "اختطاف" للمحادثات القائمة، وبتتم كالتالي:

* عملية الـ Access: المهاجم بيخترق فعلياً حساب إيميل طرف من الطرفين (زي موظف في شركة أو مورد خارجي).
* مرحلة الـ Silent Monitoring: بيفضل المهاجم يراقب الـ Inbox بهدوء عشان يفهم الـ Context بتاع الشغل والمحادثات اللي فيها فلوس.
* خطوة الـ Interception: لما تيجي فرصة مناسبة (مثلاً وقت دفع فاتورة)، المهاجم بيبعت رد من جوه الـ Thread الحقيقية ويطلب تغيير بيانات الـ Bank Account. الضحية هنا مش بيشك أبداً لأن الكلام جاي كـ Reply في محادثة قديمة هو كان طرف فيها.

***

**2. Email Spoofing**

بتعتمد الـ Email Spoofing على التزوير الظاهري للبيانات دون الحاجة لاختراق الحساب نفسه، وده بيتم عن طريق:

* تزوير الـ Display Name: المهاجم بيخلي اسم المرسل يظهر للضحية كأنه الـ CEO أو Trusted partner.
* تلاعب بالـ Email Header: بيتم تعديل الـ From field عشان يبان قدام الضحية إنه إيميل سليم، لكن في الحقيقة الإيميل مبعوث من Mail server مختلف تماماً تحت سيطرة المهاجم.
* استخدام Look-alike Domains: المهاجم بيسجل Domain قريب جداً من الحقيقي (مثلاً تغيير حرف واحد زي `g0ogle.com` بدل `google.com`) عشان يخدع عين الضحية اللي مش مركزة.

## Attacker techniques to evade email security detection

#### Using newly created domains to send a malicious email

تعتمد الـ Modern email security solutions بشكل كبير على Threat Intelligence feeds. الfeeds دي فيها قايمة بالـ Domains اللي عندها (Bad Reputation) لأنها استخدمت قبل كده في attacks  قبل كده .

* الفكرة هنا: عشان الattackerيهرب من موضوع ده، بيجيب  New Domains لسه معمولة جديد ومستخدمتش قبل كده.
* النتيجة: لما الـ Security Solution بيcheck  على الـ Domain ده، مبيلاقيش عليه أي تاريخ سيء، فبيسمح بمرور الإيميل.

***

#### Using non-blacklisted SMTP servers

احنا بنعمل check  علي ip  اللي مربوط بال smtp server  اللي بعت email&#x20;

* &#x20;الattackers بيتجنبوا استخدام سيرفرات معروفة  لأن الـ IPs بتاعتها بتكون موجودة في الـ Blacklists.
* البديل: بيحرص المهاجم على استخدام SMTP Server IPs جديده ومش  موجوده في black list، عشان يضمن إن الإيميل ميتعملوش Block بسبب Bad Reputation

***

#### Sandbox analysis evasion

دلوقتي هنكلم عن ال techniques  اللي بيعملها attackers علشان يعدي من sand box&#x20;

**Malware sleep**

بيقوم الattacker ببرمجة الـ Malware إنه ميشتغلش علي طول اول ما يتعمله execute لحد فترة معينة (مثلاً 3 دقايق) .

* السبب: الـ Sandbox ليه وقت محدد للفحص، لو الـ Malware فضل خامل طول الوقت ده، الـ Sandbox هيفتكر إنه ملف سليم ويسمح بمروره. بعد ما الوقت يخلص ويكون وصل لجهاز الضحية، يبدأ النشاط الخبيث.

**Encrypted file**

بيستخدم المهاجم حيلة إرسال Malware file مضغوط (Compressed) أو ملف Document بس مشفر بـ Password.

* الخدعة: المهاجم بيكتب الباسورد في نص الإيميل نفسه عشان الضحية يشوفه.
* المشكلة التقنية: الـ Sandbox عملية أوتوماتيكية (Non-interactive)، يعني مبيقدرش يقرا الإيميل وياخد الباسورد ويفك تشفير الملف.
* النتيجة: الـ Sandbox بيفشل في تحليل المحتوى المشفر، فبيضطر يعدي الملف للضحية عشان ميعطلش الشغل، وهنا بتتم الإصابة.

**Sandbox discovery**

بعد تشغيل الـ Malware، بيبدأ الكود الخبيث يفحص البيئة اللي هو شغال فيها. بيدور على علامات تقول إنه جوه Virtual Machine أو Sandbox.

* &#x20;لو الـ Malware اكتشف إنه متراقب داخل Sandbox، بيوقف نفسه فوراً، أو بيغير سلوكه لسلوك بريء، أو يدخل في Sleep mode&#x20;

**Responding to specific requests**

هنا ال attacker  بيرمج السيرفر إنه يرد فقط على ال requestsاللي جاية من IP addresses تابعة لمؤسسة الضحية&#x20;

لو ip  تاني بعتله مش هيرد&#x20;

***

#### Trusted Domains Hosting Phishing Pages

تعتبر هذه التقنية واحدة من أذكى حيل الـ Evasion التي ظهرت بقوة في عام 2019، حيث تخلى المهاجمون عن استخدام Domains خاصة بهم ولجأوا لاستغلال البنية التحتية لشركات عملاقة.

***

#### The Core Concept

بدلاً من أن يقوم المهاجم بحجز Domain جديد (والذي قد يكون له Bad Reputation أو New Domain يثير الشك)، يقوم الattackerبإنشاء حساب مجاني على Cloud Platforms عالمية وموثوقة مثل:

* &#x20;appspot.com: الخاصة بخدمة Google App Engine.
* &#x20;web.app: الخاصة بخدمة Google Firebase.

بما أن هذه المنصات تسمح للمطورين برفع تطبيقاتهم ومواقعهم، يقوم المهاجم برفع صفحة Phishing (مثلاً صفحة تسجيل دخول مزيفة لـ Microsoft Outlook) على هذه الاستضافة.

## The anatomy of secure email gateway logs



تعتبر حلول الـ Email Gateway Security خط الدفاع الأول لأنها بتفحص وتحلل كل بريد إلكتروني صادر أو وارد، بما في ذلك المحتوى. وجودها في مسار البيانات بناءً على النص المقدم، ده تلخيص شامل لمكونات وتشريح سجلات الـ Secure Email Gateway، وهي أداة أساسية لأي SOC Analyst، بالتنسيق المتفق عليه:

### Secure Email Gateway Logs

تعتبر حلول الـ Email Gateway Security خط الدفاع الأول لأنها بتفحص وتحلل كل بريد إلكتروني صادر أو وارد، بما في ذلك المحتوى. وجودها في مسار البيانات (Inline position) بيديها  (Visibility)، مما يجعل السجلات الخاصة بيها كنزاً أثناء عمليات الكشف عن التهديدات والتحقيقات.

***

#### Log Types

توفر هذه الأنظمة عدة أنواع من السجلات لمراقبة نشاط البريد الإلكتروني:

* ال SMTP logs: تحتوي على معلومات التسليم عبر بروتوكول SMTP، زي الـ Sender IP، وعنوان المستلم، والـ Timestamps.
* ال Message tracking logs: تقدم تفاصيل دقيقة عن الرسائل اللي عدت، شاملة الـ Metadata زي الـ Message ID، والـ Subject، والتاريخ.
* ال Content filtering logs: تسجل القواعد اللي اتطبقت على محتوى الرسالة، وهل المحتوى ده اتعمله Blocked ولا Allowed.
* ال Spam and malware logs: ترصد الإيميلات اللي اتعملها Flag كرسائل مزعجة (Spam) أو بتحتوي على برمجيات خبيثة (Malware).
* ال Quarantine logs: تخص الرسائل اللي تم عزلها في الـ Quarantine، مع ذكر سبب العزل وتفاصيل الرسالة.

***

#### Common Log Fields

بغض النظر عن اسم المنتج أو الـ Vendor، دي أهم الfields اللي هتلاقيها في السجلات ولازم تحللها:

* ال SMTP server IP: هو الـ IP اللي استخدمه الsender، وبنستخدمه عشان نكشف لو الـ Server ده موجود في الـ Blacklists
* ال Sender email address: العنوان اللي اتبعت منه الرسالة، ومهم جداً نتأكد إنه مش جاي من Blacklisted domain أو منتحل لخداع الضحية.
* ال Recipient email address: عنوان الشخص اللي استلم الرسالة، وده بيساعدنا نحدد نطاق الإصابة (Scope) ونعرف مين المستخدمين أو الأجهزة المتأثرة في حالات الـ Phishing.
* ال Email subject: الوصف اللي كتبه الراسل لمحتوى الرسالة. المهاجمين غالباً بيستخدموا عبارات تحفيزية زي "Urgent Action Required" أو "Unauthorized Access Attempt"، أو مواضيع غير منطقية لوظيفة الموظف (زي محاسب بيجيله إيميل عن كورسات IT).
* ال Attached filename: اسم الملف المرفق، ولازم نربط بين أنواع ملفات الـ Phishing والأسماء الجذابة اللي بتشجع الضحية يفتحها
* ال Attached file hash: قيمة الهاش الخاصة بالملف المرفق، ودي بنستخدمها للبحث في قواعد بيانات الـ Threat Intelligence زي VirusTotal للتأكد من سلامة الملف.
* ال Malware category: بيظهر ده بس لو قاعدة بيانات الـ Signatures طابقت الملف، وبيقولنا اسم عائلة الفيروس زي ZLoader أو RedLine Infostealer.
* ال Attached URL: بيسجل الروابط الموجودة داخل نص الرسالة، بعض الأجهزة بتسجل كل الروابط والبعض بيسجل بس اللي بيطابق قاعدة بيانات الـ Malicious URLs.
* ال  Device action: الإجراء اللي الجهاز أخذه (سواء عدى الإيميل أو وقفه)، وده بيعرف المحلل الأمني هل التهديد وصل للمستخدم ولا لأ.
* ال  Block reason: بيوضح ليه الإيميل اتعمله Block من قبل الـ Gateway.

## Investigating suspicious emails

تعتبر عملية التحقيق في الإيميلات المشبوهة هي عملية فحص شاملة لكل الأدلة الرقمية، بداية من سجلات الـ Appliances ومحتوى الإيميل، وصولاً لتحليل سلوك الراسل والمرفقات. وعشان نأكد إذا كان الإيميل Malicious أو Benign، لازم نمشي ورا الخطوات دي بالتفصيل:

***

#### Domain & SMTP Reputation

أول خطوة هي فحص سمعة الـ Domain والـ SMTP Server اللي مبعوت منهم الإيميل:

* محركات Search Engine: بنعمل بحث عن الدومين، وممكن نلاقي تقارير (Threat reports) بتأكد إنه دومين خبيث، أو نكتشف إنه دومين لسه معمول جديد (Newly created) وده بيزود الشكوك.
* أداة MxToolbox: بنستخدمها للكشف عما إذا كان الـ Domain أو الـ SMTP IP موجود في القوائم السوداء (Blacklists) المعروفة&#x20;

***

#### Spoofing Validation

حتى لو الدومين يبان إنه تبع شركة حقيقية (زي `fedex.com`)، لازم نتأكد إن المهاجم مش عامل Spoofing:

* تحليل SMTP IP: بنطلع الـ IP الحقيقي اللي بعت الإيميل من الـ Logs.
* فحص MX Records: بنستخدم MxToolbox عشان نشوف السيرفرات المصرح ليها بالإرسال باسم الدومين ده، ونقارنها بالـ IP اللي معانا.
* تحليل WHOIS: لو الـ IP مش موجود في الـ MX Records، بنعمل WHOIS lookup عشان نتأكد من ملكيته، وغالباً بنكتشف إنه Unauthorized.

***

#### Email Sender Behavior

لو الفحوصات التقنية سليمة، بنبدأ نحلل سلوك الراسل (Sender Behavior) عشان نكشف الخداع:

* تاريخ Communication History: هل استقبلنا إيميلات من الشخص ده قبل كده؟ لو أيوة، ده مؤشر إيجابي.
* نمط Subject Pattern: هل نفس الراسل بيبعت إيميلات بنفس صيغة العنوان لأقسام مختلفة في الشركة؟ دي علامة Phishing.
* علاقة Job Relevance: هل منطقي إن محاسب يجيله إيميل عن "IT Stuff"؟ عدم التوافق بين المحتوى ووظيفة المستلم مؤشر خطر.

***

#### Subject & Filename Indicators

بيعتمد المهاجمين على كلمات مفتاحية معينة لإثارة اهتمام الضحية أو إشعاره بالخطر:

* حقل Subject: استخدام كلمات زي RE: و FW: للإيحاء إنها محادثة سابقة، أو Urgent Action Required.
* اسم Filename: استخدام أسماء جذابة للمرفقات زي Invoice, Payment, Contract.

***

#### Advanced Content Analysis

عشان نحسم الأمر تماماً، بنلجأ لأدوات تحليل متقدمة لفحص الروابط والملفات:

**1. URL Analysis (URL Scan)**

بنستخدم منصة URL Scan لفحص الروابط المشبوهة:

* طريقة Submission: بنحط الرابط وبنختار الفحص سواء Public أو Private.
* النتيجة Results: الأداة بتوضح لو الرابط ده Malicious، وايه العلامات التجارية المستهدفة (Targeted Brands) زي SharePoint أو Microsoft لسرقة الاعتمادات.

**2. File Analysis (ANY.RUN)**

بنستخدم بيئة ANY.RUN Sandbox عشان نشغل الملفات ونشوف سلوكها بشكل تفاعلي (Interactive):

* فك تشفير Encrypted Files: لو الملف محمي بباسورد (مكتوب في الإيميل)، بنقدر ندخله ونتفاعل مع الملف.
* مراقبة Processes: بنشوف تسلسل العمليات، زي إن ملف Excel يشغل cmd.exe وبعدين powershell.exe.
* تحليل Network Traffic: بنتابع الـ HTTP/DNS Requests عشان نشوف الاتصالات بالسيرفرات الخبيثة.
* فك أكواد Scripts: لو لقينا أوامر PowerShell مشفرة (Base64)، بنقدر نستخدم أدوات زي CyberChef لفك التشفير وفهم الغرض الخبيث.
