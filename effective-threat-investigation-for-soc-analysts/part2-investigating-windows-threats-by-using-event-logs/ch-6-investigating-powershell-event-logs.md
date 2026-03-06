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

