# CH 5 Investigating Suspicious Process Execution Using   Windows Event Logs

## Introduction to Windows Processes

نظام التشغيل Windows بيعتمد بشكل أساسي على العمليات (Processes) عشان يشغل البرامج والمهام اللي في الخلفية. كل عملية (Process) بيكون ليها مساحة مخصصة في الذاكرة (Memory) وموارد خاصة بيها. أي نشاط بيحصل في بيئة Windows زي تسجيل الدخول، أو الوصول للملفات، أو تشغيل مكتبات الربط الديناميكي (DLLs)، دايماً بيكون مرتبط بـ Process معين.

**Tools to View Processes**

تقدر تتابع وتشوف الـ Processes اللي شغالة على الجهاز بتاعك باستخدام طريقتين أساسيتين:

* ال (GUI)باستخدام Task Manager
* او  (Command-line) اللي بتعرضلك الprocess  في cmd بتكتب الcommand ده&#x20;

```
tasklist
```

**Windows Process Attributes**

كل Process في الويندوز بيكون ليه مجموعة من (Attributes)

1. ال (Process Name): ده بيعبر عن اسم البرنامج أو الملف التنفيذي اللي شغال في الخلفية.
2. ال (Process ID): ده عبارة عن رقم تعريفي مميز وديناميكي (Dynamic Identifier) لكل Process شغال في النظام.
3. ال (Process Path): ده بيشير لمكان وجود ملف الـ Process على الهارد ديسك واللي اتعمل منه التنفيذ.
4. ال (Username): ده بيحدد الـ Context أو المستخدم اللي الـ Process شغال تحته، وده بيساعد في تحديد الصلاحيات الأمنية (Security Privileges) للعملية دي.
5. ال  (Command-line Argument): دي(Arguments)   اللي بتوجه الـ Process وتقوله ينفذ إيه بالظبط.
6. ال  (Parent Process): دي العملية الأساسية اللي قامت ب (Spawning) الـ Process الحالي.

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="506"><figcaption></figcaption></figure>

## Windows process types

&#x20;بنقسم الprocess  لنوعين أساسيين:

* &#x20;Standard Windows processes
* &#x20;Non-standard Windows processes



1. ال  (Standard Windows processes): دي عبارة عن الprocess اللي طورتها شركة مايكروسوفت، وبتكون موجودة أساساً في بيئة الويندوز عشان تدير عمليات نظام التشغيل (OS operations) زي الإقلاع (Boot)، وتسجيل الدخول (Login)، والخدمات (Services).
2. ال (Non-standard Windows processes): دي بقى الprocess اللي مش من تطوير مايكروسوفت، ومش بتنزل مع التثبيت الافتراضي (Default installation) للنسخة. العمليات دي ممكن تكون سليمة وشرعية (Legitimate) زي البرامج اللي بتعملها الشركات لاستخدامها الداخلي (Custom in-house software)مثلا زي google chrome  وممكن تكون خبيثة (Malicious)

### Common standard Windows processes

#### 1. System Process&#x20;

العملية دي هي Kernel-mode process المسؤولة عن الـ Threads اللي بتشتغل في الـ Kernel mode.

* (Process name): System
* &#x20;(Process path): N/A
* (Username): SYSTEM
* (Number of instances): One
* &#x20;(Parent process): N/A

#### 2. Understanding Threads in System Process

* &#x20;الـ System Threads: هي عبارة عن Execution units بتشتغل بالكامل جوه الـ Kernel mode، ومش محتاجة User-mode context عشان تتنفذ.
* وظيفة الـ Threads: بتعمل Executing لمهام زي الـ Memory management، والـ Disk I/O operations



#### 1. The Windows Session

الـ Session هي  اللي بتضم كل حاجة تخص مستخدم معين لما بيعمل Logon.

* مكونات الـ Session: بتشمل الـ Processes، والـ Windows Stations، والـ Desktops.
* الـ Memory: كل User بيكون ليه مساحة خاصة في الـ Virtual memory اسمها Session space.
* أنواع الـ Sessions:
  * Session 0: مخصصة للـ Services فقط (في الإصدارات الجديدة زي Vista وطالع).
  * Session 1 & Higher: مخصصة للـ Interactive users.

