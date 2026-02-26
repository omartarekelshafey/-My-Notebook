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

<figure><img src="../../.gitbook/assets/image.png" alt="" width="506"><figcaption></figcaption></figure>

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
