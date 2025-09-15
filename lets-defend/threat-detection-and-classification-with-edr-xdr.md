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
* **Indicators**&#x20;
* **Notes**&#x20;

***

### 📌 Data Collection and Analysis with EDR

* **EDR (Endpoint Detection and Response)** بيجمع بيانات تفصيلية جدًا من الأجهزة (endpoints) زي: كمبيوترات، سيرفرات، موبايلات.
* البيانات دي اسمها **Telemetry Data** وهي سجلات دقيقة ومستمرة بتوضح إيه اللي بيحصل على الجهاز لحظة بلحظة.
* الهدف: تساعد في **كشف، فهم، والرد على أي نشاط ضار**.
* البيانات دي كمان ممكن تتعمل لها تحليل معقد (Analytics) باستخدام:
  * **Heuristic checks** → فحوصات تعتمد على الأنماط والقواعد.
  * **Behavioral analysis** → تحليل سلوك البرامج أو المستخدمين.
  * **Machine Learning** → خوارزميات تتعلم تفرق بين الطبيعي والمشبوه.

**الخلاصة:** التليمتري بتاع EDR زي "الكاميرا المراقبة" اللي شغالة 24/7 على كل الأجهزة، علشان أي هجوم يتشاف بدري ويترد عليه بسرعة.

***

### 📌 Categories of Telemetry Data (أنواع البيانات اللي EDR بيجمعها)

<div align="left"><figure><img src="../.gitbook/assets/image.png" alt="" width="500"><figcaption></figcaption></figure></div>

💡 ملاحظة: مش كل EDR بيجمع نفس التفاصيل → ده بيعتمد على النسخة والإعدادات.

***

### 📌 (Telemetry data Use Cases)

#### 🔎 Threat Hunting

* المحللين يقدروا يدوروا يدويًا على أي نشاط غريب.
* مثال: اتصالات غير معتادة أو برامج مش متوقعة.

#### 🚨 Incident Response

* عند وقوع هجوم → البيانات بتوضح:
  * المهاجم دخل إزاي.
  * أي ملفات أو أنظمة اتأثرت.
  * المهاجم عمل إيه جوه الشبكة.

#### 🕵️ Forensics

* بعد الحادثة → التليمتري يساعد تعرف:
  * إيه اللي حصل بالظبط.
  * ليه حصل.
  * إزاي تمنع إنه يتكرر.

#### 📊 Risk and Compliance Assessment

* تستخدم البيانات لتقييم:
  * هل الأجهزة محدثة؟
  * هل فيه يوزرز عندهم صلاحيات زيادة؟
* ده مفيد عشان الالتزام بالـ **Security Standards**.

#### 🧠 Behavioral Analysis

* التليمتري يوضح الأنشطة العادية مقابل الغريبة.
* ممكن تدريب AI أو ML علشان يكشفوا التهديدات المستقبلية.

#### 🌐 Network Monitoring and Analysis

* تحليل الترافيك والاتصالات.
* يساعد في اكتشاف:
  * DDoS attacks.
  * Unauthorized access.
  * Data theft (سرقة بيانات).
  * تهديدات الشبكة بشكل عام.

***

## 📌 Creating Custom EDR Rules and Policies

واحدة من أقوى مميزات الـ **EDR systems** (خاصة في بيئات IT كبيرة ومعقدة) هي إنك تقدر تعمل **قواعد (Rules) مخصصة**.

* الفكرة: مش كل المؤسسات زي بعض → فالقواعد الجاهزة (Standard Rules) معمولة تهاندل التهديدات العامة، لكن مش دايمًا مناسبة لكل بيئة.
* هنا ييجي دور **Custom Rules** → تقدر تبني قواعد تناسب بيئتك واحتياجاتك بالظبط.

***

## 📌 Details on Custom EDR Rule Development

### Why is it necessary to develop a special rule?

* كل منظمة عندها تطبيقات خاصة، Workflows، وخصائص بيئة IT مختلفة.
* القواعد الجاهزة بتغطي تهديدات عامة، لكن مش دايمًا مناسبة 100%.
* Custom Rules بتسد الفجوة دي.

أسباب إضافية:

1. **التهديدات بتتغير باستمرار** → مهاجمين جدد، طرق جديدة.
   * الـ Custom Rules تخليك ترد بشكل محدد على تهديدات معينة أو حتى تهديدات مرتبطة بمكان جغرافي معين.
2. **تقدر تحدد مخاطر خاصة بمؤسستك** → وده يوفر حماية استباقية.
3. مش بس تهديدات خارجية، كمان **Internal Threats** (تهديدات داخلية أو Insider Threats).
   * Custom Rules تساعد تكتشف وتحيدها.
4. تقلل **False Positives** لأنك بتصمم القاعدة تناسب بنيتك التحتية بالظبط.

***

### How Should the Rule Development Process Be?

1. **Needs Analysis**
   * تحدد الأول إيه اللي محتاجه القاعدة.
   * أمثلة: مراقبة برنامج معين، التحكم في ترافيك من IP Range معين، مراجعة سلوك ملف أو Process.
2. **Rule Design**
   * بعد ما تحدد الاحتياج → تصمم القاعدة: إيه اللي هيتراقب؟ وإمتى تتفعل؟
3. **Testing and Implementation**
   * لازم تختبر القاعدة في بيئة تجريبية قبل ما تطبقها.
   * الهدف: تتأكد إنها شغالة صح وما بتديش False Positives أو False Negatives.
4. **Monitoring and Improvement**
   * القواعد لازم تتطور وتتظبط مع الوقت حسب التهديدات الجديدة.

***

### Important point that need extra attention

* **False Positives**: لو القاعدة صارمة جدًا أو بتغطي مجال واسع → ممكن تدي إنذارات غلط على سلوك طبيعي.
* **Performance Issues**: لو عندك قواعد كتير أو واسعة جدًا → ممكن تبطّأ السيستم أو تأثر على شغل المستخدمين.
* **Update and Maintenance**: القواعد محتاجة مراجعة وتحديث باستمرار مع تغير التهديدات وبيئة الـ IT.