***

#### 2. Windows Stations

الـ Windows Station هي عبارة عن Security boundary (حدود أمنية) وظيفتها إنها تحوي الـ Desktops والـ Processes.

* الـ Winsta0: دي هي الـ Windows station الوحيدة اللي مسموح ليها تتفاعل مع المستخدم (Interactive).
* الـ Non-interactive Stations: زي اللي بتشتغل تحتها الـ Services (مثلاً `Service-0x0-3e7$`).
* الـ Flexibility: الـ Session الواحدة ممكن يكون فيها أكتر من Windows Station.

***

#### 3. Desktops

الـ Desktop هو المكان اللي بتترسم فيه الـ GUI objects (النوافذ، القوائم، وغيرها).

* الـ Winsta0 Desktops: تحت الـ Interactive station دي فيه 3 أنواع من الـ Desktops:
  1. Default: ده اللي بتشوف فيه الأيقونات والبرامج بتاعتك.
  2. Winlogon: شاشة تسجيل الدخول.
  3. Disconnect: بيستخدم في حالات معينة لما بتفصل الجلسة.



بص يا عمر، الـ smss.exe ده هو "المهندس الاستشاري" اللي بيخطط العمارة (الـ Sessions) ويشرف على بنائها. بعد ما فهمنا يعني إيه Session وعزل، تعال نشوف العملية دي بتتم إزاي بالتفصيل حسب المرجع اللي معاك:

#### Session Manager (smss.exe) process

الـ smss.exe هو أول User-mode process بيشتغل في النظام، وهو حلقة الوصل بين الـ Kernel وبين واجهة المستخدم اللي بنشوفها.

#### 1. The Master Instance vs. Session Instances

العملية دي مش بتشتغل بنسخة واحدة طول الوقت، لكن ليها نظام معين:

* The Master Instance: دي أول نسخة بتتعمل، والـ Parent process بتاعها هو الـ System. مهمتها الأساسية إنها تعمل Creating new sessions في نظام التشغيل.
* New Instances: لكل Session جديدة بتتعمل، الـ Master instance بتعمل Creating لنسخة جديدة من smss.exe مخصصة للجلسة دي عشان تجهزها.

#### 2. How it Builds Sessions (The Workflow)

بمجرد ما الـ smss.exe تبدأ تجهز Session، بتمشي في خطوات محددة جداً حسب نوع الجلسة:

* For Session 0:
  1. بتبدأ الأول بتشغيل الـ csrss.exe عشان يدير الـ Processes and threads.
  2. بعدها بتشغل الـ wininit.exe، وده المسؤول "الكبير" عن الـ Windows services في الجلسة دي.
* For Session 1 and higher:
  1. برضه بتشغل الـ csrss.exe الخاص بالجلسة دي.
  2. لكن هنا بتشغل الـ winlogon.exe بدل `wininit` عشان ده اللي بيتعامل مع الـ Users logging in والـ Interactive UI.

***

#### 3. smss.exe Attributes Table

Process name: smss.exe\
• Process path: %Systemroot%\System32\smss.exe\
• Username: SYSTEM\
• Number of instances: One for the master instance plus one for each new session creation\
• Parent process: System

#### Client Server Runtime Subsystem (csrss.exe)

الـ csrss.exe هو المسؤول عن الـ User-mode side للـ Windows subsystem.

* الوظيفة (Functionality): بيتم عمل Created لنسخة من الـ csrss.exe مع كل New session عشان تعمل Manage للـ Processes and threads وتعمل Import للـ DLLs اللي بتوفر الـ Windows API.
* خصائص العملية (Process Attributes):
  * اسم العملية (Process Name): csrss.exe.
  * مسار العملية (Process Path): `%Systemroot%\System32\csrss.exe`.
  * اسم المستخدم (Username): SYSTEM.
  * عدد النسخ (Number of instances): نسخة واحدة لكل Session (يعني هتلاقي واحدة للـ Session 0 وواحدة لجلسة المستخدم).
  * العملية الأب (Parent process): N/A؛ رغم إن الـ smss.exe instance هي اللي بتعمله Created، بس مش بيظهر كـ Parent في أي Analysis tool.

