# detection eng part 1

## detection eng term

تمام 👌 خليني أفكّهالك خطوة خطوة، بالإنجليزي × عربي عشان يبقى أوضح:

***

#### 🔹 Loop 1 — The Ideal State | الحالة المثالية

الفكرة: الفريق الأزرق (Blue Team) يكون عنده **فهم كامل للأصول Assets** في بيئته (أجهزة، هويات، بيانات، سيرفرات).

* بيحط **Controls** (ضوابط أمنية) تمنع فئات كاملة من الهجمات.
* مثال: لو عندك مشكلة Brute Force → تعمل MFA. لو عندك مشاكل Ransomware → تمنع الماكروز + segmentation.

👉 كأنك بتحط **أقفال قوية** على بابك.

***

#### 🔹 Loop 2 — Hedge Against Loop 1 Failure | الخطة البديلة

حتى لو عندك أفضل lock (قفل) في الباب، ممكن المهاجم ييجي بـ **شاكوش ضخم** ويكسره.

* هنا دور Loop 2: **Detection + Response**.
* زي إنك مركب **كاميرات مراقبة + إنذار**، بحيث لو حد كسر القفل، هتعرف بسرعة وتتصرف.
* ده بالظبط دور **Detection Engineering** → بنبني قواعد Rules + آليات Response عشان نحد من أثر الهجوم بسرعة.

👉 الهدف: نخرج من Loop 2 بسرعة ونرجع للوضع المثالي (Loop 1).

***

#### 🔹 Loop 3 — When Containment Fails | لما الاحتواء يفشل

أحيانًا containment (العزل/إيقاف الحساب/منع الاتصال) ممكن ما ينجحش أو يحصل **ضرر كبير بالفعل**.

* هنا بنحتاج نروح لـ **Recovery** (استرجاع خدمات/بيانات) + **Gap Analysis** (تحليل الفجوات).
* بنسأل: ليه control فشل؟ ليه detection ما لقطش الهجوم بدري؟ إيه اللي ناقص في الإجراءات؟
* التعلم من Loop 3 لازم يتغذّى راجع على Loop 1 & 2 عشان نحسن الوقاية والكشف في المستقبل.

👉 كأنك بعد ما البيت اتسرق، بتصلح القفل، بتركب باب أقوى، وتزوّد الكاميرات.

***

#### 🧠 الخلاصة:

* **Loop 1 = Prevention is king** (المنع أفضل وسيلة).
* **Loop 2 = Detection + Response = Safety net** (شبكة أمان لو الوقاية فشلت).
* **Loop 3 = Recovery + Lessons** (لو حصل ضرر، نسترد + نتعلم).



## detection eng process

تمام ✨ الموضوع ده بيتكلم عن **Detection Engineering Process** (عملية بناء وتطوير أنظمة الكشف).\
خلينا نشرح خطوة خطوة بالعربي × الإنجليزي:

***

#### 🛠️ **Detection Engineering Process**

**0. Detection Story (قصة الكشف)**

* قبل ما نكتب أي Rule، لازم نفهم الـ **Attack Scenario**: المهاجم هيعمل إيه؟ إيه الهدف؟
* بنحوّل الهجوم لقصة:\
  &#xNAN;_&#x45;xample:_ "Attacker يستخدم PowerShell لتنزيل malicious file."
* الهدف: نربط الهجوم بالـ **MITRE ATT\&CK** أو أي framework.

***

**1. Research (بحث وتحليل)**

* ندرس الـ **TTPs** (Techniques, Tactics, Procedures) اللي المهاجمين بيستعملوها.
* نقرأ reports, threat intel, incident data.
* الهدف: نعرف **Indicators** و **Patterns**.

***

**2. Query (الاستعلام / القاعدة)**

* نحول القصة والبحث لـ **detection query** (زي rule في SIEM/EDR).
* مثال: في Splunk, Sigma, أو KQL (Microsoft Sentinel).
* _Example query:_ `EventID=4104 AND powershell.exe AND Invoke-WebRequest`.

***

**3. Backtest (الاختبار الرجوعي)**

* نجرب الـ query على **historical data** (بيانات قديمة).
* الهدف: نشوف:
  * هل القاعدة بترجع أحداث حقيقية؟
  * هل في **false positives** كتيرة؟

***

**4. Canary (التجربة المحدودة)**

* ننشر القاعدة في بيئة محدودة أو test environment.
* نتابع: هل detection بيشتغل صح؟ هل في noise؟
* ده زي "الطائر الكاناري" في المناجم – بيدينا إشارة بدري.

***

**5. Documentation (التوثيق)**

* نكتب كل حاجة:
  * الـ story.
  * الـ query.
  * الـ logic.
  * الـ references (مثلاً MITRE ATT\&CK ID).
* الهدف: أي حد في الفريق يقدر يفهم ويعيد استخدام detection بسهولة.

***

**6. Onboarding (الإطلاق الفعلي)**

* ننشر detection rule في **production** (الأنظمة الحقيقية).
* نضيفه للـ monitoring dashboards و alerting systems.

***

**7. Continuous Improvement (التحسين المستمر)**

