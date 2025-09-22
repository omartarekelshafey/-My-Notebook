# siem part 1

ELASTICSEARCH (DATABASE ENGINE)

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>



| **Rational Database** | **Elasticsearch** | **الشرح**                                                                      |
| --------------------- | ----------------- | ------------------------------------------------------------------------------ |
| **DB Server**         | **ES Node**       | السيرفر اللي بيشغل قاعدة البيانات ↔ النود اللي بيشغل Elasticsearch.            |
| **Table**             | **Index**         | الجدول اللي بيخزن البيانات ↔ الـ Index اللي بيخزن Documents.                   |
| **Table Schema**      | **Mapping**       | تعريف الجدول (أعمدة + أنواع البيانات) ↔ تعريف الـ Index (Fields + Data Types). |
| **Row**               | **Document**      | كل صف بيانات في الجدول ↔ Document واحد في Elasticsearch.                       |
| **Column**            | **Field**         | العمود في الجدول ↔ Field داخل Document.                                        |

## elastic search shards

تمام، خلينا نشرحها واحدة واحدة وبطريقة سهلة:

أول حاجة، **فهم فكرة الـ Shard**:\
تخيل عندك كتاب كبير جدًا من 1000 صفحة. بدل ما يبقى في إيد شخص واحد يقرأه كله، ممكن تقسمه لـ 10 أجزاء (كل جزء 100 صفحة). كده 10 أشخاص يقدروا يقروا الكتاب في نفس الوقت.\
الجزء اللي كل واحد ماسكه = **Shard**.

***

#### أنواع الـ Shards:

1. **Primary Shards**\
   دي النسخة الأصلية للبيانات. يعني الجزء الأساسي اللي Elasticsearch بيقسم عليه الداتا لما تعمل Index جديد.\
   مثال: لو عندك جدول كبير من العملاء، الـ primary shards هما اللي ماسكين البيانات الأساسية.
2. **Replica Shards**\
   دي نسخ مطابقة من الـ primary shards. فايدتها حاجتين:
   * **Fault Tolerance**: لو shard أساسي وقع أو السيرفر بتاعه باز، النسخة الاحتياطية (Replica) موجودة.
   * **Load Balancing**: ممكن تستخدمها في البحث عشان السرعة (توزيع الضغط).

***

#### ليه الـ Shards مهمة؟

* **Data Distribution**: بتخلي البيانات الكبيرة تتوزع على أكتر من سيرفر.
* **Parallel Processing**: البحث أو التحليل بيتقسم على shards مختلفة في نفس الوقت، فيسرع الأداء.
* **Fault Tolerance**: حتى لو جزء من الداتا باز أو السيرفر وقع، النسخ (Replicas) تحفظلك الداتا وتخلي السيستم شغال.



## Nodes types

تمام 👌 خلينا نفصصها واحدة واحدة بنفس أسلوب الـ Shards

#### أنواع الـ Nodes:

1. **Data Node** 🗄️
   * هو اللي شايل **الـ Shards** (البيانات الفعلية).
   * أي Index بيتقسم ويتخزن على الـ Data Nodes.
   * كمان هو اللي بينفذ العمليات التقيلة زي البحث (queries) والـ aggregations.

***

2. **Coordinating Node** 🔀
   * زي **Traffic Manager**.
   * بياخد الـ request من العميل ويوزعها على الـ Data Nodes.
   * بيجمع النتايج من أكتر من Node ويرجعها للعميل بشكل مرتب.
   * لو الـ request للـ indexing، يبعته للـ **Ingest Node** الأول.
   * مهمته كمان يتأكد إن مفيش **duplicates** راجعة من الـ Shards.

***

3. **Ingest Node** ⚙️
   * متخصص في **تحضير البيانات قبل التخزين**.
   * بيستخدم حاجة اسمها **Ingest Pipelines** فيها Processors (زي GROK أو Date parser).
   * مثال: لو عندك logs عشوائية، الـ Ingest Node ممكن يظبطها قبل ما يخزنها.

***

4. **Master Node** 👑
   * هو اللي ماسك **العقل المدبر للكلاستر**.
   * مسؤول عن إدارة الـ cluster state (مين موجود؟ إيه الـ indices؟ إيه حالة الـ nodes؟).
   * بيتحكم في إنشاء الـ indices، إضافة/إزالة nodes، وتوزيع الـ shards.
   * ملحوظة: مش بيمسك بيانات فعلية (مش Data Node)، هو إداري أكتر.

***

5. **Machine Learning Node** 🤖
   * بيشغل الـ ML jobs (ميزة X-Pack ML).
   * ممكن تديه مثلاً مهمة anomaly detection على logs.
   * بيشتغل لو أنت مفعل الـ ML feature في Elastic.

***

#### ملاحظة مهمة:

* Node واحد ممكن ياخد **أكتر من دور** (يعني ينفع يبقى Data + Ingest في نفس الوقت).
* في الـ production عادة بنفصل الأدوار عشان الأداء والـ scaling.



**DATA COLLECTING METHODS**\
**Agent-Based**\
Elastic Agent\
Beats

\
**Agent-Less**\
Syslog\
API\
etc

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