***

#### Windows Initialization (wininit.exe)

العملية دي هي اللي بتبدأ أهم العمليات الأمنية والخدمية في النظام.

* ال(Functionality): الـ wininit.exe بتمثل الـ Session 0 وهي المسؤولة عن عمل Initializing لكل من الـ Service Control Manager (services.exe) والـ Local Security Authority process (lsass.exe).
* (Process Attributes):
  * &#x20;(Process name): wininit.exe.
  * &#x20;(Process path): `%Systemroot%\System32\wininit.exe`.
  * &#x20;(Username): SYSTEM.
  * &#x20;(Number of instances): One
  * ال  (Parent process): N/A؛ برضه الـ smss.exe هي اللي بتعمله Created بس مش بيظهر كـ Parent.

#### Service Control Manager (services.exe)

الprocess  هي مسئولة عن كل  الـ Services والـ Drivers في الويندوز. هي اللي بتقرر مين يشتغل ومين يقف.

* ال (Functionality): الـ Service Control Manager (SCM) هو الـ Process المسؤول عن عمل Loading and launching لكل الـ Windows services والـ Drivers.
*   (Process Attributes):

    * &#x20;(Process name): services.exe.
    * &#x20;(Process path): `%Systemroot%\System32\services.exe`.
    * &#x20;(Username): SYSTEM.
    * &#x20;(Number of instances): One&#x20;
    * &#x20;(Parent process): wininit.exe.



#### Dynamic Link Library (DLL) and svchost.exe

الـ DLL هي السر وراء وجود نسخ كتير من الـ svchost.exe في الـ Task Manager.

#### 1. What is a DLL?

الـ DLL هي اختصار لـ Dynamic Link Library، وهي عبارة عن ملف بيحتوي على Code and Data تقدر أكتر من Application تستخدمهم في نفس الوقت:

* ال Shared Resources: بدل ما كل برنامج يكتب الكود بتاعه من الصفر، الويندوز بيحط الوظائف المشتركة في ملفات DLL عشان الكل ينده عليها.
* ال Not Executable: ملفات الـ DLL مش بتقدر تشتغل لوحدها زي ملفات الـ `.exe`؛ هي محتاجة Host process يشغلها ويحملها في الـ Memory.
* ال Efficiency: الطريقة دي بتوفر مساحة كبيرة في الـ RAM والـ Hard disk لأن الكود بيتم تحميله مرة واحدة بس وتشاركه بين البرامج.

***

#### 2. Why svchost.exe Hosts DLLs?

بما إن كتير من الـ Windows services مكتوبة كـ DLL files، الويندوز عمل الـ svchost.exe عشان يكون هو الـ Shell أو الـ Container اللي بيحتوي الملفات دي:

* الـ svchost.exe هو الـ Process المسؤول عن عمل Running and hosting للـ Service DLLs.
* Grouping with "-k": عشان النظام ميبقاش زحمة، الـ svchost.exe بيستخدم Unique "-k" parameter عشان يجمع الـ Similar services  في نسخة واحدة. مثلاً، خدمات الشبكة كلها ممكن تتجمع في Instance واحدة من الـ svchost.exe.

***

#### 3. svchost.exe Process Attributes

* &#x20;(Process name): svchost.exe.
* &#x20;(Process path): `%Systemroot%\System32\svchost.exe`.
* &#x20;(Username): SYSTEM, LOCAL SERVICE, أو NETWORK SERVICE.
* &#x20;(Number of instances): Many.
* &#x20;(Parent process): services.exe.

#### Runtime Broker (RuntimeBroker.exe)

