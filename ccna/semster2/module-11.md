# module 11

## Implement Port Security

* #### **(Secure Unused Ports):**
* واحدة من أبسط الطرق لتأمين الشبكة هي تعطيل (Disable) أي منفذ (Port) مش واصل عليه جهاز حالياً.
* يتم ذلك عن طريق الدخول على المنفذ واستخدام الأمر التالي:

```bash
shutdown

```

* لتفعيل المنفذ مرة تانية لو احتجته، استخدم أمر `no shutdown`.
* #### **(Mitigate MAC Address Table Attacks):**
* أبسط وأنجح طريقة لمنع هجمات الـ MAC Address Table overflow هي تفعيل خاصية الـ Port Security.
* الخاصية دي بتحدد عدد معين من الـ MAC Addresses المسموح ليها بالاتصال بالمنفذ.
* #### **(Enable Port Security):**
* ملاحظة مهمة: الـ Port Security بيشتغل فقط على المنافذ اللي معمولة Access أو Trunk بشكل يدوي (Manually Configured)، ومش بيشتغل على المنافذ الـ Dynamic.
* الأوامر اللازمة للتفعيل:

```bash
switchport mode access
switchport port-security

```

* بشكل افتراضي، الحد الأقصى للـ MAC Addresses هو 1 فقط.
* #### **(Limit and Learn MAC Addresses):**
* يوجد ثلاث طرق للـ Switch عشان يتعلم الـ MAC Address على المنفذ الآمن:

1. **طريقة (Manually Configured):** الأدمن بيدخل الـ MAC بيده.
2.

**طريقة (Dynamically Learned):** الـ Switch بيتعلم الـ MAC من أول جهاز يوصل، لكن لو عملت Reboot المعلومة بتتمسح.

3.

**طريقة(Dynamically Learned - Sticky):** ودي أفضل طريقة، الـ Switch بيتعلم الـ MAC ويحفظه في الـ Running-config، فبيفضل موجود حتى بعد الـ Restart (لو حفظت الإعدادات).

* أمر تفعيل الـ Sticky:

```bash
switchport port-security mac-address sticky

```

* #### **(Port Security Violation Modes):**
* ماذا يحدث لو جهاز غير مصرح بيه حاول يدخل؟ فيه 3 أوضاع:

1. **وضع (Shutdown):** (ده الافتراضي) المنفذ بيقفل تماماً وبيدخل في حالة `error-disabled` ولمبة المنفذ بتطفي.
2. **وضع (Restrict):** المنفذ بيفضل شغال لكن بيرمي الـ Packets المخالفة وبيسجل العداد (Counter) وبيبعت رسالة Syslog.
3. **وضع (Protect):** أقلهم أماناً، بيرمي الـ Packets المخالفة بس، من غير ما يسجل عداد ولا يبعت رسايل.

***

### Mitigate VLAN Attacks

الجزء ده بيتكلم عن منع الهجمات اللي بتستهدف القفز بين الشبكات الافتراضية (VLAN Hopping).

* **(VLAN Hopping Attacks):**
* المهاجم ممكن يخدع الـ Switch انه يقلب المنفذ لـ Trunk عن طريق بروتوكول DTP، وده بيسمح له يوصل لكل الـ VLANs.
* نوع تاني اسمه Double-tagging attack بيستغل طريقة عمل الـ Hardware في الـ Switches.
* **VLAN (Mitigation Steps):**
* للحماية من الهجمات دي لازم نطبق الخطوات التالية:

1. إلغاء التفاوض (Disable DTP) على المنافذ غير الـ Trunk عن طريق تحويلها لـ Access.
2. تعطيل المنافذ غير المستخدمة ونقلها لـ VLAN ميتة (Unused VLAN).
3. تفعيل الـ Trunk يدوياً على المنافذ اللي محتاجة تكون Trunk.
4. إلغاء الـ DTP على منافذ الـ Trunk باستخدام الأمر `switchport nonegotiate`.
5. تغيير الـ Native VLAN لرقم غير مستخدم (غير VLAN 1).

***

### Mitigate DHCP Attacks

هنا بيشرح إزاي نحمي الشبكة من تلاعب الـ DHCP (زي DHCP Spoofing و Starvation).

