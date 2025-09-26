# CH5

### Introduction to Windows Registry

هنبدأ الأول بالـ Windows، وهنبدأ بأهم حاجة بتميز الـ Windows عن باقي أنظمة التشغيل وهي **الـ Registry**.\
الـ Registry بتكون متسجلة في ملفات بنسميها **Hive**، وهي اللي بتحتوي على معظم الـ Configuration والـ Cache الخاصة بالـ User أو بالـ Operating System.

***

### Accessing the Registry

* من قائمة Start في Windows نكتب `regedit` → ده هيفتح أداة اسمها **Registry Editor**.
* الـ Registry Editor هي Tool موجودة جوه الـ Windows بتسمحلك تعرض وتعدل على الـ Registry.

<div align="left"><figure><img src="../../.gitbook/assets/image (3).png" alt="" width="375"><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/Screenshot 2025-09-09 233312.png" alt="" width="270"><figcaption></figcaption></figure></div>

***

### History of the Registry

* قبل Windows 95، الـ Windows كان لسه بسيط، ومعظم الـ Configurations سواء بتاعة الـ Applications أو الـ Users أو حتى الـ OS نفسه، كانت بتتسجل في ملفات عادية اسمها **.ini files**.
* من بعد Windows 95، مايكروسوفت بدأت تنقل الملفات دي وتخزنها في شكل جديد اسمه **Registry**.

***

### Main Registry Hives

الـ Registry بتتكون من 5 Hives أساسية موجودة في أي Windows version تقريبًا:

1. **HKEY\_CLASSES\_ROOT**
   * فيه معظم الـ File Types والـ Extensions Information الخاصة بالـ Operating System.
2. **HKEY\_CURRENT\_USER**
   * فيه كل البيانات الخاصة بالـ User اللي شغال دلوقتي على المكنة.
   * بيحتوي على Application Settings، System Settings، Environment Variables… إلخ.
3. **HKEY\_LOCAL\_MACHINE**
   * فيه معظم ملفات الـ Configuration الخاصة بالـ Applications والـ Operating System نفسه.
   * مثال: Security Configurations، Installed Software، System Configurations.
4. **HKEY\_USERS**
   * فيه معلومات عن كل الـ Users اللي عملوا Login على الـ System.
   * كل User بيكون عنده SID خاص بيه متسجل هنا.
5. **HKEY\_CURRENT\_CONFIG**
   * فيه بيانات متعلقة بالـ Hardware Configuration الحالي.

***

### Important Hives for Forensics

إحنا كـ Forensics Investigators بنهتم بالـ Hives دي أكتر:

* **HKEY\_CURRENT\_USER**
* **HKEY\_LOCAL\_MACHINE**
* **HKEY\_USERS**

مثال:

* في HKEY\_USERS هتلاقي إن كل User عنده SID متسجل، وكل User عمل Login هتلاقي بياناته موجودة تحت الـ SID بتاعه.
* HKEY\_CURRENT\_USER → ده الـ User اللي شغال حاليًا.
* HKEY\_LOCAL\_MACHINE → فيه بيانات الـ Security، الـ Software، والـ Configurations الخاصة بالـ OS.

***

### Registry Storage

الـ Registry في الآخر عبارة عن ملفات بيتم تخزينها على الـ Windows.

مثال:

* الـ **HKEY\_CURRENT\_USER** بيتسجل جوه ملف موجود في:\
  `C:\Users\<Username>\NTUSER.DAT`
  * كل User عنده ملف خاص بيه.
  * الملف ده زي Database شايل بيانات الـ Registry الخاصة بالـ User.
  * الملف ده اسمه **Hive**.

***

### Extracting Registry Hives

طب إزاي أقدر أعمل Extraction للـ Hive؟

* لو عملت Copy/Paste عادي للملف → مش هينفع، لأن الـ Windows بيحمي ملفات الـ .dat اللي متعلقة بالـ Registry.
* الملفات دي بنسميها **Protected System Files**.

***

### Using FTK Imager

نقدر نستخرج الـ Hives باستخدام Tools زي **FTK Imager**:

