# Threat Hunting and IR with XDR/EDR

## Threat Hunting (المفيد المختصر)

#### ✅ تعريف

* **Threat Hunting** = أسلوب أمني **استباقي (Proactive)**، مش بيستنى الإنذارات أو الهجوم يحصل، لكن بيدور بنفسه على التهديدات اللي ممكن تكون دخلت الشبكة من غير ما الأدوات العادية تكشفها.

***

#### ✅ أهم المميزات

1. **Proactive Approach** : البحث عن التهديدات قبل ما تسبب ضرر.
2. **In-Depth Data Analysis:** تحليل عميق للـ logs، network traffic، endpoint data.
3. **Specialized Tools & Techniques:** استخدام أدوات وتقنيات متقدمة مش بس الأدوات التقليدية.
4. **Human-Focused:** بيعتمد بشكل كبير على خبرة المحللين مش على الأتمتة فقط.

***

#### ✅ ليه مهم؟

1. **Evolving Threats** → المهاجمين بيطوروا طرق جديدة (Zero-Day, APTs).
2. **Closing Gaps** → بيكشف الهجمات اللي الأدوات التقليدية ما تقدرش تكشفها.
3. **Comprehensive Visibility** → رؤية كاملة للشبكة، الأجهزة الطرفية، والـ logs.
4. **Damage Reduction** → يقلل فترة وجود المهاجم في الشبكة (dwell time).
5. **Risk Management** → يساعد في إدارة المخاطر وحماية الأصول المهمة.
6. **Human Factor** → البشر يقدروا يلاحظوا أنماط سلوك الأدوات الآلية ممكن تفوتها.

***

## Purpose and Methods of Threat Hunting

#### **Purposes of Threat Hunting (أهداف التهديد hunting):**

* **Proactive Defense** → مش بيستنى الهجوم يحصل، بيبحث عن التهديدات قبل ما تسبب ضرر.
* **Reducing Attacker’s Residence Time** → يقلل المدة اللي المهاجم بيقعدها جوه الشبكة قبل ما يتكشف.
* **Protection Against Advanced Threats** → يحمي ضد هجمات متقدمة زي APTs.
* **Security Posture Improvement** → يوضح الثغرات ويقوي البنية الأمنية.

#### **Methods of Threat Hunting (طرق التهديد hunting):**

* **Hypothesis-Based** → يبدأ بفرضية ويحقق فيها (مثلاً: فيه Malware معين موجود؟).
* **Machine Learning & Analytics** → يعتمد على تحليل السلوك والشذوذ عن الطبيعي.
* **Signature-Based** → يستخدم بصمات/تواقيع لأنشطة ضارة معروفة.
* **TTP-Based** → يركز على التكتيكات والتقنيات اللي بيستخدمها المهاجم (بناءً على CTI).
* **Automation & Triage** → استخدام أدوات تلقائية للتصنيف المبدئي للأحداث المشبوهة.



### 🎯 **Threat Hunting Techniques with EDR/XDR**

مع إن **EDR/XDR** من أهم الأدوات في الـ Threat Hunting، لكنها مش كفاية لوحدها. بنحتاج أدوات تانية زي:

* **SIEM:** لتجميع وربط وتحليل الـ logs.
* **CTI (Cyber Threat Intelligence)** → معلومات استخباراتية عن التهديدات.
* **NIDS/NDR** → للكشف عن التهديدات على مستوى الشبكة.
* **Sandboxes** → لتشغيل الملفات المشبوهة في بيئة معزولة وتحليل سلوكها.

***

### 🛠 **الطرق الأساسية للـ Threat Hunting باستخدام EDR/XDR**

#### 1. **Indicator-based Hunting**

* يعتمد على **IOC** (Indicators of Compromise) زي IP، domain، hash، URL.
* الـ IOCs ممكن تيجي من:
  * أحداث تم كشفها قبل كده.
  * مصادر عامة.
  * Threat Intel خاصة أو قطاعية.
* **مثال**: تقرير بيقول إن Botnet بيتحكم فيه من IP معين → المحلل بيدور على الـ IP ده في Network Traffic بتاع المؤسسة علشان يعرف إذا فيه اتصال أو لا.

***

#### 2. **Behavioral-based Hunting**

* بدل ما يعتمد على IOCs، بيركز على **سلوك غير طبيعي** للـ users أو الـ systems.
* **مثال**:
  * User عادي بيشغل أدوات إدارية (زي PowerShell أو CMD) بامتيازات Admin.
  * مستخدم مش مفروض يفتح برامج معينة لكن فجأة بيستخدمها.
* ده بيعتمد على **analytics** + **baseline** (السلوك الطبيعي).

***

#### 3. **Heuristic Hunting**

* مش بيعتمد على signatures أو IOCs معروفة، إنما على **قواعد عامة** + **تحليل سلوكيات مش طبيعية**.
* مناسب للتهديدات الجديدة أو الـ Zero-day.
* **مثال**: جهاز بيعمل **Port Scanning سريع جدًا** لآلاف البورتات في ثواني → نشاط مش طبيعي وغالبًا ضار.