* نتابع القاعدة طول الوقت.
* نعدلها لو ظهرت bypasses أو false positives.
* نضيف learnings من **incidents حقيقية** أو من Loop 3 اللي شرحناه قبل شوية

\----------------------------------------------------------------------------------------------------------------------

## detection eng inputs

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

**Threat Intelligence**&#x20;

* بنستخدم تقارير intel اللي بتقول إيه الـ **latest attacks** أو الـ **IOCs** (Indicators of Compromise).
* _مثال:_ Intel report بيقول إن فيه APT group بيستعملوا `rundll32.exe` مع malicious DLL → نكتب detection عليه.

***

**Threat Hunting (الصيد الاستباقي للتهديدات):**\
ده مش مجرد انتظار intel، ده عملية داخلية proactive للبحث عن أي نشاط غريب أو مش متوقع.

* الـ hunter ممكن يبدأ من intel (زي معلومة عن rundll32).
* بعد كده يدور في الـ environment:
  * هل `rundll32.exe` بيشتغل من أماكن مش طبيعية؟
  * هل بيحمل DLLs مش معروفة؟
  * هل فيه anomalous patterns مرتبطة بيه؟
* لو لقوا حاجة suspicious → تتحول لـ **detection rule**.



**Red Teaming Activities**&#x20;

* لما الـ red team يجربوا attack simulation ويستعملوا techniques معينة.
* أي حاجة ينجحوا يعملوها → فرصة نكتب detection جديد.
* _مثال:_ Red Team عمل privilege escalation بواحدة من الـ techniques → Detection Engineer يكتب rule يكتشف ده.

***

**Business Requirements**&#x20;

* ساعات في متطلبات تخص الشركة أو الـ industry.
* _مثال:_ البنك محتاج يراقب أي محاولة تغيير في SWIFT logs.
* يبقى لازم detection مخصوص.

***

**New Log Source**&#x20;

* لو تم إضافة system جديد (مثلاً: Cloud service, Firewall, EDR).
* لازم نعمل detections تستغل الـ logs الجديدة.
* _مثال:_ إضافة Okta logs → نكتب detection لمحاولات MFA bypass.

***

**New Policy / Regulation**&#x20;

* ساعات compliance بيفرض requirements.
* _مثال:_ PCI-DSS أو GDPR بيطلبوا تراقب حاجات معينة.
* يبقى نعمل detection rules توافق المتطلبات دي.

***

## Rules

**WHAT DOES QUERY DO WHEN**\
**CALLED?**

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

### 🖥️ **SIEM Query Flow**

1. **User queries**\
   المستخدم (محقق أو Detection Engineer) يكتب query في الـ SIEM:\
   "هاتلي أي logs فيها `maliciousdomain.com` من index اسمه dns".
2. **SIEM search**\
   الـ SIEM يروح للـ index (فهرس logs) بدل ما يدوّر في كل التخزين (وده أسرع بكتير).
3. **Match found**\
   لو لقى الـ domain في أي log، بيرجع:
   * الـ raw log (البيانات الخام).
   *
     * metadata (زي: الوقت، الجهاز، الـ user اللي عمل request…).
4. **User receives results**\
   المستخدم يشوف الـ logs اللي فيها الدومين الخبيث.

**------------------------------------------------------------------------------------------------------------------**

**WHY ARE RULE SETS NEEDED?**

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>



### 🧠 **SIEM Query via Ruleset & Query Service (شرح مبسط):**

1. **Load each rule**\
   الـ SIEM أو الـ Query Service بيجيب ruleset (المجموعة كلها).
2. **Perform the query stored in the rule on index:n**\
   لكل rule فيه query محفوظة → SIEM يشغلها على الـ index المناسب.
3. **Search in storage**\
   لو الـ index موجود، يبدأ يدور في الـ logs.
4. **Found it!**\
   لو فيه match → يرجع:
   * الـ raw log.
   * الـ metadata (مين، إمتى، فين).
5. **Result = Alert (غالبًا)**\
   **---------------------------------------------------------------------------------------------------**

| 📌 **الفكرة**       | Query واحدة بتدور على **event محدد** (زي maliciousdomain.com في DNS logs).                         | ربط **أكتر من event** من مصادر مختلفة علشان تكتشف هجوم متقدم.                                                          |
| ------------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 🔎 **بيشتغل إزاي؟** | بيبحث في الـ logs عن شرط واحد (Indicator of Compromise - IOC).                                     | بيربط events متعددة (failed logins + privilege escalation + data exfiltration).                                        |
| ✅ **المميزات**      | - بسيط وسهل. - سريع التنفيذ. - مناسب للهجمات المباشرة (single IOC).                                | - Ability to detect advanced threats. - Understanding relationships between data points. - High customization ability. |
| ❌ **العيوب**        | - Limited، ما يكشفش هجمات معقدة. - ممكن يدي false positives كتيرة. - محتاج analyst يتابع باستمرار. | - Complicated & time-consuming day-to-day. - Risk of False Positives (ممكن تهدد detection).                            |
| 🛠️ **أمثلة**       | - Detect malicious domain. - Search عن rundll32.exe execution.                                     | - Failed logins متكررة + abnormal login time + large data exfiltration.                                                |