**Step 1 — Add Evidence Item**\
**Step 2 — Open C Drive**\
**Step 3 — select root folder**\
**Step 4 —select users folder and select user folder**\
**Step 5 — Locate NTUSER.DAT**

* مثال:
  * جوه فولدر الـ User → هتلاقي ملف `NTUSER.DAT`.
  * هتلاقي كمان `NTUSER.DAT.LOG` → دي عبارة عن **Transaction Files**.
  * الـ Transaction Files دي بتخزن التغييرات اللي بيعملها الـ User مؤقتًا (زي ما بيفتح Browser أو يعمل Search) قبل ما تترحل للـ Hive الرئيسي
* لو أخدت `NTUSER.DAT` بس → ده اسمه **Dirty Hive** (غير مكتمل)، لأنه لسه في تغييرات متسجلتش.

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-09 224442.png" alt=""><figcaption></figcaption></figure>

***

### Registry Hive Locations

باقي الـ Hives بتتخزن في:\
`C:\Windows\System32\config\`

أمثلة:

* `SAM` → Accounts + User Info.
* `SYSTEM` → System Configuration.
* `SOFTWARE` → Installed Applications.
* `SECURITY` → Security Policies.

***

### Protected Files Extraction

الموضوع ممكن يتعمل Manual، لكن الأفضل نستخدم الـ Option اللي موجود في FTK Imager وهو:\
**Obtain Protected Files**

* ده بيطلعلك كل الـ Hives (SAM, SYSTEM, SOFTWARE, SECURITY, NTUSER.DAT, …).



<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-09 225411.png" alt="" width="467"><figcaption><p>manual method</p></figcaption></figure></div>



***

### Example with FTK Imager

اول من file  اختار**Obtain Protected Files**

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-09 225433.png" alt="" width="260"><figcaption></figcaption></figure></div>

* حدد مكان تحفظ فيه files
* بيظهرلك Option:
  * **Password recovery only**&#x20;
  * **Password recovery and all registry files**&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="306"><figcaption></figcaption></figure></div>

### **result**&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-09 230135.png" alt=""><figcaption></figcaption></figure>

## Registry Analysis in Digital Forensics

### Problem with Using Regedit

* ملفات الـ **Registry Hives** بتتبعتلك كـ evidence.
* لو حاولت تفتحها بـ **Regedit** العادي، هو مش هيسمحلك تختار ملف خارجي.
* السبب: Regedit بيقرأ الـ **active registry** بتاع الـ Operating System اللي شغال حاليًا على جهازك.
* وبالتالي لو فتحت حاجة، هتكون بتشوف الـ registry بتاع جهازك مش بتاع جهاز الضحية (Forensic Lab).

***

### Registry Explorer (Eric Zimmerman’s Tool)

* عشان نحل المشكلة دي بنستخدم **Registry Explorer** (من أدوات Eric Zimmerman – SANS Instructor).
*   ممكن تنزلها من:

    [https://ericzimmerman.github.io/#!index.md](https://ericzimmerman.github.io/#!index.md)
* التول بتتوزع كـ **ZIP File** → تعملها extract.
* لازم يكون عندك **.NET Framework v4**.

***

### Dirty Hives and Transaction Logs

* أوقات لما تـ Load Hive بيظهرلك تحذير: **Dirty Hive**.
  * معناها: مش كل البيانات اتحفظت.
  * في Transaction Logs ناقصة.

<div align="left"><figure><img src="../../.gitbook/assets/1 (1).png" alt="" width="455"><figcaption></figcaption></figure></div>

## 🛠️ Handling Dirty Hives



#### 1. Extraction من FTK Imager

* **Step 1 — Add Evidence Item**\
  **Step 2 — Open C Drive**\
  **Step 3 — select root folder**\
  **Step 4 —select users folder and select user folder**\
  **Step 5 — Locate NTUSER.DAT**

#### 2. Export الملفات

* اعمل Export للفايلز واختر فولدر مخصص ليهم.
* هتلاقي مع الـ Hive ملفات زي:
  * `.LOG1`
  * `.LOG2`
  * أحيانًا `.LOG3`

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 175248.png" alt="" width="563"><figcaption></figcaption></figure></div>

#### 3. Load في Registry Explorer

* افتح **Registry Explorer**.
* اعمل **Load Hive** من الفولدر اللي فيه الـ Hive + Logs.

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 210858.png" alt="" width="563"><figcaption></figcaption></figure>

* الأداة أوتوماتيك هتعمل **Recovery** للـ Dirty Hive باستخدام الـ Logs.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 210549.png" alt="" width="563"><figcaption></figcaption></figure></div>

### ShellBags

#### التعريف

* **ShellBags** هي مجموعة من الـ **Registry Keys & Values** في الويندوز.
* وظيفتها إنها تخزن **إعدادات عرض الفولدرات** اللي اليوزر فتحها قبل كده (زي الـ view mode: icons, list, details).
* لكن في نفس الوقت، المعلومات دي بتكشف بشكل غير مباشر:
  * إيه الفولدرات اللي اتفتحت؟
  * إمتى اتفتحت آخر مرة؟

#### أماكن وجودها

* ShellBags بتتخزن في اتنين Hives:
  1. **NTUSER.DAT**
     * خاص باليوزر (User Profile).
     * بيخزن فولدرات اليوزر اللي فتحها.
  2. **USRCLASS.DAT**
     * خاص برضه باليوزر لكن بيركز أكتر على إعدادات الـ Explorer.

### ShellBags Explorer

* أداة تانية من أدوات **Eric Zimmerman**: **ShellBags Explorer**.
* موجوده يف نفس موقع وعايز بردو .net&#x20;

#### استخدام ShellBags Explorer

**steps**&#x20;

* **Load Offline Hive**
  * Open ShellBags Explorer.
  * Select **File → Load Offline Hive**.
  *   Choose a user hive like:

      * NTUSER.DAT
      * USRCLASS.DAT

      &#x20;              &#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 181813.png" alt="" width="341"><figcaption></figcaption></figure></div>

* **Analyze User Activity**
  *   The tool will display:

      * Folders the user opened.
      * Names of devices the user connected to (e.g., SMB shares, other PCs).
      * Directories browsed.
      * Search operations performed inside Windows Explorer.



<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 193022.png" alt="" width="563"><figcaption></figcaption></figure></div>

***

### 🔹 Regripper

### 📌 Overview

* RegRipper أداة قوية لتحليل الـ **Windows Registry**.
* متاحة على **Windows و Linux** كـ GUI وكمان كـ Command Line.
* بتنزل كـ **ZIP File** من GitHub → مجرد تعمل Download & Extract.

### 🛠️ Components

* **`rip.exe`** → Command Line version.
* **`rr.exe`** → GUI version.

### ⚙️ Usage

1. اختر الـ Registry Hive اللي عايز تحلله.
2. حدد مكان اللي هيكون فيه ال report&#x20;
3. اضغط **Rip**.

**after rip                                                                                            before rip**

<div><figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 194805.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 194837.png" alt=""><figcaption></figcaption></figure></div>

### 📊 Capabilities

* مش بس بتركز على **ShellBags**، لكنها بتحلل **أي Hive** بالكامل.
* مثال: عند تحليل **SYSTEM Hive**، ممكن تستخرج:
  * معلومات الـ **Startup Programs**.
  * بيانات الـ **Backup & Restore**.
  * قائمة بالـ **Installed Applications**.
  * **Timeline** لبعض الأحداث.

### 📄 Output

* ينتج ملف **Text Report (.txt)**.
* التقرير بيكون كبير ومليان تفاصيل.
* سهل البحث فيه بالكلمات المفتاحية.

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2025-09-10 194738.png" alt="" width="279"><figcaption></figcaption></figure></div>



## What we are looking for at analysis phase

### 🖥️ From SYSTEM Hive

1. **Computer Name**
2. **Time Zone**
3. **Network Interfaces**
4. **Connected Devices / Drivers**

***

### 👤 From NTUSER.DAT Hive

1. **Installed Software**
2. **Internet Explorer Data** _(قديمة شوية لكن ممكن تلاقيها)_
   * يحتوي على:
     * **TypedURLs** → العناوين اللي اليوزر كتبها يدويًا.
     * التبويبات المفتوحة.
3. **Recent Files (MRU - Most Recently Used)**
   * يوضح آخر ملفات اتفتحت
   * مع أسماء الملفات والـ Location بتاعها.
4.  **Run MRU (Commands)**

    recently commands used
5. **Mounted Devices**
   * يوضح الحاجات اللي  اتعملها Mount على الجهاز.

***

### Notes

* مش لازم تحفظ كل الـ Registry Paths
* الأماكن دي ممكن تختلف حسب نسخة الويندوز (Windows 7 / 10 / 11).
* كل الحاجات ديه ممكن تبها من خلالregistry explorer او من خلال regripper

***

## Important Directories in the Linux Filesystem



### 1. User & Temporary Directories

**/home**

ده المجلد الرئيسي اللي بيحتوي على المجلدات الخاصة بكل مستخدم على النظام. كل مستخدم بيكون له مجلد خاص بيه بيحمل اسمه، وجواه بيلاقي ملفاته الشخصية زي:

* Downloads
* Documents
* Desktop

> 📝 ملحوظة: نادراً جداً ما بيتم تغيير مكان الـ `/home` ده، لكنه ممكن تقنياً.

**/tmp**

ده مجلد الملفات المؤقتة (Temporary Files). أي ملفات بيتم إنشاؤها بشكل مؤقت بواسطة النظام أو البرامج بتتحط هنا. بيشتغل زي الـ "Cache" الخاص بالسيستم.

* محتواه بيتمسح: كل الملفات اللي جوه `/tmp` بتتحذف مع كل مرة بتعمل فيها ريستارت (Reboot) للـ سيستم.
* أهميته في التحليل: ممكن تلاقي فيه ملفات نزلها المستخدم بشكل مؤقت وتعرف منها معلومات عن نشاطه.

***

### 2. System & Binary Directories

**/bin**

اختصار لكلمة "Binaries". المجلد ده بيحتوي على الملفات التنفيذية (البرامج والأوامر) الأساسية اللي بيحتاجها النظام وكل المستخدمين عشان يشتغل، زي أوامر `ls`, `cp`, `cat`.

* أهميته: من خلال فحص محتويات المجلد ده، تقدر تعرف إيه هي الأدوات والبرامج الأساسية اللي تم تثبيتها أو عمل `compile` ليها على الجهاز.

**/etc**

ده يعتبر مركز التحكم بتاع النظام، شبيه بالـ "Registry" في ويندوز. بيحتوي على كل ملفات الإعدادات والـ Configuration الخاصة بالنظام والبرامج المثبتة. من خلاله تقدر تعرف:

* أسماء المستخدمين والجروبات: زي ملفات `passwd` و `group`.
* الخدمات (Services): إعدادات الخدمات الرئيسية زي `SSH`, `FTP`, وغيرها من السيرفرات اللي متسطبة.
* إعدادات الشبكة والنظام.

> 📝 ملحوظة: غالباً مسار `/etc` مش بيتغير لأنه أساسي لعمل النظام.

***

### 3. Devices & Recovered Files

**/media & /mnt**

المجلدين دول مخصصين لعملية الـ Mounting، وهي توصيل وحدات تخزين خارجية بالنظام عشان تقدر تتعامل معاها.

* `/media`: غالباً النظام بيستخدمه تلقائياً لما توصل فلاشة أو هارد ديسك خارجي.
* `/mnt`: عادةً بيستخدمه مدير النظام (System Admin) عشان يعمل Mount لوحدات تخزين بشكل يدوي.

**/lost+found**

ده مجلد خاص ومهم جداً لعملية استعادة الملفات. لو حصل أي خطأ في النظام (زي انقطاع مفاجئ للكهرباء) أثناء كتابة ملف على الهارد ديسك، نظام الملفات بيحاول يستعيد الأجزاء التالفة أو المفقودة من الملفات دي وبيحطها في مجلد `/lost+found`. بنسميها "Orphaned files" أو الملفات اليتيمة.

***

#### 4. Logging Directories

**/var**

المجلد ده بيحتوي على الملفات المتغيرة (Variable files)، يعني الملفات اللي حجمها ومحتواها بيتغير باستمرار أثناء تشغيل النظام. أهم حاجة جواه هو مجلد الـ Logs.

* `/var/log`: ده المكان الافتراضي اللي بيتخزن فيه معظم ملفات الـ "Logs" أو سجلات الأحداث بتاعة النظام والبرامج المختلفة. تحليل الملفات دي مهم جداً عشان تعرف إيه اللي حصل وبيحصل على السيستم.

***

#### Linux Flexibility

من المهم تعرف إن الهيكل اللي شرحناه ده هو الشكل الافتراضي في معظم توزيعات لينكس. لكن من قوة لينكس إنه نظام مرن جداً، والمستخدم المحترف يقدر يغير الأماكن دي:

* الـ Mount points: ممكن يختار أي مسار عشان يعمل Mount للأجهزة بتاعته.
* البرامج والـ Binaries: ممكن يحط البرامج بتاعته في أي مكان تاني غير `/bin` أو `/usr/bin`.
* الـ Logs: ممكن يغير مكان حفظ الـ Logs لمسار مختلف تماماً عن `/var/log`.



### Linux operating system analysis <a href="#linux-operating-system-analysis" id="linux-operating-system-analysis"></a>

#### Accessing the System for Investigation <a href="#accessing-the-system-for-investigation" id="accessing-the-system-for-investigation"></a>

* **المبدأ الأساسي:** في لينكس، **"كل شيء عبارة عن ملف"**.
* **طرق الحصول على البيانات:**
  1. **(Single User Mode):** يمكن استخدامه للوصول المباشر
  2. **استخدام Live CD** يُفضل استخدام توزيعة متخصصة مثل **SIFT**

#### User History and Commands <a href="#user-history-and-commands" id="user-history-and-commands"></a>

* **الأمر `history`:** يُستخدم لعرض الأوامر التي قام المستخدم الحالي بتنفيذها.
* **ملف `.bash_history`:** هو الملف الذي يتم فيه تخزين سجل الأوامر.
  * **المسار:** `/home/username/.bash_history`
  * يمكن فحص هذا الملف مباشرة للحصول على سجل كامل للأوامر التي تم تنفيذها بواسطة المستخدم.

**Environment Variables and Paths**

* **ملف `.bashrc`:**
  * **المسار:** `/home/username/.bashrc`
  * **الوظيفة:** يحتوي على أوامر وسكريبتات تعمل تلقائيًا عند تسجيل دخول المستخدم. يمكن أن يكشف عن مسارات مخصصة أو برامج يتم تشغيلها عند بدء الجلسة.
* **ملف `.profile`:**
  * **المسار:** `/home/username/.profile`
  * **الوظيفة:** يقوم بتحديد متغيرات البيئة والمسارات التي يستخدمها المستخدم، مما يعطي فكرة عن أماكن الملفات التنفيذية.

**User Information**

* **ملف `/etc/passwd`:**
  * **الوظيفة:** يحتوي على قائمة بجميع حسابات المستخدمين على النظام، بالإضافة إلى معلومات هامة مثل:
    * اسم المستخدم.
    * مسار المجلد الرئيسي (Home Directory).
    * الـ Shell الافتراضي.
* **تصفية المستخدمين:** يمكن استبعاد حسابات الخدمات والتركيز على المستخدمين الفعليين عن طريق البحث عن الحسابات التي لا تحتوي على `nologin` كـ shell افتراضي باستخدام أمر `grep`.

**System Logs**

* **الموقع الرئيسي:** أغلب سجلات النظام والخدمات موجودة داخل مجلد `/var/log`.
* **سجلات هامة للفحص:**
  * **Authentication Logs:** سجلات تسجيل الدخول والمصادقة.
  * **Kernel Logs:** سجلات نواة النظام.
  * **Service Logs:** سجلات الخدمات مثل Apache, Samba, Antivirus.
* **ملفات الإعدادات:** يمكن فحص إعدادات خدمة تسجيل السجلات (مثل `rsyslog` أو `syslog`) في مجلد `/etc/rsyslog.d/` لمعرفة أين يتم توجيه كل نوع من السجلات.

**Mounted File Systems**

* **ملف `/etc/mtab`:**
  * **الوظيفة:** يعرض قائمة بجميع أنظمة الملفات المُتصلة حاليًا بالنظام (Mounted) وإعداداتها، مما يساعد على فهم تقسيم القرص الصلب وأي وحدات تخزين متصلة.

**Scheduled Tasks (Cron Jobs)**

* **ملف `/etc/crontab`:**
  * **الوظيفة:** يحتوي على المهام المجدولة (Cron Jobs) التي تعمل تلقائيًا في أوقات محددة. فحص هذا الملف يمكن أن يكشف عن وجود سكربتات أو برامج ضارة تعمل في الخلفية.



حاضر، عدلتها زي ما طلبت بالظبط.

***

### Firefox Forensics on Linux&#x20;

***

#### 1. Locating the Profile Directory

الخطوة الأولى هي إننا نلاقي ال directory اللي Firefox بيخزن فيه كل بيانات المستخدم بما إن Firefox على Ubuntu بيتثبت عن طريق `snap`، فالمسار بتاعه بيكون هنا&#x20;

```
~/snap/firefox/common/.mozilla/firefox/
```

جوه الdirectory  ده، هتلاقي directory تاني باسم عشوائي (زي `f1quz1a9.default-release` مثلًا)، هو ده directory البروفايل الأساسي اللي فيه كل البيانات المهمة. أي مجلدات تانية زي `Crash Reports` مش بنحتاجها في عملية التحليل دي.

<figure><img src="../../.gitbook/assets/Screenshot 2025-09-13 151926.png" alt=""><figcaption></figcaption></figure>

***

#### 2. Key Artifact Files

جوه directory البروفايل، هتلاقي مجموعة من الملفات اللي بتنتهي با .**sqlite** دي عبارة عن قواعد بيانات مصغرة، وكل ملف مسؤول عن تخزين نوع معين من البيانات.

أهم الملفات دي هي:

* `places.sqlite`: ده أهم ملف فيهم كلهم، لأنه بيحتوي على:
  * سجل المواقع اللي زرتها (History).
  * المواقع المحفوظة في المفضلة (Bookmarks).
  * قائمة الملفات اللي نزلتها (Downloads).
* `cookies.sqlite`: الملف المسؤول عن تخزين كل الكوكيز اللي المواقع بتحفظها على جهازك.

***

#### 3. Practical Analysis Steps

بعد ما حددنا مكان الملفات المهمة، هنبدأ في خطوات التحليل الفعلية. ملحوظة هامة: قبل ما تبدأ، لازم تنسخ الملفات اللي هتحللها (زي `places.sqlite`) لمكان تاني (زي الديسكتوب مثلًا) عشان تشتغل على النسخة ومتبوظش الدليل الأصلي.

**Step 1: Copy the Database**

انسخ ملف `places.sqlite` من مسار البروفايل وحطه في مجلد جديد على الديسكتوب عشان تبدأ تحليله.

**Step 2: Use an SQLite Viewer**

عشان تفتح وتقرأ ملفات `.sqlite`، هتحتاج برنامج متخصص. ممكن تستخدم:

* DB Browser for SQLite: برنامج مجاني وممتاز للكمبيوتر.
* مواقع أونلاين: في مواقع بتسمحلك ترفع ملف قاعدة البيانات وتشوف محتوياته على طول.

**Step 3: Examine the Database Content**

1. افتح ملف `places.sqlite` اللي نسخته باستخدام البرنامج.
2. هتلاقي جواه  (Tables)، كل جدول بيحتوي على نوع معين من البيانات.
3. عشان تطلع history :
   * روح على جدول اسمه `moz_places`. الجدول ده فيه كل الروابط (URLs) اللي المستخدم زارها، ومعاها معلومات تانية زي عدد الزيارات وتاريخ آخر زيارة.
4.  عشان تطلع bookmarks:

    * هتلاقيها برضه موجودة ومترتبة جوه قاعدة البيانات دي، غالبًا في جدول `moz_bookmarks`.

