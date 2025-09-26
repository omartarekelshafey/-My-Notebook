# CH 2

## Digital Forensics process

### Identification

* أول خطوة: بيتم التعرف على إن في جريمة أو مشكلة حصلت.
* بنحدد المعلومات الأساسية عن القضية (هل هي جريمة قتل، جريمة إلكترونية، شخص مفقود، ...).
* الهدف: تجميع كل البيانات الأولية اللي هتوجهنا في التحقيق.

### Collection (Acquisition)

* جمع الـ **Artifacts** (الحاجات اللي ممكن تكون مرتبطة بالجريمة).
* زي الأدوات اللي في مسرح الجريمة (في الطبيعي: مسدس، آثار أقدام... في digital: ملفات، Logs، Emails...).
* مهم نعرف الفرق بين:
  * **Artifact**: أي حاجة اتجمعت من مسرح الجريمة سواء مرتبطة بالقضية أو لا.
  * **Evidence**: حاجة طلعت من الـ Artifact وليها تأثير مباشر على القضية (زي بصمة المجرم مش كل البصمات).

### Preservation

* الحفاظ على الأدلة الرقمية بعد جمعها.
* الهدف: منع أي تغيير أو تلف في الأدلة.
* خطوات الحفظ:
  * الاحتفاظ بالنسخة الأصلية في مكان آمن وصعب التلاعب بيه.
  * أي تجارب أو اختبارات (Examination) بتتعمل على نسخ من الأدلة مش الأصل.
* مثال: صورة اتعمل عليها تعديل ممكن تفقد Metadata → علشان كده لازم النسخة الأصلية تتخزن بشكل آمن.

### Analysis

* بيتم فيها فحص الأدلة (Artifacts) عشان نطلع منها **Evidence**.
* بتحصل عملية إنشاء الـ **Timeline** (الخط الزمني للأحداث).
* الهدف: استخراج الدليل اللي يثبت أو ينفي الوقائع.
* هنا بيتحول الـ Artifact إلى Evidence مع تأثير مباشر على القضية.

### Reporting

* آخر خطوة: كتابة تقرير جنائي رقمي.
* التقرير بيشمل:
  * التجارب اللي اتعملت.
  * النتائج اللي اتوصلنا ليها.
  * النظريات المطروحة وربطها بالأدلة.

## انت كا Forensics practitioner محتاج ايه ؟

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p>هو ده اللي انت محتلجه كا  Forensics practitioner </p></figcaption></figure>



## &#x20;(Forensic Methodology)

في تلات حاجات اساسيه في methodology \


<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### 1. 🔍 Hypothesis/Prediction (الفرضية/التوقع)

* **الدور**: تبدأ العملية بتوقع مبدئي بناءً على المعلومات الأولية (مثلاً: "هذا الشخص قام بالهجوم").
* **التنفيذ**: في مرحلة **Field Work**، تجمع البيانات وتحدد نقاط الاكتساب (Acquisition Points) عشان تبني الفرضية دي. زي ما قلت، "الفردية دي بتتحط على أساس إني متوقع حاجة حصلت".
* **الأهمية**: دي البداية اللي بتخطط ليها قبل ما تبدأ الاكتساب أو التحليل.

### 2. 🧪 Validation (التحقق)

* **الدور**: لازم تتحقق من الفرضية عشان تتجنب التحيز. زي ما قلت، "لو مفيش فالديشن، ممكن تحور الأدلة عشان تثبت فرضيتك".
* **التنفيذ**: يتم التحقق عن طريق **مراجعة زميل (peer review)** أو محلل تاني بنفس المستوى أو أعلى. ده بيحدث في **Lab Work** بعد التحليل، ويمكن يقول لك "البروف مش كافي، اعيد الشغل".
* **الأهمية**: التحقق بيضمن إن النتيجة نزيهة ومش متأثرة بآرائك الشخصية. لو الفرضية غلط، الأدلة هتثبت كده وتفتح باب فرضيات تانية.

### 3. ✅ Proof (الإثبات)

* **الدور**: النتيجة النهائية اللي بتثبت الفرضية أو تنفيها (مثلاً: "المتهم بريء لأن مفيش دليل").
* 💡 الدليل لازم يكون **مستخرج بشكل علمي** + **متوثق كويس** علشان يقف في المحكمة.

### example of methodology steps &#x20;

### 1. 🔍 Field Work

**steps**

* **Get Authority:** لازم تاخد إذن رسمي (من المدير، النيابة، إلخ) قبل ما تبدأ.
* **Collecting Basic Information:** اجمع كل بيانات القضية (زي نوع الجهاز المصاب) قبل الاكتساب.
* **Determine Acquisition Points:** حدد مصادر البيانات (مثلاً: إيميلات معينة، لا كل الجهاز).
* **Acquisition:** استخدم أدوات لسحب البيانات (مثل استخراج الـ logs أو الميموري).
* **Coding/Recording/Labeling:** ضع labelعلى كل artifact يوضح المحتوى
* **Preservation/Submission:** احفظ الأدلة وسلمهم مع تقرير يحتوي على الفرضية.
* **Reporting/Hypothesis:** ارفع تقرير يوضح الـ artifacts والفرضية (مثلاً: "هذا الشخص المتهم").

### 2. 🧪 Lab Work

**steps**&#x20;

* **Acquire:** استلم الـ artifacts من Field Work مع الـ label والـ Chain of Custody (فورم يوضح انتقال الأدلة).
* **Cloning:** اصنع نسخة من الـ image عشان تحافظ على الأصل وتعمل عليها.
* **Extraction:** اني اطلع ال **Evidence**\
  **Analysis:** تحليل البيانات لإثبات أو نفي الفرضية.