* ال (Functionality): الـ Process ده بيساعد في عمل Manage permissions للتطبيقات اللي جاية من الـ Microsoft Store، وببيشتغل كـ Proxy بين الـ Windows Universal apps وبين إعدادات الـ Privacy/Security.
* &#x20;(Process Attributes):
  * &#x20;(Process name): RuntimeBroker.exe.
  * &#x20;(Process path): `%Systemroot%\System32\RuntimeBroker.exe`.
  * &#x20;(Username): The logged-in user.
  * (Number of instances): One or more.
  * &#x20;(Parent process): svchost.exe.

#### Local Security Authentication Service (lsass.exe)

الprocess ديه هي المسؤول الأول عن التحقق من هوية المستخدم.

* الـ lsass.exe مسؤول عن Authenticating users سواء مقابل الـ Domain controller لحسابات الـ Domain، أو مقابل الـ SAM table للحسابات الـ Local.
* &#x20;هو المسؤول عن تطبيق الـ Security policy وحفظ الـ Authentication credentials في الـ Memory section الخاص بيه. ده بيخليه Prime target للمهاجمين اللي بيحاولوا يسرقوا الـ Login credentials.
* (Process Attributes)
  * (Process name): lsass.exe.
  * &#x20;(Process path): `%Systemroot%\System32\lsass.exe`.
  * &#x20;(Username): SYSTEM.
  * &#x20;(Number of instances): One&#x20;
  * &#x20;(Parent process): wininit.exe.

***

**Windows Logon (winlogon.exe)**

الprocess دي هي اللي بتدير عملية دخول وخروج المستخدمين من الـ Interactive session.

* ال  (Functionality): بتتعامل مع الـ Interactive user logins and logouts. هي المسؤولة عن تشغيل الـ LogonUI.exe عشان تستلم الـ Credentials من المستخدم، وبعدين بتبعتها للـ lsass.exe عشان يعمل ليها Validation.
* (Process Attributes):
  * &#x20;(Process name): winlogon.exe.
  * &#x20;(Process path): `%Systemroot%\System32\winlogon.exe`.
  * (Username): SYSTEM.
  * (Number of instances): One for each interactive user login.
  * ال  (Parent process): N/A (بيتم عمل Created ليها بواسطة الـ smss.exe بس مش بتظهر كـ Parent).

***

**Logon User Interface (LogonUI.exe)**

دي gui  اللي بتشوفها لما بتيجي تكتب الباسورد.

* الوظيفة (Functionality): مسؤولة عن الـ User interface لشاشة الـ Login. لما بتكتب بياناتك، هي اللي بتبعتها للـ winlogon.exe أو الـ lsass.exe عشان تكمل عملية الـ Authentication.
* (Process Attributes):
  * &#x20;(Process name): LogonUI.exe.
  * &#x20;(Process path): `%Systemroot%\System32\LogonUI.exe`.
  * &#x20;(Username): SYSTEM.
  * &#x20;(Number of instances): One or more.
  * &#x20;(Parent process): winlogon.exe.

***

**Windows Explorer (explorer.exe)**

ده اللي المستخدم بيتعامل معاه بعد ما بيعمل Login.

* ال (Functionality): مسؤول عن توفير الـ User interface للـ Desktop، والـ Taskbar، والـ File manager. هو اللي بيخليك توصل للملفات والـ Applications.
* (Process Attributes):
  * &#x20;(Process name): explorer.exe.
  * (Process path): `%Systemroot%\explorer.exe` (لاحظ إنه مش في `System32`).
  * &#x20;(Username): The logged-in user.
  * (Number of instances): One for each interactive user login.
  * ال(Parent Process): N/A (بيكون Orphaned بعد ما الـ Userinit.exe اللي شغله يقفل).

