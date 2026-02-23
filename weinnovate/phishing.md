# Phishing

## Definition

**Phishing**: ده نوع هجوم بيعملوا فيه هاكرز نفسهم جهة موثوق فيها عشان يضحكوا على الناس ويخلوهم يسلّموهم بيانات زي الباسورد أو معلومات فلوس. بيستخدموا إيميلات باين إنها حقيقية أو مواقع مزيفة أو رسايل شبه الأصل.

## Impact

1. **Data Theft and Identity Theft**
2. **Financial Losses**
3. **Malware Infection**
4. **Operational Disruption**
5. **Reputational Damage**

## Types

| type               | description                          |
| ------------------ | ------------------------------------ |
| **Spear Phishing** | استهداف شخص أو شركة معينة بالذات     |
| **Whaling**        | استهداف المديرين الكبار أو “الحيتان” |
| **Vishing**        | التصيّد عن طريق مكالمات تليفون       |
| **Smishing**       | رسائل SMS خادعة لسرقة بيانات         |



**Why Do People Fall for This?!**

Social Engineering: People trust authority; they act fast in emergencies.\
Example Tactics: “Fake emails saying you missed a package.” Or “Your account is locked! Click here to\
recover it.

## Techniques and Tactics

تمام، خليني أكتبلك النسخة كلها عربي + شوية مصطلحات إنجليزي عشان تبقى واضحة ومتنساقة مع اللي فات:

**Techniques and Tactics**

* **Deceptive Emails**
  * _Fake Sender Info_: انتحال إيميل من جهة موثوق فيها (زي: `support@bankofy0urtrust.com`).
  * _Urgency & Threats_: رسائل فيها تهديد أو استعجال زي "Immediate Action Required!" عشان يضغطوا على الضحية.
  * _Phishing Links_: روابط مضللة بتحوّل لصفحات تسجيل دخول مزيفة لسرقة البيانات.
* **Fake Websites**
  * _Look-Alike Domains_: تغيير بسيط في الرابط (زي: `faceb00k.com`) يخلي الموقع شبه الأصلي.
  * _SSL Certificates_: استخدام HTTPS عشان الموقع يبان إنه آمن ويكسب ثقة الضحية.
  * _Credential Harvesting_: صفحات دخول مزيفة بتسحب بيانات الدخول من المستخدم.
* **Social Engineering**
  * _Pretexting_: المهاجم يمثل دور زي موظف HR عشان يقدر ياخد معلومات.
  * _Baiting_: إغراءات زي "جايزة خاصة" تخلي الضحية يضغط على لينك.
  * _Quid Pro Quo_: المهاجم يمثل دعم فني ويوعد بمساعدة مقابل إنه ياخد وصول لجهاز الضحية.



## how to detect Phishing&#x20;



* **Email Gateways**: بتشتغل كخط الدفاع الأول، بتفحص الإيميلات وتكشف اللينكات الخبيثة، المرفقات، وأنماط الـ phishing المعروفة. كمان بتستخدم **Threat Intelligence Feeds** عشان تتابع أحدث الأساليب.
* **Techniques in Gateways**: تكشف علامات زي الـ spoofed domains، عناوين مرسل متغيرة، أو كلمات مفتاحية مرتبطة بالـ phishing. بتعمل كمان **sandboxing** للينكات (تجربتها في بيئة آمنة) عشان تشوف السلوك.
* **EDR Alerts**: SOC بيحلل التنبيهات لو في ملف مشبوه اتنزّل أو المستخدم ضغط على لينك.
* **Threat Intelligence**: المحللين في SOC ما بيركزوش على التنبيه الواحد بس، لكن بيشوفوا **patterns**. الـ feeds بتديهم وعي بالـ phishing tactics الجديدة، الـ compromised domains، والـ malicious IPs المعروفة.

## The SOC Playbook

**The SOC Playbook – When You Catch a Phish**

* **Immediate Action**: عزل المستخدم أو الجهاز المصاب بسرعة.
* **Analyze**: مراجعة محتوى اللينك وتحليل إذا كان فيه Malware أو محاولة سرقة بيانات.
* **Communicate**: إرسال تنبيهات وتوعية للمستخدمين المتأثرين.

## SOC Response Once Phishing is Detetced

* **Isolation and Containment**: عزل الأجهزة أو الحسابات المتأثرة عشان يمنعوا انتشار الهجوم.
* **Investigation and Remediation**: المحللين بيتتبعوا مصدر الهجوم، يقيموا حجم الضرر، ويعملوا حظر للـ IPs أو الـ URLs المستخدمة.
* **User Notification and Awareness**: تنبيه المستخدم المتأثر، وتوجيهه يغير الباسورد، يحسن ممارسات الأمان، وكمان نشر وعي داخل المنظمة.

## Prevention Measures

Training: Educate employees on phishing basics.\
Strong Email Filters: Keep spam out before it even lands.\
Multi-Factor Authentication (MFA): Joke that this is like “lock, stock, and two smoking passwords.”

## Email workflow

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>



## Email Security measures

**SPF** >>>Sender Policy Framework ده علشان يتاكد انه مصدر ايميل\
**DKIM**>>>Domain Keys Identified Mail لتاكد انه ايميل وهو بيبعت محصلوش حاجه&#x20;

**DMARC** >>>Domain-based Message Authentication, Reporting بيمنع التعديل علي بولسي

تمام 👌\
أنت محتاج النص يتكتب **من اليمين للشمال (RTL)** عشان يبقى متنسق مع العربي. أنا هظبطهولك كده:

***

#### SPF >>> Sender Policy Framework

ده علشان يتأكد إن مصدر الإيميل صحيح.

مثال:

* عندنا IP: `1.1.1.1` (سليم) و IP: `6.6.6.6` (بتاع attacker).
* الـ `1.1.1.1` عايز يبعت لـ MUA معين.
* الـ attacker يحاول يبعت بدلًا من `1.1.1.1`.
* الـ destination هترفض الرسالة لأنها محددة مين اللي مسموح له يبعت.

كمان في **email header** بيظهر جزء اسمه **Auth-Result**، والـ SPF بيكون ليه نتائج:

* **Pass** → سليم.
* **Fail** → مرفوض.
* **None** → مش متحدد.
* وفي حالات تانية زي **SoftFail** (بين الـ Fail والـ None).

***

#### DKIM >>> Domain Keys Identified Mail

ده بيعتمد على **Digital Signature**.

* الإيميل بيتحط فيه توقيع (Signature).
* الـ Receiver بيشوف التوقيع ويتأكد منه.
* لو تمام → يبقى الإيميل ما اتغيرش.

إزاي ده بيتم؟

* الإيميل بيتشفّر بـ **Private Key** عند المرسل.
* لما يوصل، الـ Receiver يستخدم **Public Key** علشان يتأكد إن التوقيع صحيح.

**مشكلة أخيرة: One Final Problem – How Many "From" Addresses?**\
أحيانًا الإيميل اللي ظاهر قدامك يكون من شخص أو جهة (زي "الجامعة")، لكن جواه في الـ "Mail From" يطلع عنوان تبع Attacker.\
الحل هنا بيكون باستخدام **DMARC**.

***

#### DMARC >>> Domain-based Message Authentication, Reporting & Conformance

* هنا لازم الدومين يكون مظبوط.
* والـ IP مظبوط.
* ويتحقق من شروط **SPF + DKIM** مع بعض.
* كده بيتأكد إن الـ "From" الظاهر للمستخدم متطابق مع الحقيقي.



## Email threat types

تمام 👌\
خلينا نرتب الكلام ده ونكتبه من اليمين للشمال بشكل منسق وواضح، بحيث يبقى أسهل للمذاكرة:

***

### أنواع التهديدات عبر البريد الإلكتروني (Email Threat Types)

#### 🎯 Spearphishing Attachments (مرفقات التصيّد الموجّه)

* **ملفات Microsoft Office خبيثة**: بيتم حقن المستند بـ VBA Macros ضارة.
* **ملفات PDF خبيثة**: بيتم إرفاق PDF شكله طبيعي لكنه يحتوي على كود يستغل ثغرات في برنامج قراءة الـ PDF.
* **ملفات مضغوطة (.rar, .7z, .zip, إلخ)**: المهاجم يرسل ملف مضغوط بداخله برنامج خبيث (Executable)، ويخدع الضحية إنه يفك الضغط ويشغّله.
* **ملفات ISO Images**: زاد استخدامها مؤخرًا كطريقة لتوصيل (Deliver) البرمجيات الخبيثة.
* **ملفات HTML**: مرفقات HTML تحاكي صفحات تسجيل دخول مألوفة بهدف سرقة بيانات الدخول.

***

#### 🔗 Spearphishing Links (روابط التصيّد الموجّه)

* رابط خبيث يهدف إلى **سرقة بيانات الدخول (Credentials Harvesting)**.
* رابط خبيث يهدف إلى **تحميل برمجيات خبيثة (Malware Download)**.

***

#### 💣 Blackmail Emails (رسائل ابتزاز إلكتروني)

* عرض **Screenshots** من بيانات مخترقة أو من جهاز الضحية.
* **انتحال عنوان البريد الإلكتروني للضحية نفسه (Email Spoofing)** لزيادة المصداقية.

***

#### 🏢 Business Email Compromise (اختراق البريد الإلكتروني التجاري)

* **تقنية Email Thread Hijacking**: المهاجم يدخل في محادثة بريدية حقيقية ويستمر بنفس السياق لخداع الضحية.

***

## header analysis

تمام ✅ هنشيل الـ **BCC** و **CC** ونخلي التركيز على **To** فقط.\
وده هيكون الشكل النهائي المنظم 👇

***

### 📌 Important Email Header Fields

| **From**              | يوضح اسم وبريد المرسل                              | التحقق هل المرسل حقيقي ولا Spoofed             |
| --------------------- | -------------------------------------------------- | ---------------------------------------------- |
| **To**                | يوضح تفاصيل المستقبل المباشر                       | يكشف هل الإيميل موجّه لشخص محدد أو Bulk (Spam) |
| **Date**              | وقت إرسال الرسالة                                  | المقارنة مع _Received headers_ لاكتشاف التلاعب |
| **Subject**           | موضوع الرسالة                                      | قد يحتوي على أنماط Phishing أو Spam            |
| **Return-Path**       | مكان استقبال رسائل الفشل (Bounce)                  | اختلافه عن _From_ قد يشير إلى Spoofing         |
| **Reply-To**          | العنوان اللي يستقبل الردود                         | المهاجم قد يضع عنوان مختلف لخداع الضحية        |
| **Domain Key / DKIM** | توقيع رقمي للتأكد من سلامة الرسالة                 | فشل الاختبار = احتمال Spoofing أو Phishing     |
| **Message-ID**        | رقم تعريفي فريد لكل رسالة                          | التكرار = حملة Spam أو تزوير                   |
| **MIME-Version**      | يوضح دعم الإيميل لمحتويات (صور، HTML، Attachments) | يساعد في كشف Attachments ضارة                  |
| **Received**          | يسجل كل سيرفر مر عليه الإيميل (Reverse Order)      | مقارنة الـ IP ووقت الإرسال تكشف التلاعب        |
| **X-Spam-Status**     | يوضح Spam Score للرسالة                            | يساعد في تحديد Spam من Legitimate              |