***

### 🔎 **Threat Hunting with SentinelOne**

واحدة من أقوى المنصات اللي بتساعد في الـ Threat Hunting.

#### ✨ **مميزات أساسية:**

* **Deep Visibility**: بتجمع Telemetry Data ضخمة تقدر تبحث فيها (IP، domain، URL، hash).
* **Retention**: البيانات بتاعة الـ hunting بتتخزن 14 يوم افتراضيًا.
* **Queries**: تقدر تستخدم Search Bar “Start Hunting” (Autocomplete بيساعدك تقترح fields).
* **Tabs مختلفة** لعرض البيانات:
  * Processes
  * Cross Process
  * Indicators
  * Files
  * Network Actions
  * DNS
  * URL
  * Registry
  * Scheduled Tasks
  * Logins
  * Driver Load
  * Command Scripts

## 🎯 **Threat Hunting Techniques with EDR/XDR**

مع إن **EDR/XDR** من أهم الأدوات في الـ Threat Hunting، لكنها مش كفاية لوحدها. الصيادين بيحتاجوا أدوات تانية زي:

* **SIEM** → لتجميع وربط وتحليل الـ logs.
* **CTI (Cyber Threat Intelligence)** → معلومات استخباراتية عن التهديدات.
* **NIDS/NDR** → للكشف عن التهديدات على مستوى الشبكة.
* **Sandboxes** → لتشغيل الملفات المشبوهة في بيئة معزولة وتحليل سلوكها.

***

### 🛠 **الطرق الأساسية للـ Threat Hunting باستخدام EDR/XDR**

#### 1. **Indicator-based Hunting**

* يعتمد على **IOC** (Indicators of Compromise) زي IP، domain، hash، URL.
* الـ IOCs ممكن تيجي من:
  * أحداث تم كشفها قبل كده.
  * مصادر عامة.
  * Threat Intel خاصة أو قطاعية.
* **مثال**: تقرير بيقول إن Botnet بيتحكم فيه من IP معين → المحلل بيدور على الـ IP ده في Network Traffic بتاع المؤسسة علشان يعرف إذا فيه اتصال أو لا.

***

#### 2. **Behavioral-based Hunting**

* بدل ما يعتمد على IOCs، بيركز على **سلوك غير طبيعي** للـ users أو الـ systems.
* **مثال**:
  * User عادي بيشغل أدوات إدارية (زي PowerShell أو CMD) بامتيازات Admin.
  * مستخدم مش مفروض يفتح برامج معينة لكن فجأة بيستخدمها.
* ده بيعتمد على **analytics** + **baseline** (السلوك الطبيعي).

***

#### 3. **Heuristic Hunting**

* مش بيعتمد على signatures أو IOCs معروفة، إنما على **قواعد عامة** + **تحليل سلوكيات مش طبيعية**.
* مناسب للتهديدات الجديدة أو الـ Zero-day.
* **مثال**: جهاز بيعمل **Port Scanning سريع جدًا** لآلاف البورتات في ثواني → نشاط مش طبيعي وغالبًا ضار.

***

### 🔎 **Threat Hunting with SentinelOne**

واحدة من أقوى المنصات اللي بتساعد في الـ Threat Hunting.

#### ✨ **مميزات أساسية:**

* **Deep Visibility**: بتجمع Telemetry Data ضخمة تقدر تبحث فيها (IP، domain، URL، hash).
* **Retention**: البيانات بتاعة الـ hunting بتتخزن 14 يوم افتراضيًا.
* **Queries**: تقدر تستخدم Search Bar “Start Hunting” (Autocomplete بيساعدك تقترح fields).
* **Tabs مختلفة** لعرض البيانات:
  * Processes
  * Cross Process
  * Indicators
  * Files
  * Network Actions
  * DNS
  * URL
  * Registry
  * Scheduled Tasks
  * Logins
  * Driver Load
  * Command Scripts

***

تمام 👌 خلينا ناخد الكلام ده ونفكّكه شرح تفصيلي خطوة بخطوة بحيث ما نفوّت ولا نقطة، ونربطه كويس بموضوع **Incident Response مع EDR/XDR**.

***

### أولاً: Incident Response Process (المراحل الأساسية)

Incident management أو Incident Response عبارة عن دورة متكاملة هدفها تقلل تأثير الهجمات وتخلّي المؤسسة جاهزة دايمًا. المراحل الرئيسية:

1. **Incident Detection – اكتشاف الحادث**
   * يتم باستخدام Firewalls, IDS/NDR, EDR/XDR.
   * الهدف: تلتقط الـ “signal” الأول اللي يقول فيه نشاط غير طبيعي (ملف غريب، اتصال خارجي مشبوه، login غير مألوف).
