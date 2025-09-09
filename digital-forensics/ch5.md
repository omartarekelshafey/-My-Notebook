# CH5



***

### Introduction to Windows Registry

هنبدأ الأول بالـ Windows، وهنبدأ بأهم حاجة بتميز الـ Windows عن باقي أنظمة التشغيل وهي **الـ Registry**.\
الـ Registry بتكون متسجلة في ملفات بنسميها **Hive**، وهي اللي بتحتوي على معظم الـ Configuration والـ Cache الخاصة بالـ User أو بالـ Operating System.

***

### Accessing the Registry

* من قائمة Start في Windows نكتب `regedit` → ده هيفتح أداة اسمها **Registry Editor**.
* الـ Registry Editor هي Tool موجودة جوه الـ Windows بتسمحلك تعرض وتعدل على الـ Registry.

<div align="left"><figure><img src="../.gitbook/assets/image.png" alt="" width="375"><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Screenshot 2025-09-09 233312.png" alt="" width="270"><figcaption></figcaption></figure></div>

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

<figure><img src="../.gitbook/assets/Screenshot 2025-09-09 224442.png" alt=""><figcaption></figcaption></figure>

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



<div align="left"><figure><img src="../.gitbook/assets/Screenshot 2025-09-09 225411.png" alt="" width="467"><figcaption><p>manual method</p></figcaption></figure></div>



***

### Example with FTK Imager

اول من file  اختار**Obtain Protected Files**

<div align="left"><figure><img src="../.gitbook/assets/Screenshot 2025-09-09 225433.png" alt="" width="260"><figcaption></figcaption></figure></div>

* حدد مكان تحفظ فيه files
* بيظهرلك Option:
  * **Password recovery only**&#x20;
  * **Password recovery and all registry files**&#x20;

<div align="left"><figure><img src="../.gitbook/assets/image (1).png" alt="" width="306"><figcaption></figcaption></figure></div>

**result**

<figure><img src="../.gitbook/assets/Screenshot 2025-09-09 230135.png" alt=""><figcaption></figcaption></figure>

