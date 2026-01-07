# Splunk SIEM Explained a Beginner's Guide In Arabic

what are the  component of splunk, how to deal with splunk&#x20;

#### 1. What is SIEM?&#x20;

الـ SIEM اختصار لـ Security Information and Event Management. هو ببساطة حل (Solution) مركزي بيحل مشكلة تجميع اللوجز (Logs) يدوياً من الأجهزة المختلفة.

وظائف الـ SIEM الأساسية الأربعة:

1. Collecting (التجميع): تجميع اللوجز من مصادر مختلفة في مكان مركزي واحد بدل ما تلف على كل جهاز.
2. Normalizing (التهيئة/المعايرة): تنظيم البيانات دي ووضعها في جداول (Tables) وتنسيق موحد عشان تكون جاهزة للشغل.
3. Analyzing (التحليل): استخدام قواعد (Rules) للبحث عن أنماط معينة (Patterns) داخل اللوجز (مثلاً: البحث عن PowerShell بيستخدم `EncodedCommand`).
4. Alerting (التنبيه): لو الـ Rules لقت تطابق (Match) مع تهديد معين، النظام بيطلع تنبيه (Alert) للمحلل الأمني.

***

#### 2. Log Sources Types (أنواع مصادر اللوجز)

اللوجز اللي بتدخل للـ SIEM بتيجي من نوعين أساسيين:

* Network-Centric: زي اللوجز اللي جاية من الراوتر (Router)، السويتش (Switch)، الـ IPS، أو الـ WAF. دي بتديك معلومات عن الـ Source IP والـ Destination IP وحركة الترافيك.
* Host-Centric: زي اللوجز اللي جاية من أجهزة الويندوز (Windows Workstations) ، اللينكس (Linux)، أو الـ Web Servers. دي بتديك تفاصيل أدق زي مين عمل Access لفايل معين، أو Process حصلها Creation.

***

#### 3. Splunk Components (مكونات سبلانك)

سبلانك (Splunk) هو نوع من أنواع الـ SIEM Solutions، وبيتكون من 3 أجزاء رئيسية (Components) بتشتغل مع بعضها عشان تنفذ المراحل الأربعة اللي قلنا عليها:

**A. The Forwarder (المُرسل)**

* الوظيفة: هو "Agent" (برنامج صغير) بينزل على الـ Endpoints (سواء سيرفرات أو أجهزة موظفين).
* الدور: وظيفته الأساسية Collect Logs (تجميع اللوجز) ويبعتها للـ Indexer.
* أنواعه:
  1. Universal Forwarder (Light): خفيف جداً، وظيفته بس يجمع ويبعت اللوجز زي ما هي.
  2. Heavy Forwarder: تقيل شوية، لأنه بيقدر يعمل Parsing & Filtering (يفلتر البيانات ويحللها مبدئياً) قبل ما يبعتها.

**B. The Indexer (المفهرس)**

* الوظيفة: هو المخزن والمحرك اللي بيستلم البيانات من الـ Forwarder.
* الدور: بيقوم بعملية Indexing، يعني بيعمل Parsing و Filtering للبيانات ويرتبها ويخزنها في فهارس (Indexes) وجداول عشان تكون جاهزة للبحث.

**C. The Search Head (واجهة البحث)**

* الوظيفة: الواجهة اللي بيتعامل معاها الـ User (أنت كـ SOC Analyst).
* الدور: من خلاله بتقدر تعمل Search (بحث)، وتكتب الـ Queries، وتعمل Dashboards، وتشوف الـ Alerts، وتعمل التحقيقات (Investigations)
