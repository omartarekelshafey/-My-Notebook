# Splunk SIEM Explained a Beginner's Guide

## 1. What's SIEM?

مصطلح الـ SIEM هو اختصار لـ Security Information and Event Management. هو ببساطة حل (Solution) مركزي بيحل مشكلة تجميع اللوجز (Logs) يدوياً من الأجهزة المختلفة.

الوظائف الأساسية للـ SIEM (تتلخص في 4 مراحل):

* مرحلة (Collecting): تجميع اللوجز من مصادر مختلفة في مكان مركزي واحد بدل ما تلف على كل جهاز.
* مرحلة (Normalizing): تنظيم البيانات دي ووضعها في جداول (Tables) وتنسيق موحد عشان تكون جاهزة للشغل.
* مرحلة (Analyzing): استخدام قواعد (Rules) للبحث عن أنماط معينة (Patterns) داخل اللوجز (مثلاً: البحث عن PowerShell بيستخدم EncodedCommand).
* مرحلة  (Alerting): لو الـ Rules لقت تطابق (Match) مع تهديد معين، النظام بيطلع تنبيه (Alert) للمحلل الأمني.

***

## 2. Log Sources Types

البيانات واللوجز اللي بتدخل للـ SIEM بتيجي من نوعين أساسيين:

* النوع الأول (Network-Centric): زي اللوجز اللي جاية من الراوتر (Router)، السويتش (Switch)، الـ IPS، أو الـ WAF. دي بتديك معلومات عن الـ Source IP والـ Destination IP وحركة الترافيك.
* النوع الثاني (Host-Centric): زي اللوجز اللي جاية من  (Windows Workstations)، (Linux)، أو الـ Web Servers. دي بتديك تفاصيل أدق زي مين عمل Access لفايل معين، أو Process حصلها Creation.

***

## 3. Splunk Components

#### A. The Forwarder

* الوظيفة: هو "Agent" (برنامج صغير) بينزل على الـ Endpoints (سواء سيرفرات أو أجهزة موظفين).
* الدور: وظيفته الأساسية Collect Logs (تجميع اللوجز) ويبعتها للـ Indexer.
* الأنواع:
  * النوع (Universal Forwarder): خفيف جداً، وظيفته بس يجمع ويبعت اللوجز زي ما هي.
  * النوع (Heavy Forwarder): تقيل شوية، لأنه بيقدر يعمل Parsing & Filtering (يفلتر البيانات ويحللها مبدئياً) قبل ما يبعتها.

#### B. The Indexer

* الوظيفة: هو المخزن والمحرك اللي بيستلم البيانات من الـ Forwarder.
* الدور: بيقوم بعملية Indexing، يعني بيعمل Parsing و Filtering للبيانات ويرتبها ويخزنها في فهارس (Indexes) وجداول عشان تكون جاهزة للبحث.

#### C. The Search Head

* الوظيفة: الواجهة اللي بيتعامل معاها الـ User (أنت كـ SOC Analyst).
* الدور: من خلاله بتقدر تعمل Search (بحث)، وتكتب الـ Queries، وتعمل Dashboards، وتشوف الـ Alerts، وتعمل التحقيقات (Investigations).