2. **Incident Investigation – التحقيق**
   * SOC أو Incident Response Team يحلّل البيانات بالأدوات (SIEM, Threat Intel, Forensics tools).
   * هنا الفريق بيجاوب: إيه اللي حصل؟ إمتى؟ على أي جهاز أو يوزر؟ مدى الانتشار؟
3. **Incident Response – الاستجابة**
   * بمجرد التأكد، يتم التحرك فورًا.
   * الأدوات: EDR يعزل الجهاز، XDR يوقف سيشن مشبوه، Firewall يعمل block IP، إلخ.
   * الهدف: وقف النزيف قبل ما الحادث يتوسع.
4. **Incident Remediation – المعالجة/التصحيح**
   * البحث عن سبب الحادث (Root Cause).
   * تحديثات، إغلاق ثغرات، تحسين ضوابط الوصول، تدريب المستخدمين.
   * الهدف: منع تكرار الهجوم مرة تانية.

***

### ثانياً: دور EDR/XDR في Incident Response

EDR/XDR بيزوّد المراحل ديه بقيمة ضخمة، خلينا نشوف إزاي:

#### 1. **Early Threat Detection (الكشف المبكر)**

* **EDR** يراقب الأجهزة (Endpoints) زي لابتوبات وسيرفرات. يلاحظ سلوك غير طبيعي: process غريب، execution مش مألوف.
* **XDR** بيراقب كمان الشبكة، الـ cloud، والـ identities. يربط الأحداث: مثلاً جهاز بدأ يتصل بـ C2 بعد ما يوزر استلم إيميل phishing.
* الفايدة: الاكتشاف بيحصل بدري جدًا → يقلّل وقت المهاجم داخل الشبكة.

***

#### 2. **Rapid Response Capacity (قدرة الاستجابة السريعة)**

* **EDR/XDR** عنده Automation:
  * Quarantine file.
  * Isolate endpoint من الشبكة.
  * Kill process.
  * Block IP/domain أو سحب صلاحيات user.
* الفايدة: الاستجابة سريعة، بتوقف الهجوم قبل ما ينتشر (مثلاً ransomware قبل ما يشفّر باقي الأجهزة).

***

#### 3. **Detailed Analysis and Diagnosis (تحليل وتشخيص مفصّل)**

* EDR/XDR بيجمع تفاصيل الهجوم:
  * إيه الملف اللي بدأ الهجوم؟
  * إيه العمليات اللي اتولدت بعده؟
  * مين اليوزر اللي استُخدم؟
  * إيه الأجهزة اللي اتأثرت؟
* ده بيساعد الفريق يفهم الـ Root Cause ويعمل containment/remediation مظبوط.

***

#### 4. **Identifying the Chain of Events (تحديد سلسلة الأحداث)**

* XDR ممتاز في الحتة دي → بيربط القطع ببعض:
  * Step 1: Phishing Email
  * Step 2: User clicks attachment
  * Step 3: Malware execution
  * Step 4: C2 traffic
  * Step 5: Lateral Movement
* الفايدة: تبني Attack Timeline كاملة تساعد في فهم السيناريو وحماية الشبكة مستقبلًا.

***

#### 5. **Provide Visibility (الرؤية الشاملة)**

* **EDR** → رؤية endpoints (processes, files, users).
* **XDR** → رؤية أكبر تشمل الشبكة + الـ cloud + الـ apps.
* الفايدة: لو المهاجم بيلف من جهاز لشبكة لـ cloud، الفريق يقدر يشوف الصورة كاملة.

***

#### 6. **Automation and Efficiency (الأتمتة والكفاءة)**

* XDR بيشيل شغل ممل من البشر: correlation, alert grouping, automated playbooks.
* يقلّل الـ human error ويخلي SOC أسرع وأكثر فاعلية.

***

#### 7. **Data Collection and Storage (جمع وتخزين البيانات)**

* EDR/XDR بيخزن logs & telemetry.
* مهم جدًا:
  * للتحقيق بعد الحادث.
  * للدروس المستفادة.
  * للتقارير (Compliance, Audit).

***

#### 8. **Learning and Improvement (التعلم والتحسين)**

* كل حادث بيولّد دروس: إيه اللي نجح؟ فين الثغرة؟
* XDR/EDR بيوفر data & reports تساعد تبني defenses أقوى (زي تحديث rules أو training للمستخدمين).

***

#### 9. **Integration of Various Data Sources (تكامل المصادر)**

* **XDR** بيلمع هنا: يدمج بيانات من EDR + NDR + Email + Cloud + IAM + Threat Intel.
* الفايدة: رؤية موحدة من كل الجوانب → يقلل blind spots.

***

#### 10. **Data Based Decision Making (قرارات مبنية على البيانات)**

* التقارير والتحليلات من EDR/XDR → تساعد الفريق يتخذ قرارات صحيحة.
* مثال: إغلاق خدمة؟ عزل جهاز؟ أم مجرد مراقبة؟
