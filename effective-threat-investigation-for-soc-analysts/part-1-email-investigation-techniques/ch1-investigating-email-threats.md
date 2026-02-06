# CH1 Investigating Email Threats

## Top infection vectors

#### **Initial Access**

بعد ما المهاجم بيخلص مرحلة الاستطلاع (Reconnaissance) وتجهيز الأدوات (Weaponization)، بيبدأ يدور على أنسب طريقة يدخل بيها لبيئة الضحية. المرحلة دي بنسميها initial access، ودي أهم النقط اللي بتشرحها:

***

#### **Common Techniques**

المهاجمين عندهم طرق كتير عشان يثبتوا رجلهم جوه الشبكة، ومن أهمها:

* تقنية Phishing Emails: وهي إرسال رسائل بريد إلكتروني احتيالية بتستهدف المستخدمين.
* استغلال Public-facing Applications: عن طريق تتبع الثغرات في البرامج المتاحة بشكل مباشر على الإنترنت.
* أسلوب Drive-by Compromise: استدراج الضحية لزيارة موقع إلكتروني تم اختراقه مسبقاً.
* سرقة Valid Credentials: الحصول على بيانات دخول حقيقية زي حسابات الـ VPN أو الـ RDP.

Why do attackers prefer phishing emails to gain initial\
access?
-------

في أسباب كتير بتخلي الـ Phishing هو الخيار المفضل للـ Attackers للوصول للـ Initial Access، ومنها:

**1. Easy Reconnaissance**

خلال مرحلة الـ Reconnaissance Phase، بيقدر المهاجم يجمع الـ Email addresses بسهولة من مصادر كتير زي:

* منصات Social media: وبالأخص موقع LinkedIn.
* إعلانات Job postings: اللي بتنشر إيميلات التواصل.
* قواعد Data leaks: المتاحة على الـ Dark Web.
* أرشيف Wayback Machine: زي موقع Archive.org.
* منصات Marketing platforms: زي موقع ZoomInfo.com.

**2. Simple Weaponization**

تجهيز الـ Weaponized attachment مش عملية صعبة، والمهاجمين بيستخدموا طرق زي:

* رفع Malware: على Cloud platforms شرعية وتبادل الـ Download link.
* استخدام VBA macros: لدمج أكواد خبيثة جوه الـ Documents.
* إرسال Malware executable: في شكل ملف Compressed format.

**3. Human Vulnerability**

بيعتمد الـ Attacker بشكل أساسي على نقص الـ Security awareness عند الـ Users، لإن أغلبهم مش مدرب كفاية إنه يتعامل مع الattacks  .

## Email threat types

استخدام خدمات البريد الإلكتروني بيعرض المؤسسة لتهديدات متنوعة مش بس الـ Phishing. المهاجمين بيستخدموا الـ Email لأغراض تانية زي الـ Blackmailing، والـ Information leakage، والـ Lateral movement.

***

#### **Spearphishing Attachments**

تعتبر الـ Spearphishing Attachments وسيلة لاستهداف أشخاص محددين بملفات ملغمة للحصول على الـ Initial Access أو الـ Credentials.

**Common Attachment Types**

بيختار المهاجم نوع الملف بناءً على بيئة الضحية، وأشهر الأنواع هي:

* ال Microsoft Office documents: زي الـ Word والـ Excel، وبتعتمد على الـ VBA macros.
* ال PDF files: بتستغل ثغرات الـ PDF reader أو بتنفذ كود JavaScript.
* ال Compressed files: زي الـ .zip أو .rar لإخفاء الـ Malware.
* ال ISO images: بتستخدم لتخطي الـ File filters وبرامج الـ Antivirus.
* ال HTML files: بتستخدم لمحاكاة صفحات الـ Login لسرقة الحسابات.

***

#### **Spearphishing Link**

بتعتمد الـ Spearphishing Link على إرسال رابط خبيث بدلاً من ملف، وليها غرضين أساسيين:

* عملية Credential harvesting: توجيه الضحية لموقع مزيف لسرقة بيانات الدخول&#x20;
* تحميل Malware: استضافة الملفات الخبيثة على  OneDrive أو Dropbox ومحاوله ان victim  ينزل ال malware عنده ويشغله

***

* #### **Blackmail Email**

بيُعرف الـ Blackmail email أحياناً بـ Sextortion، وفيه بيدعي المهاجم إنه اخترق جهاز الضحية وسرب بيانات حساسة، وبيطلب فدية بالـ Bitcoin.

**Proof of Infection Methods**

الattack  بيستخدم طرق عشان يقنع الvictim  إن الاختراق حقيقي:

* ائل Screenshots: عرض صور لبيانات  الvictim تم الحصول عليها من الـ Infostealer أو شرائها من الـ Dark web.
* تقنية Email spoofing: تزوير عنوان المرسل ليظهر وكأن الضحية بعت الإيميل لنفسه، وده بيوحي إن الحساب مخترق فعلياً.

***

#### **Business Email Compromise (BEC)**

تعتبر الـ Business Email Compromise أو اختصاراً BEC واحدة من أخطر أنواع الـ Email scams اللي بتستهدف المؤسسات، لأنها مش بتعتمد على ملفات خبيثة قد ما بتعتمد على الـ Deception والتلاعب النفسي.

**Definition and Impact**

هجوم الـ BEC بيستهدف بشكل محدد الـ Individuals اللي ليهم صلاحيات مالية، زي الـ Executives أو الـ Finance employees، بهدف دفعهم لتنفيذ Fraudulent financial transactions. الهجوم ده بيسبب خسائر مالية ضخمة جداً للشركات (Significant financial losses).

***

**Core Techniques in BEC**

عشان المهاجم ينجح في عملية الـ Business Email Compromise، لازم يكسر حاجز الشك عند الضحية. بيعتمد في ده على طريقتين أساسيتين هما الأخطر في المرحلة دي:

***

**1. Email Thread Hijacking**

تعتبر الـ Email Thread Hijacking تقنية "اختطاف" للمحادثات القائمة، وبتتم كالتالي:

* عملية الـ Access: المهاجم بيخترق فعلياً حساب إيميل طرف من الطرفين (زي موظف في شركة أو مورد خارجي).
* مرحلة الـ Silent Monitoring: بيفضل المهاجم يراقب الـ Inbox بهدوء عشان يفهم الـ Context بتاع الشغل والمحادثات اللي فيها فلوس.
* خطوة الـ Interception: لما تيجي فرصة مناسبة (مثلاً وقت دفع فاتورة)، المهاجم بيبعت رد من جوه الـ Thread الحقيقية ويطلب تغيير بيانات الـ Bank Account. الضحية هنا مش بيشك أبداً لأن الكلام جاي كـ Reply في محادثة قديمة هو كان طرف فيها.

***

**2. Email Spoofing**

بتعتمد الـ Email Spoofing على التزوير الظاهري للبيانات دون الحاجة لاختراق الحساب نفسه، وده بيتم عن طريق:

* تزوير الـ Display Name: المهاجم بيخلي اسم المرسل يظهر للضحية كأنه الـ CEO أو Trusted partner.
* تلاعب بالـ Email Header: بيتم تعديل الـ From field عشان يبان قدام الضحية إنه إيميل سليم، لكن في الحقيقة الإيميل مبعوث من Mail server مختلف تماماً تحت سيطرة المهاجم.
* استخدام Look-alike Domains: المهاجم بيسجل Domain قريب جداً من الحقيقي (مثلاً تغيير حرف واحد زي `g0ogle.com` بدل `google.com`) عشان يخدع عين الضحية اللي مش مركزة.