<table data-header-hidden data-full-width="false"><thead><tr><th width="168.79998779296875"></th><th width="160.79998779296875"></th><th width="309"></th><th width="172"></th><th></th></tr></thead><tbody><tr><td> <strong>Process Name</strong></td><td> <strong>Parent Process</strong></td><td><strong>process path</strong> </td><td> <strong>Username</strong></td><td> <strong>Instances</strong></td></tr><tr><td>System</td><td>N/A</td><td>N/A</td><td>SYSTEM</td><td>One</td></tr><tr><td>smss.exe</td><td>System</td><td><code>%Systemroot%\System32\smss.exe</code></td><td>SYSTEM</td><td>One (Master)</td></tr><tr><td>csrss.exe</td><td>N/A (Created by smss.exe)</td><td><code>%Systemroot%\System32\csrss.exe</code></td><td>SYSTEM</td><td>One per Session</td></tr><tr><td>wininit.exe</td><td>N/A (Created by smss.exe)</td><td><code>%Systemroot%\System32\wininit.exe</code></td><td>SYSTEM</td><td>One</td></tr><tr><td>services.exe</td><td>wininit.exe</td><td><code>%Systemroot%\System32\services.exe</code></td><td>SYSTEM</td><td>One</td></tr><tr><td>svchost.exe</td><td>services.exe</td><td><code>%Systemroot%\System32\svchost.exe</code></td><td>SYSTEM, LOCAL/NETWORK SERVICE</td><td>Many</td></tr><tr><td>lsass.exe</td><td>wininit.exe</td><td><code>%Systemroot%\System32\lsass.exe</code></td><td>SYSTEM</td><td>One</td></tr><tr><td>winlogon.exe</td><td>N/A (Created by smss.exe)</td><td><code>%Systemroot%\System32\winlogon.exe</code></td><td>SYSTEM</td><td>One per User Login</td></tr><tr><td>LogonUI.exe</td><td>winlogon.exe</td><td><code>%Systemroot%\System32\LogonUI.exe</code></td><td>SYSTEM</td><td>One or More</td></tr><tr><td>explorer.exe</td><td>N/A</td><td><code>%Systemroot%\explorer.exe</code></td><td>Logged-in User</td><td>One per User Login</td></tr><tr><td>RuntimeBroker.exe</td><td>svchost.exe</td><td><code>%Systemroot%\System32\RuntimeBroker.exe</code></td><td>Logged-in User</td><td>One or More</td></tr></tbody></table>

## Windows Process Tracking events

نظام الويندوز بيسمح لك تتبع كل process بيتم إنشاؤها أو إنهاؤها من خلال تسجيل Event IDs محددة في ملف الـ Security event log.&#x20;

#### 1. Key Process Tracking Events

عندنا نوعين أساسيين من الـ Events بنراقبهم:

* الـ Event ID 4688: بيسجل  (Process creation activity).
* ال Event ID 4689: بيسجل (Process exit activity)

***

### 2. Analysis of Event ID 4688

الـ Event 4688 بعنوان "A new process has been created"الـ Event ده متقسم لـ 3 أقسام رئيسية:

1. Creator Subject
2. &#x20;Target Subject
3. &#x20;Process Information
   * New Process ID
   * &#x20;New Process Name
   * &#x20;Creator Process ID
   * &#x20;Creator Process Name

<div align="left"><figure><img src="../../.gitbook/assets/image.png" alt="" width="563"><figcaption></figcaption></figure></div>

#### 1. Creator Subject Section

القسم ده بيقدم معلومات عن الـ User والـ Login session اللي بدأ تشغيل الـ New process.

* ال Parent Owner: بيوضح برضه مين هو الـ Owner بتاع الـ Parent process اللي عمل Created للعملية الجديدة.

#### 2. Target Subject Section

القسم ده مخصص للمعلومات المتعلقة بالـ User اللي بيملك الـ Newly created process.

* ال Process Context: بيعرفك الـ Context اللي العملية شغالة تحته، والـ Login session المرتبطة بيها.
* ال Empty Fields Case: لو الـ Owner بتاع العملية الجديدة هو نفسه المستخدم اللي بدأها (يعني نفس بيانات الـ Creator Subject)، الحقول في القسم ده هتكون Empty

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



#### Process Information Section (Event ID 4688)