* **Proof:** قدم دليل قوي يثبت الفرضية أو ينفيها .

## Types Digital Forensics

### Volatile vs Non-volatile Forensics

#### 🔹 Volatile Forensics (الأدلة المتطايرة)

* الأدلة اللي بتفقد بسرعة مع فصل الكهرباء.
* أشهر مثال: **الـ Memory (RAM)**.
* أول ما التيار الكهربائي يتفصل، البيانات اللي فيها بتروح.
* أمثلة:
  * Memory Forensics
  * Network Forensics (لأن الترافيك بيتفقد لو ما اتعملش له Capture في الوقت الحقيقي).

#### 🔹 Non-volatile Forensics (الأدلة غير المتطايرة)

* الأدلة اللي ما بتضيعش بفصل الكهرباء.
* مثال: **Hard Disk** (البيانات والميتاداتا محفوظة).
*   أمثلة:

    * File System & OS Forensics
    * Storage/Disk Forensics
    * Mobile Device Forensics
    * Image, Video & Audio Forensics



1. **File System & OS Forensics**
   * تحليل الـ File System والـ OS (Windows, Linux, macOS, Android).
2. **Storage/Disk Forensics**
   * تحليل الديسك نفسه حتى لو الفايل سيستم متدمر.
3. **Memory Forensics**
   * تحليل محتوى الرام.
   * مهم جدًا لأنه بيوضح البرامج اللي كانت شغالة وقت معين.
4. **Network Forensics**
   * التقاط وتحليل الترافيك.
   * لازم يحصل Capture في نفس اللحظة، وإلا البيانات بتضيع.
5. **Mobile Device Forensics / IoT Forensics**
   * تحليل الموبايلات والأجهزة الذكية.
   * فيها Storage + Memory.
6. **Image, Video & Audio Forensics**
   * يركز على التلاعب بالصور والفيديوهات والصوتيات (زي قضايا الـ Deepfake).

***

### Artifacts Types

* **Web Browser History**&#x20;
* **Download & Temporary Files**&#x20;
* **Printer Logs**&#x20;
* **Registry**&#x20;
* **Deleted Files**&#x20;
* **Emails**&#x20;
* **SMS** .
* **Photos taken by digital cameras**
* **Event Logs**&#x20;
* **Applications & Packages**
* **Social Media & OSINT**



## Stat Command

### `ls -l`

* بيعرضلك تفاصيل عن الملفات بشكل طويل:
  * **Permissions**:&#x20;
  * **Timestamps**: تاريخ آخر تعديل (Modification Time).

**example**

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### 3. استخدام أمر `stat`

* بيديك تفاصيل أعمق عن الملف مقارنة بـ `ls`.
* بيعرض:
  * **Inode**:  بيديك مكان ال file  علي الهارد.
  * **Size**
  * **Blocks**: عدد البلوكات اللي مستخدمها الملف.
  * **File Type**:
  * **Timestamps**:
    * **Access**
    * **Modify**
    * **Change**&#x20;
    * **Birth**&#x20;

example

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

***

### 5. Notes

*   **Move file** :

    * الـ **Inode** بيبقى زي ما هو  معناه إن الملف متغيرش فعليًا، بس مكانه اتغير.

    before move                                                                              after move&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/image (23).png" alt="" width="375"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/Screenshot 2025-09-05 124816.png" alt="" width="375"><figcaption></figcaption></figure></div>

*   **Copy الملف**:

    * بيتولد **Inode جديد** → يعني اتكتب فعليًا نسخة جديدة.

    before copy                                                                                  after copy&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-05 124816.png" alt="" width="375"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/Screenshot 2025-09-05 125318.png" alt="" width="375"><figcaption></figcaption></figure></div>

## EXIF TOOL

&#x20;هنجرب دلوقتي نفس اللي عملناه بال stat بس المرادي هنستعمل exif tool&#x20;

اول  حاجه نزلها لو مش عندك ب sudo apt install exif \
&#x20;       بعدها  تكتب Exif  واسم الصورة&#x20;

example

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-05 160704.png" alt=""><figcaption></figcaption></figure>



## windows properties

#### 1**Original File**

اي ملف خلينا نقول صورة مثلا بيكون فيها ال meta data  ديه&#x20;

* **Creation Date** (تاريخ الإنشاء).
* **Modification Date** (آخر تعديل).
* **Access Date** (آخر مرة تم فتحه).
* الميتاداتا الأصلية موجودة (نوع الموبايل – الكاميرا – وقت الالتقاط – البرنامج اللي صور بيه).

#### &#x20;**Paint**

* لما فتحت الصورة في **Paint** وعدلتها وبعدها عملت save&#x20;

كده ال meta data  اللي كانت موجوده في اول هتتغير لانه احنا عدلنا علي الصورة&#x20;

***

#### 3. **Copy-Paste**&#x20;

* لما عملت **Copy-Paste** للصورة:
  * الميتاداتا الأصلية فضلت زي ما هي.
*   الاستنتاج:

    النسخ العادي بيحافظ على الميتاداتا.

    ينفع لو الهدف إننا نعرض الميتاداتا في المحكمة.

بس طبعا الطريقه هتبقي غلط لو انا مهتم بمكان الفايل في الهارد  لانه لما بتعمل copy  مكان الفايل بيتغير في الهارد