* **(DHCP Attacks Review):**
* هدف هجوم DHCP Starvation هو استنفاذ كل العناوين المتاحة عشان يعمل Denial of Service (DoS).
* هجوم DHCP Spoofing بيتم فيه وضع خادم DHCP مزيف في الشبكة عشان يوزع عناوين وإعدادات غلط للعملاء.
* **DHCP (DHCP Snooping):**
* تقنية DHCP Snooping بتفلتر رسايل الـ DHCP وبتعمل Rate-limit (تحديد سرعة) على المنافذ غير الموثوقة.
* يتم تصنيف المنافذ لنوعين:
* **نوع الاول(Trusted Interfaces):** زي الـ Trunks والمنافذ الواصلة بالسيرفرات والرواتر.
* **نوع التاني (Untrusted Interfaces):** زي كل منافذ الـ Access اللي واصلة بأجهزة المستخدمين.
* الـ Switch بيبني جدول اسمه "DHCP Snooping Binding Table" بيربط فيه الـ MAC Address بالـ IP Address للمنافذ غير الموثوقة.
* **(Implementation Steps):**
* الأمر الأساسي لتفعيل الخدمة عالمياً:

```bash
ip dhcp snooping

```

* لتحديد منفذ موثوق (Trusted):

```bash
ip dhcp snooping trust

```

* لتحديد عدد الرسائل المسموح بها عل&#x649;**(Untrusted Interfaces)** (Rate Limit):

```bash
ip dhcp snooping limit rate <number>

```

***

### Mitigate ARP Attacks

* **(Dynamic ARP Inspection - DAI):**
* في هجمات الـ ARP، المهاجم بيبعت رسايل ARP Replies مزيفة عشان يربط الـ MAC بتاعه بالـ IP بتاع الـ Gateway (بيعمل ARP Poisoning).
* خاصية DAI بتعتمد على قاعدة بيانات DHCP Snooping عشان تتأكد إن الـ IP والـ MAC اللي في رسالة الـ ARP حقيقيين.
* الخاصية دي بتعمل "Drop" (إسقاط) لأي رسالة ARP مزيفة جاية من منفذ غير موثوق.
* **(Configuration Guidelines):**
* يُنصح بجعل كل منافذ الـ Access "غير موثوقة" (Untrusted)، وجعل المنافذ الواصلة بـ Switches تانية أو Routers "موثوقة" (Trusted).
* أوامر التفعيل (يتم تفعيلها على الـ VLAN):

```bash
ip arp inspection vlan <vlan_id>

```

* لتحديد (Trusted Interface):

```bash
ip arp inspection trust

```

***

### Mitigate STP Attacks

آخر جزء بيتكلم عن حماية بروتوكول Spanning Tree.

* **أدوات الحماية (PortFast and BPDU Guard):**
* المهاجم ممكن يتلاعب بالـ STP عشان يخلي جهازه هو الـ Root Bridge ويتحكم في حركة المرور.
* الحل هو استخدام ميزتين: PortFast و BPDU Guard.
* **ميزة السرعة (PortFast):**
* تقوم الخاصية دي بتحويل المنفذ فوراً لحالة Forwarding، متجاوزة حالات Listening و Learning.
* تُطبق فقط على منافذ الـ Access الواصلة بأجهزة كمبيوتر (End Devices).
* التفعيل على الواجهة:

```bash
spanning-tree portfast

```

* **ميزة حماية الوحدات (BPDU Guard):**
* لو المنفذ المفعل عليه PortFast استقبل رسالة BPDU (وده مش مفروض يحصل من جهاز كمبيوتر)، الخاصية دي بتعمل Error-disable للمنفذ فوراً.
* ده بيمنع توصيل Switches غير مصرح بيها.
* التفعيل على الواجهة:

```bash
spanning-tree bpduguard enable

```

***

### Port Security Aging

النقطة دي بتتكلم عن كيفية إدارة المدة الزمنية اللي الـ Switch بيحتفظ فيها بالـ MAC Addresses الآمنة قبل ما يحذفها.

* مفهوم التقادم (Aging Concept): تُستخدم خاصية Aging عشان نمسح الـ Secure MAC addresses من المنفذ بشكل أوتوماتيكي من غير ما نضطر نمسحها يدوياً. ده مفيد عشان الجدول ما يتمليش عناوين قديمة مش بنستخدمها.
* (Aging Types): يوجد نوعان من الـ Aging ممكن تفعيلهم على المنفذ
  1. المطلق (Absolute): بيتم مسح العناوين بعد مرور وقت محدد (Aging time)، بغض النظر هل الجهاز لسه بيبعت داتا ولا لأ.
  2. عدم النشاط (Inactivity): بيتم مسح العناوين فقط لو الجهاز بطل يبعت داتا لمدة محددة.
*   تفعيل الخاصية (Configuration): عشان تفعل الـ Aging أو تغير وقته (بالدقائق) أو نوعه، بتستخدم الأمر ده داخل إعدادات الواجهة (Interface Mode):

    ```
    switchport port-security aging time <time_in_minutes>
    switchport port-security aging type {absolute | inactivity}
    ```

    (ملاحظة: لو خليت الوقت 0، ده معناه إن الـ Aging بقى Disabled)