القسم ده هو أهم جزء في الـ Event لاكتشاف وتحليل أي نشاط مشبوه، لأنه بيربط العملية الجديدة بأصلها وصلاحياتها. إليك شرح كل الحقول اللي فيه:

* ال New Process ID: ده الرقم التعريفي للعملية الجديدة، وبيستخدم لتتبع نشاطها وربطها بـ Events تانية ليها نفس الـ ID.
* ال New Process Name: بيعرض اسم العملية والمسار الكامل للملف اللي اشتغل (Full Path)، وده أساسي لكشف العمليات اللي شغالة من أماكن مشبوهة.
* ال Token Elevation Type: بيحدد الصلاحيات اللي الـ UAC اداها لprocess، وليه 3 قيم أساسية:
  * ال %%1936 (Type 1): هو Full Token بيحتوي على كل الصلاحيات بدون تعديل، وبيستخدم لو الـ UAC مقفول أو للحسابات النظامية (SYSTEM/Administrator).
  * ال %%1937 (Type 2): هو Elevated Token بيحتوي على كل الصلاحيات، وبيظهر لما المستخدم يختار Run as Administrator والـ UAC شغال.
  * ال %%1938 (Type 3): هو Limited Token بصلاحيات محدودة، وبيستخدم لما يكون الـ UAC شغال والبرنامج مش محتاج صلاحيات أدمن.

بص يا عمر، الجدول ده فيه الخلاصة لكل رتب الأمان (Integrity Levels) اللي في الصور، مع شرح مبسط لكل رتبة عشان تبقى فاهمها وأنت بتحلل أي Log:

#### جدول مستويات النزاهة (Mandatory Label)

| **(RID Label)** | **(SID)**    | **(RID)**    | **(Meaning)**    | explain                                                                |
| --------------- | ------------ | ------------ | ---------------- | ---------------------------------------------------------------------- |
| Untrusted       | S-1-16-0     | `0x00000000` | Untrusted        |  دي أقل حاجة وملهاش أي صلاحيات.                                        |
| Low             | S-1-16-4096  | `0x00001000` | Low integrity    |  بتعطى للمتصفحات عشان لو جالك فيروس يفضل محبوس جواها وما يلمسش ملفاتك. |
| Medium          | S-1-16-8192  | `0x00002000` | Medium integrity |  دي لأغلب البرامج اللي بتفتحها عادي زي الـ Word.                       |
| Medium Plus     | S-1-16-8448  | `0x00002100` | Medium/high      |  درجة أعلى شوية من العادي                                              |
| High            | S-1-16-12288 | `0X00003000` | High integrity   | ر دي لما تعمل Run as Administrator، وبتقدر تعدل في ملفات النظام.       |
| System          | S-1-16-16384 | `0x00004000` | System integrity |  لعمليات الويندوز والخدمات الأساسية اللي بتدير الجهاز.                 |
| Protected       | S-1-16-20480 | `0x00005000` | Protected        |  عمليات محمية جداً ومخصصة لحماية حقوق الملكية أو ملفات حساسة جداً.     |

* يعني إيه SID؟
  * هو اختصار لـ Security Identifier، وده "الرقم القومي" الطويل اللي الويندوز بيستخدمه عشان يميز   مستخدم  او process بشكل فريد.
* يعني إيه RID؟
  * هو اختصار لـ Relative Identifier، وده الجزء الأخير من الـ SID (زي 4096 أو 8192) وبيعبر عن مستوي permission اللي علي يوزر او ال process&#x20;

كده الجدول جاهز معاك، تحب نطبق ده على الـ Log اللي في الصورة الأولى ونشوف الـ `RuntimeBroker.exe` كان واخد رتبة إيه؟

* ال Creator Process ID: هو الـ PID بتاع  (Parent Process)، وبيساعد في تتبع  (Process Tree).
* ال Creator Process Name: المسار الكامل ل(Parent Process)، وده بيساعد في  (Anomalous patterns).
* ال Process Command Line: بيعرض الأوامر والمفاتيح اللي استخدمت لتشغيل الprocess  الحقل ده مهم جداً لفهم غرض الprocess  وكشف المهاجمين اللي بيستخدموا أدوات زي `cmd.exe` أو `powershell.exe` بأوامر خبيثة.
  * ملحوظة: الحقل ده مش مفعل تلقائياً، لازم تفعله من الـ Group Policy تحت مسار `Audit Process Creation | Include command line`.

