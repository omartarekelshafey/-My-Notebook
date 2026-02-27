# CH 5Investigating Suspicious  Process Execution Using   Windows Event Logs

## Introduction to Windows Processes

نظام التشغيل Windows بيعتمد بشكل أساسي على العمليات (Processes) عشان يشغل البرامج والمهام اللي في الخلفية. كل عملية (Process) بيكون ليها مساحة مخصصة في الذاكرة (Memory) وموارد خاصة بيها. أي نشاط بيحصل في بيئة Windows زي تسجيل الدخول، أو الوصول للملفات، أو تشغيل مكتبات الربط الديناميكي (DLLs)، دايماً بيكون مرتبط بـ Process معين.

### Tools to View Processes

تقدر تتابع وتشوف الـ Processes اللي شغالة على الجهاز بتاعك باستخدام طريقتين أساسيتين:

* ال (GUI)باستخدام Task Manager
* او  (Command-line) اللي بتعرضلك الprocess  في cmd بتكتب الcommand ده&#x20;

```
tasklist
```

### Windows Process Attributes

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

### Windows Logon (winlogon.exe)

الprocess دي هي اللي بتدير عملية دخول وخروج المستخدمين من الـ Interactive session.

* ال  (Functionality): بتتعامل مع الـ Interactive user logins and logouts. هي المسؤولة عن تشغيل الـ LogonUI.exe عشان تستلم الـ Credentials من المستخدم، وبعدين بتبعتها للـ lsass.exe عشان يعمل ليها Validation.
* (Process Attributes):
  * &#x20;(Process name): winlogon.exe.
  * &#x20;(Process path): `%Systemroot%\System32\winlogon.exe`.
  * (Username): SYSTEM.
  * (Number of instances): One for each interactive user login.
  * ال  (Parent process): N/A (بيتم عمل Created ليها بواسطة الـ smss.exe بس مش بتظهر كـ Parent).

***

### Logon User Interface (LogonUI.exe)

دي gui  اللي بتشوفها لما بتيجي تكتب الباسورد.

* الوظيفة (Functionality): مسؤولة عن الـ User interface لشاشة الـ Login. لما بتكتب بياناتك، هي اللي بتبعتها للـ winlogon.exe أو الـ lsass.exe عشان تكمل عملية الـ Authentication.
* (Process Attributes):
  * &#x20;(Process name): LogonUI.exe.
  * &#x20;(Process path): `%Systemroot%\System32\LogonUI.exe`.
  * &#x20;(Username): SYSTEM.
  * &#x20;(Number of instances): One or more.
  * &#x20;(Parent process): winlogon.exe.

***

### Windows Explorer (explorer.exe)

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

#### 2. Analysis of Event ID 4688

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

