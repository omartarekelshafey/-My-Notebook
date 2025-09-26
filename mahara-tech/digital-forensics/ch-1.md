# CH 1

<table><thead><tr><th width="249.9998779296875">Section</th><th>Explanation</th></tr></thead><tbody><tr><td><strong>What is Forensic Science</strong></td><td>علم بيستخدم الطرق العلمية لتحليل الأدلة (زي DNA، بصمات، أسلحة) عشان يكشف الحقايق ويربط الجريمة بالفاعل.</td></tr><tr><td><strong>Why Digital Forensics</strong></td><td><p></p><p>المجرمين بقوا يستخدموا التكنولوجيا في الجرائم (اختراق، ابتزاز، سرقة </p><p>بيانات...)</p><p>فا علشان كده ال trace evidence اتغير يعني في اول كنت بدور علي شعر بصمة رجل الحاجات في digital forensics بتشوف ال meta data او logs وغيره من Artifact مش شرط يكون الحاجات ديه علي جهاز كومبيوتر بس علي اي جهاز عامتا</p></td></tr><tr><td><strong>Power of Digital Forensics</strong></td><td><p>Digital forensics can support in revealing crimes and tracking traces such as:• <strong>Fraud (الاحتيال):</strong> كشف عمليات نصب مالي وتحويلات غير مشروعة.</p><p></p><p>• <strong>Child Exploitation (استغلال الأطفال):</strong> تتبع الشبكات اللي بتستغل الأطفال على الإنترنت.</p><p></p><p>• <strong>Terrorism (الإرهاب):</strong> تحليل اتصالات ورسائل المجموعات الإرهابية.</p><p></p><p>• <strong>Drug Trafficking (تهريب المخدرات):</strong> تتبع الصفقات والاتصالات المشبوهة عبر الإنترنت.</p><p></p><p>• <strong>Homicide (جرائم القتل):</strong> استخراج داتا من موبايلات أو أجهزة المجرمين أو الضحايا لتوضيح ملابسات الجريمة.</p></td></tr></tbody></table>

Digital Forensics & Incident Response (DFIR)

## Digital Forensics And Incident Response

* **Similarity:**\
  الاتنين بيشتغلوا على **تحليل الـ Artifacts** وجمع الأدلة الخاصة بالجرائم السيبرانية.
* **اختلاف Incident Response:**
  * بيركز على **التحليل السريع** علشان يحدد السبب الجذري (Root Cause).
  * الهدف الأساسي: **الاحتواء (Containment) + الاستئصال (Eradication) + الاسترجاع (Recovery)**.
  * الوقت عامل أساسي، فالموضوع بيتعمل بسرعة عشان نرجّع السيستم يشتغل.
* **اختلاف Digital Forensics:**
  * بيركز على **تحليل كامل وشامل** للـ Artifacts.
  * العملية بتاخد وقت أطول لأنها لازم تكون دقيقة وقابلة للاستخدام في المحكمة.
  * أهم خطوتين: **Acquisition (جمع البيانات بطريقة سليمة)** و **Preservation (الحفاظ عليها من التلاعب)**.
  * لو المنظمة هتروح محكمة، لازم الأدلة تكون محفوظة بشكل يثبت إنها ما اتغيرتش.

## Digital Forensics And malware analysis

* **Similarity:**
  * الاتنين بيشتركوا في **استخراج الـ Artifacts**.
  * الاتنين بيطلعوا **Indicators of Compromise (IOC)** زي IPs، Domains، Hashes.
* **الاختلاف:**
  * Malware Analysis بيركز أكتر على **سلوك وبرمجة البرمجيات الخبيثة** نفسها.
  * Digital Forensics بيركز على **استخدام الأدلة الرقمية في سياق الجريمة**.

## Digital Forensics And Threat Hunting

* **Similarity with Digital Forensics:**
  * الاتنين بيعملوا **تحليل للـ Artifacts** وبيشتغلوا على تتبع الأدلة.
  * بيستخدموا نفس الأسلوب في **الفرضيات + التحليل**.
* **الفرق:**
  * في Threat Hunting مش بيهتموا بموضوع **Preservation** (الحفاظ على الأدلة).
  * أما في Digital Forensics لازم يكون في **حفظ للأدلة** عشان نقدر نثبت إنها **أصلية وغير متلاعب فيها**.
*   **العلاقة:**

    * الاتنين بيكملوا بعض وقت الـ **Compromise Assessment** (تقييم الاختراق).
    * Threat Hunting يلاقي الأثر بسرعة → Digital Forensics يحافظ ويحلل بشكل قانوني.



## Investigations Triad&#x20;

ديه تلات حاجات بتتنفذ مع بعض لما بيحصل  incident هنشوفهم واحده واحده دلوقتي

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### 🔹 الفكرة الأساسية

الـ **Investigations Triad** هو نموذج يعتمد على ثلاث وظائف أساسية تعمل مع بعض زي أضلاع مثلث لضمان تحقيق رقمي ناجح:

1. **Vulnerability/Threat Assessment & Risk Management**
2. **Incident Response / SOC Team**
3. **Digital Forensics / Digital Investigations**

الثلاثة بيكملوا بعض، ومحدش يقدر يشتغل لوحده لو عايزين نوصل لتحقيق كامل.

### 1. Vulnerability Assessment & Risk Management

* **المهمة**: بيختبر سلامة السيستم والسيرفرات (High Integrity).
* **العمل**: يتأكد من إن مفيش ثغرات (Zero-Day أو Vulnerabilities) أو إن الثغرات اتعمل لها Patch.
* **الفايدة**: بيساعد الـ investigator يستبعد فرضيات غلط.
  * **مثال**: لو في هجوم وقالوا يمكن بسبب ثغرة ما ، والـ Risk Manager أكد إن الثغرة دي متقفلة قبل وقت الهجوم → يبقى دي مش السبب.

### 2. Incident Response / SOC Team

* **المهمة**: أول فريق بيتم الرجوع ليه لما يتقال في اختراق أو Suspicious Activity.
* **الأدوات**:
  * **SIEM**: بيجمع Logs.
* **الدور**: بيلم الأدلة الأولية (Artifacts) من اللوجات والتولز، ويشوف لو في Callbacks أو Connections مع C2 Server.
* **الفايدة**: بيدي الـ Investigator بيانات أولية يثبت أو ينفي بيها الفرضيات.

### 3. Digital Forensics / Digital Investigations

* **المهمة**: بيبدأ بعد الـ Incident Response.
* **العمل**: بيركز على تحليل عميق للأدلة (Artifacts + Evidence) ويحافظ عليها قانونيًا (Preservation).
* **الهدف**: يقدم نتايج قوية ومقبولة قانونيًا.



