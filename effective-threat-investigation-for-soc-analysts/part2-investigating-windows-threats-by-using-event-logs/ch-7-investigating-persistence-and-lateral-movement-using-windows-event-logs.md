# CH 7 Investigating Persistence and Lateral Movement Using Windows Event Logs

### مفهوم الـ Persistence

كلمة Persistence معناها إن المهاجم بيحاول يحافظ على وصوله للجهاز المخترق لأطول فترة ممكنة. التحدي اللي بيواجه أي "Malware" هو إن الجهاز لو عمل Reboot أو المستخدم عمل Log off، (Process) بتاعة الفيروس تقف. عشان كده المهاجم بيلجأ لطرق تخلي الفيروس يشتغل "أوتوماتيكياً" مع كل بداية للسيستم.

***

### تقنية الـ Registry Run Keys

الـ Windows Registry ده عبارة عن قاعدة بيانات ضخمة فيها كل إعدادات الويندوز والبرامج. المهاجمين بيستغلوا أماكن معينة فيه اسمها Run Keys، أي حاجة بتتحط جواها، الويندوز بيشغلها فوراً أول ما المستخدم يسجل دخول.

#### أهم الأماكن (Hives) اللي الattacker بيبص عليها:

1. قيمة HKEY\_CURRENT\_USER (HKCU): دي إعدادات خاصة بالمستخدم اللي فاتح دلوقتي بس.
2. قيمة HKEY\_LOCAL\_MACHINE (HKLM): دي إعدادات عامة للجهاز كله، وأي حد يفتح الجهاز الفيروس هيشتغل عنده (بتحتاج صلاحيات Admin).

#### مسارات الـ Run Keys الشهيرة:

* `...\Microsoft\Windows\CurrentVersion\Run`: البرنامج بيشتغل "كل مرة" الويندوز يفتح فيها.
* `...\Microsoft\Windows\CurrentVersion\RunOnce`: البرنامج بيشتغل "مرة واحدة بس"

| **(Event ID)** | **(Event Name)**                        | **الشرح بالعربي (مبسط)**                                                                                                      |
| -------------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 4656           | A handle to an object was requested     | ده معناه إن فيه برنامج أو مستخدم طلب "إذن" عشان يفتح أوبجكت معين (زي مفتاح ريجستري). دي أول خطوة في التعامل مع أي حاجة.       |
| 4657           | A registry value was modified           | ده أهم واحد للـ Persistence، معناه إن فيه قيمة جوه الريجستري اتغيرت فعلياً (تعديل، إضافة، أو مسح قيمة).                       |
| 4658           | The handle to an object was closed      | ده بيظهر لما البرنامج يخلص شغله مع الأوبجكت ويقفله. بيفيد في معرفة "مدة" الوصول كانت قد إيه.                                  |
| 4660           | An object was deleted                   | ده بيسجل لحظة مسح الأوبجكت تماماً. لو مهاجم حاول يمسح أثر لمفتاح ريجستري خبيث، الحدث ده بيكشفه.                               |
| 4663           | An attempt was made to access an object | ده بيسجل "المحاولة الفعلية" لاستخدام الأوبجكت بعد ما الـ Handle اتفتح. بيعرفك هل المهاجم قرأ البيانات بس ولا حاول يكتب ويعدل. |

#### تحليل الحدث 4656

الصورة بتشرح إن الحدث ده متقسم لـ 4 أجزاء رئيسية، وكل جزء بيكمل الصورة عشان تفهم الهجمة ماشية إزاي:

#### (Subject)

* المهم فيه: بيعرفك "مين" اليوزر اللي نفذ العملية.
* الموجود في الصورة: اليوزر اسمه `pgustavo`. ده الحساب اللي المهاجم مسيطر عليه أو بيستخدمه.

#### (Object)

* المهم فيه: بيعرفك إيه "الهدف" اللي اليوزر بيحاول يفتحه.
* Object Type: هنا مكتوب Key، وده بيأكد إن التعامل مع الـ Registry.
* Object Name: ده أهم حتة، لأنه بيكشف المسار: `\REGISTRY\MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`.
* الاستنتاج: ده واحد من مسارات الـ Persistence المشهورة اللي اتكلمنا عنها.

#### (Process Information)

* المهم فيه: بيعرفك "الأداة" أو البرنامج اللي استخدمه اليوزر للوصول للريجستري.
* الموجود في الصورة: المسار هو `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`.
* الاستنتاج: استخدام PowerShell للوصول لمفاتيح التشغيل (Run Keys) هو سلوك مشبوه جداً (Abnormal Access)، لأن البرامج العادية مش بتحتاج الباور شيل عشان تشتغل.

#### (Access Request Information)

* المهم فيه: بيعرفك الصلاحيات المطلوبة (زي القراءة أو الاستعلام).
* ملاحظة الكتاب: الجزء ده غالباً مش بيكون مفيد أوي في التحقيق السريع مقارنة بالأجزاء اللي فاتت.

***

#### (Investigative Notes)