#### 💡 User Account Control (UAC)&#x20;

الـ UAC هو ميزة أمنية بتحمي النظام من التعديلات غير المصرح بها، وبمجرد ما process تطلب صلاحيات Administrator، الـ UAC بينبهك عشان توافق أو ترفض. هو دهاللي بيحدد قيم الـ Token Elevation Type والـ Mandatory Label اللي بنشوفها فوق.

### **Windows Process Exit Tracking (Event ID 4689)**

#### 1. Sections of Event ID 4689

الـ Event ده بيتكون من قسمين أساسيين:

* ال Subject Section: بيقدم معلومات عن الـ Login session والمستخدم (User) اللي كانت العملية شغالة تحت الـ Context بتاعه.
* ال Process Information Section: بيحتوي على بيانات العملية اللي قفلت زي الـ Process ID، والـ Process Name، والـ Full path بتاعها

#### 2. Tracking Process Execution Time

أهم فايدة للـ Event 4689 هي إننا نقدر نحسب "مدة تشغيل العملية" عن طريق ربطها بالـ Event 4688:

* Correlation: بنستخدم الـ Process ID المشترك بين الـ Event 4688 (لحظة البداية) والـ Event 4689 (لحظة النهاية).

## Investigating suspicious process executions



### Hiding in plain sight

فكرة الـ Technique ده بتعتمد إن الـ Attacker بيسمي الـ Malware بتاعه بأسماء مشابهة جداً للـ Standard Windows processes المعروفة.

* أمثلة على كده استخدام أسماء زي `Svch0st.exe`، `scvhost.exe`، أو `lssas.exe`.
* طريقة تانية بيعملها الـ Attacker هي إنه يستخدم نفس اسم الـ Windows process بالظبط، بس يعمل ليه Save و Load من Windows path مختلف عن المسار بتاع الـ Legitimate process الأصلية.
* الهدف من الـ Techniques دي إن الـ Attackers يعملوا Hide in plain sight ويقدروا يعملوا Evade detection efforts.

### Detecting Suspicious Process Executions

عشان نقدر نعمل Detect و Investigate للـ Suspicious activities دي بشكل فعال، لازم نكون عارفين الـ Common Windows standard process names والـ Full paths بتاعتهم، وكمان الـ Expected parent processes.

* المعلومات دي بتساعدنا نعمل Identifying لأي Discrepancies أو Anomalies في الـ Process execution.
* مثال على ده إننا نكتشف Malicious process ليها اسم مشابه لـ Legitimate one، أو نلاقي Process بتعمل Running من مسار غير الـ Standard path.
* عن طريق تحليل الـ Parent-child process relationships، بنقدر نكتشف أي Suspicious behavior، زي مثلاً إن فيه Process طلعت من Unexpected parent process، أو إن فيه Legitimate process طلعت Suspicious child process.

### Practical Case Study (Figure 5.9)

المثال اللي في الصورة بيوضح عملية Suspicious execution للعملية اللي اسمها `svchost.exe`.

1. أول حاجة غريبة هنا إن الـ `svchost.exe` process دي شغالة من المسار `C:\Windows`، وإحنا عارفين إن الـ Legit process المفروض تشتغل من المسار ده:

DOS

```
C:\Windows\System32\
```

2. تاني حاجة، الـ Process دي حصل ليها Spawned من الـ `cmd.exe` process، والمفروض زي ما اتعلمنا إن الـ Expected parent process بتاعها يكون الـ `services.exe` process.
3. طبعاً لو مكنتش عارف الـ Normal behaviors للـ Standard Windows processes، مكنتش هتقدر تلاحظ الـ Techniques دي أبداً.

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>
