# Threat Detection and Classification with EDR/XDR

## Fundamentals of Threat Analysis

### Definition of Threat

* أي نشاط/شخص/حدث ممكن يسبب ضرر للأصول الرقمية.
* يشمل: هجمات دول، مجرمين إلكترونيين، أو تهديدات داخلية (Insider Threat).
* الهدف: فهم طبيعة ومصدر وتأثير التهديد لبناء إستراتيجية أمن قوية.

### Threat Actors

* هم الجهات/الأشخاص اللي بيشكلوا تهديد مباشر.
* الأنواع: APTs (مدعومة من دول)، مجرمين إلكترونيين، هاكتفست، موظفين داخليين (Careless أو Malicious).
* كل Actor ليه دوافع، قدرات، وأدوات مختلفة.

### Threat Vectors

* الطرق اللي بيستغلها المهاجم للوصول للأنظمة.
* أمثلة: Email Attachments، ثغرات المتصفحات، USB Devices، Social Engineering.
* فهم الـ Vectors بيساعد في التوقع والاستعداد.

### Asset Evaluation

* تحديد وتصنيف وتقييم قيمة الأصول الرقمية.
* يشمل: سيرفرات، قواعد بيانات، تطبيقات، شبكة، ملكية فكرية.
* الهدف: معرفة الأصول الأكثر أهمية لتحديد الأولويات.

### Threat Probability

* احتمال حدوث تهديد ضد أصل/نظام محدد.
* بيتأثر بـ: الإجراءات الأمنية، قدرات المهاجمين، وأهمية الأصل.
* بيساعد في توزيع الموارد على أهم المخاطر.

### Impact Assessment

* تقييم حجم الضرر لو التهديد حصل.
* يشمل: فقدان بيانات، توقف العمليات، سمعة الشركة، التزامات قانونية.
* مهم لتحديد الأولويات وصياغة خطط الاستجابة.

### Threat–Vulnerability Relationship

* مش كل تهديد خطر إلا لو قابل ثغرة فعلية.
* مثال: Malware يستهدف نسخة معينة → خطر فقط لو النسخة دي موجودة.
* الربط بين التهديدات والثغرات أساسي في إدارة المخاطر.

### Threat Rate

* معدل تكرار التهديد خلال فترة زمنية.
* معدل عالي = خطر أكبر.
* بيتحدد من Threat Intelligence داخلي وخارجي.
* بيساعد في معرفة التهديدات القريبة والمتكررة.

### Preventive & Mitigation Strategies

* **Preventive**: منع التهديدات (Firewalls, Authentication, Monitoring).
* **Mitigation**: تقليل الأثر لو حصل هجوم (Incident Response, Recovery).
* لازم يشتغلوا مع بعض علشان نظام أمني قوي.

## Threat Detection and Classification with EDR/XDR

***

### EDR/XDR Threat Detection (this a generic methods)

#### 1. Machine Learning & AI

* يستخدم خوارزميات تتعلم من بيانات ضخمة.
* يكشف الهجمات بدقة أعلى حتى لو ماكانش ليها توقيع معروف.

#### 2. Behavioral Analysis

* بيراقب النشاط الطبيعي (baseline).
* أي انحراف (زي مستخدم بيعمل أفعال غير معتادة) = تهديد محتمل.

#### 3. Heuristic Analysis

* بدور على "خصائص وسلوكيات" مش شرط توقيع محدد.
* بيكشف برمجيات جديدة أو متغيرة.

#### 4. Signature-Based Detection

* يعتمد على التواقيع المعروفة للمالوير.
* فعال جدًا ضد التهديدات القديمة/المعروفة.

#### 5. Fileless Threat Detection

* بيراقب الهجمات اللي بتحصل في **الذاكرة** من غير ملفات (PowerShell, WMI, scripts).
* مهم عشان دي بتفلت من الـ AV.

#### 6. Execution in a Virtual Environment (Sandboxing)

* بيشغل الملفات المشبوهة في بيئة معزولة.
* يكشف نواياها قبل ما تشتغل على الجهاز الحقيقي.

#### 7. Network Traffic Analysis (مميز في XDR)

* بيراقب الاتصالات المشبوهة في الشبكة.
* يكشف C2 traffic أو lateral movement.

#### 8. Integrated Threat Intelligence

* بيربط مع قواعد بيانات تهديدات عالمية.
* بيخلي الكشف محدث ضد آخر الهجمات.

***

### EDR/XDR Threat Classification (تصنيف التهديدات)

#### 1. By Threat Type

* بيصنف الهجوم حسب نوعه: Malware, Ransomware, Exploit, Phishing, Lateral Movement.

#### 2. By Threat Source

* بيحدد المهاجم: APTs، Insider، Hacktivists، Cybercriminals.

#### 3. By Target

* بيركز على مين/إيه اللي بيتهاجم: SCADA، بنوك، قواعد بيانات، أنظمة حساسة.

#### 4. By Attack Purpose

* ليه الهجوم حصل؟ Data Theft، DoS، Espionage، Reputation Damage.

#### 5. By Complexity

* بيقيم مستوى التعقيد: Low، Medium، High.
* بيعتمد على خبرة وموارد المهاجم.

***

### Threat Detection & Classification with SentinelOne

انواع التهديدات اللي بيصنفها SentinelOne:

* **Malware**: أي برنامج خبيث.
* **Ransomware**: تشفير البيانات + طلب فدية.
* **Virus**: بيتكاثر وينتشر في البرامج.
* **Hacktool**: أدوات لاختراق الأنظمة.
* **Infostealer**: سرقة بيانات حساسة.
* **PUA**: برامج مزعجة لكن مش بالضرورة خبيثة.
* **Trojan**: ملف متخفي كبرنامج سليم لكن بيعمل Backdoor.
* **Packing**: إخفاء الكود الضار بالتشفير/الضغط.
* **Rootkit**: يخبي وجود المالوير ويوصل للـ Kernel.

***

### Detection Engines in SentinelOne&#x20;

1. **Reputation Engine**

* يقارن الملفات مع قاعدة بيانات ضخمة (Malware, URLs, IPs).
* سريع وفعال ضد التهديدات المعروفة (مثال: mimikatz.exe يتمنع فورًا).

2. **Static AI**

* يحلل الملف من غير ما يشغله.
* قوي ضد Zero-day وبيمنع التهديد قبل ما يشتغل.

3. **Static AI - Suspicious**

* يرصد الملفات "المريبة" اللي مش واضحة 100%.

4. **Behavioral AI - Executables**

* يركز على السلوك في التشغيل (تعديل ملفات نظام، Memory Injection).
* يوقف العمليات الضارة فيreal time .

5. **Documents, Scripts Engine**

* يحلل المستندات (Word, Excel) والـ Scripts (PowerShell, JS).
* يكشف أوامر خبيثة مدسوسة في ملفات عادية.

6. **Lateral Movement Engine**

* يكشف محاولات المهاجمين التحرك من جهاز لجهاز جوه الشبكة.

7. **Anti-Exploitation / Fileless Engine**

* يكشف الاستغلال (Exploits) والهجمات بدون ملفات (Memory-based).

8. **PUA Engine**

* يرصد البرامج المزعجة (Adware, Toolbars, Hijackers).



تمام ✅ خليني أعملك ملخص مرتب بأسلوب ينفع تحطه في GitBook، وكل عنوان أكتب تحته سطر صغير يوضح ده بتاع إيه قبل الشرح التفصيلي.

***

## Threat Management and Analysis

📌 **ده الجزء اللي بيشرح ليه EDR/XDR مهمين في الإدارة والتحليل بتوع التهديدات، وإزاي بيخلوا الاستجابة استباقية مش رد فعل متأخر.**

EDR/XDR بيدوا فرق الأمن القدرة إنها تتابع الأنشطة على الـ endpoints والشبكة لحظيًا، وتكشف أي سلوك غريب، وتاخد إجراءات تلقائية أو شبه تلقائية. وده بيخلي المؤسسات تسبق الهجوم بدل ما تفضل بس ترد عليه.

***

### Threat Management and Analysis Steps

📌 **ده الجزء اللي بيوضح الـ Lifecycle اللي بيمر بيه أي تهديد من أول ما يتشاف لحد ما نتعلم منه.**

#### 1. Detection (الكشف)

متابعة مستمرة لكل أنشطة الـ endpoint (ملفات، system calls، network traffic). الهدف هنا كشف أي تهديد معروف أو غير معروف.

#### 2. Investigation (التحقيق)

بعد الكشف، بيبدأ المحللين يفحصوا بعمق علشان يفهموا نوع التهديد، مصدره، وتأثيره المحتمل.

#### 3. Response (الاستجابة)

لو التهديد اتأكد، بيتعمل خطة رد فورًا: إزالة البرمجيات الضارة، عزل الأجهزة، أو حتى رد شامل أكبر.

#### 4. Remediation (المعالجة)

إصلاح أي ضرر حصل: استرجاع البيانات، إعادة الأنظمة لحالتها، وإضافة دفاعات جديدة.

#### 5. Learning (التعلم)

تحليل معمق لفهم إزاي حصل الاختراق أو الهجوم. الهدف هنا سد الثغرات والاستعداد لهجمات مشابهة.

#### 6. Threat Hunting (الصيد الاستباقي)

بعض الـ EDR بيدعم البحث الاستباقي. المحللين يدوروا على تهديدات كامنة لسه ما اتكشفتش.

***

### Threat Management and Analysis with SentinelOne

📌 **ده الجزء اللي بيشرح إزاي SentinelOne بيطبق المراحل دي عمليًا جوه المنصة.**

في SentinelOne، التهديدات بتظهر تحت قائمتين:

* **Threats:** تهديدات اتكشفت بالمحركات الداخلية (engines).
* **Alerts:** تنبيهات ناتجة عن قواعد مخصصة (Star Custom Rules).

***

### Threat Details

📌 **ده الجزء اللي بيشرح إيه التفاصيل اللي تقدر تشوفها لكل تهديد.**

لما تفتح التهديد من واجهة SentinelOne، بتظهر معلومات زي:

* **Endpoint Name** → اسم الجهاز المصاب.
* **File Path** → مكان الملف الخبيث.
* **Command Line Arguments** → أوامر التشغيل اللي استُخدمت.
* **Signer Identity** → هوية الجهة الموقعة للملف.
* **Classification** → نوع التهديد (Ransomware, Trojan…).
* **Originating Process** → العملية اللي بدأت التهديد.
* **Initiated By** الموضوع بدا منين
* **Engines** → أي محرك كشف التهديد.
* **Detection Type** → أسلوب الكشف (Behavioral, Signature…).
* **Analyst Verdict:** It is the decision or interpretation made by the cybersecurity analyst or an automated system about the threat.
* **Incident Status** → (i.e. quarantined, resolved, pending, etc.)
* **Indicators** → الـ IoCs المرتبطة.
* **Notes**&#x20;

***