1. قيمة الحدث 4656: بالرغم إنه مش بيقولك إيه "اسم الفيروس" اللي اتضاف، لكنه بيعرفك التكنيك (Technique) اللي المهاجم استخدمه عشان يثبت نفسه في الجهاز.
2. أهمية التوقيت: كـ SOC Analyst، لازم تراقب لو حصل وصول للريجستري من أدوات زي `CMD` أو `PowerShell` في أوقات غريبة (بره ساعات العمل).
3. الحدث 4657 (تعديل القيمة): ده اللي بيدينا التفاصيل "السمينة" (اسم ملف الفيروس ومساره)، بس محتاج يتفعل يدوي عن طريق الـ SACL لأنه مش شغال بالـ Default.

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

### &#x20;الـ Scheduled Tasks

الـ Scheduled Tasks دي وظيفة في ويندوز بتسمح للمستخدم (أو المهاجم) إنه يخلي الجهاز ينفذ "أمر" أو يشغل "برنامج" بشكل تلقائي في وقت محدد أو لما حاجة معينة تحصل (زي لما تعمل Log in).

#### How  to create a Scheduled Tasks

ممكن من خلال  (GUI)، او  (Command Line) عشان السرعة والـ Automation. من خلال  `schtasks.exe`.

مثال على malicious command  (استخدمته مجموعة APT3):

Bash

```
schtasks /create /tn mysc /tr C:\Users\Public\test.exe /sc ONLOGON /ru System
```

* الوصف: الأمر ده بيكريت تاسك اسمها `mysc` بتشغل ملف `test.exe` كل ما حد يعمل Login، والخطير هنا إنها بتشتغل بصلاحيات الـ System (أعلى صلاحيات في الجهاز).

***

### &#x20;الـ Windows Event Logs

لما الattacker  بيعمل Task جديدة، الويندوز بيسجل ده في الـ Security Log&#x20;

#### &#x20;Event ID 4698

الـ Event ده معناه: "A scheduled task was created"

**تحليل محتوى الـ Event (زي ما في الصور):**

الحدث ده متقسم لجزئين أساسيين لازم تفحصهم كـ SOC Analyst:

1. قسم الفاعل (Subject): بيقولك "مين" اليوزر اللي كرت التاسك دي (في المثال كان `pgustavo`).
2. قسم معلومات المهمة (Task Information): وده الدسم كله، وبيبقى مكتوب بصيغة XML:
   * Task Name: اسم المهمة (في المثال: `MordorSchtask`).
   * Triggers: "امتى" المهمة هتشتغل (في المثال: كل يوم الساعة 9 الصبح).
   * Actions: "إيه" اللي هيتنفذ بالظبط (وده أخطر جزء).

### حالة عملية (Case Study) من الكتاب:

في المثال اللي في الصور، المهاجم عمل حاجة ذكية جداً (Suspicious Behavior):

* الـ Action: خلى المهمة تشغل PowerShell.
* الأمر: الأمر كان طويل ومشفر (Encoded) بـ Base64، وبيروح يقرأ كود مخفي جوه الـ Registry.
* النوع: ده بنسميه Fileless Attack، لأن الكود الخبيث مش موجود في ملف `.exe` على الهارد، ده مستخبي في الريجستري والباور شيل بيقرأه ويشغله في الرامات فوراً.

<div align="left"><figure><img src="../../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure></div>

<div align="left"><figure><img src="../../.gitbook/assets/image (12).png" alt="" width="563"><figcaption></figcaption></figure></div>

### الـ Windows services

الـ Service هي (Process) بتشتغل في الخلفية، والمهاجمين بيستغلوها عن طريق إنشاء New service أو تعديل Existing service عشان تشغل الكود الخبيث بتاعهم.

#### create service&#x20;

الattacker  بيستخدم  `sc.exe` (اختصار لـ Service Control).

```
sc.exe create TestService binpath= c:\windows\temp\NewServ.exe start= auto
```

* binpath: ده المسار اللي فيه الملف الخبيث اللي الخدمة هتشغله.
* start= auto: دي أهم حتة للمهاجم، معناها إن الخدمة هتشتغل لوحدها أول ما الجهاز يفتح (Auto-start).

***

### &#x20;Event Logs

#### 1. الـ Security Log (الحدث 4697)

اسمه A service was installed in the system. ده بيظهر في سجل الأمان وبيتقسم لجزئين:

* قسم الـ Subject: بيقولك "مين" المستخدم اللي عمل الـ Service.
* قسم الـ Service Information:&#x20;
  * Service Name
  * Service File Name.
  * ال Service Start Type: بياخد أرقام بتعرفك الservice  هتشتغل إمتى.
  * ال Service Account: الحساب اللي الservice  هتاخد صلاحياته&#x20;

#### 2. الـ System Log (الحدث 7045)

ده برضه اسمه A service was installed in the system بس بيتسجل في الـ System log. الفرق إنه مش بيكتب مين اليوزر اللي عمل كده في قسم منفصل، بس بيديك نفس تفاصيل الـ Service Information اللي في الحدث 4697.

***

### معاني أرقام الـ Start Type

في الـ Logs، نوع البداية بيظهر كرقم، والمهاجم بيركز دايماً على رقم 2:

* 0 (Boot): بتشتغل مع الـ Drivers الأساسية للويندوز.
* 1 (System): بتشتغل عن طريق الـ I/O subsystem.
* 2 (Auto Start): دي اللي المهاجم بيستخدمها عشان يضمن الـ Persistence.
* 3 (Manual): بتشتغل يدوي بس.
* 4 (Disabled): الخدمة معطلة.
