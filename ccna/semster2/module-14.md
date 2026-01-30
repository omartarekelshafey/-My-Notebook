# module 14

## &#x20;Path Determination

تعتبر عملية Path Determination من أهم وظائف الـ Router، حيث يقوم بتحديد أفضل واجهة (Interface) لإرسال الـ IP packet بناءً على خريطة داخلية تسمى Routing table.

### &#x20;Longest Match

* بيعتمد الـ Router على قاعدة بتسمى Longest match لاختيار أفضل مسار في الجدول.
* الـ Routing table بتحتوي على Route entries بتتكون من Prefix و Prefix length.
* عشان يحصل مطابقة (Match)، لازم عدد معين من الـ Far-left bits في عنوان الـ Destination IP يتطابق مع الـ Route الموجود في الجدول.
* الـ Longest match هو المسار اللي فيه أكبر عدد من الـ Bits المتطابقة، وهو اللي الـ Router بيفضله دايماً.
* سبب تفضيل الراوتر لكده هو إن المسار ده بيعتبر "الأكثر تحديداً" (Most specific) للوجهة المطلوبة، وكل ما زاد الـ Prefix length (يعني عدد الـ Bits المتطابقة)، كل ما كان المسار أدق وأقرب للهدف

### build Routing Table

الـ Router بيجمع المعلومات في جدول التوجيه من عدة مصادر:

* الDirectly Connected Networks: بتضاف تلقائياً لما يكون الـ Interface واخد IP address و Prefix length وحالته (Active) أو (Up and up).
* الRemote Networks: الشبكات البعيدة اللي الـ Router بيعرفها بطريقتين:
  * الStatic routes: بتضاف يدوياً من قبل مدير الشبكة.
  * الDynamic routing protocols: بتضاف لما الـ Protocols تتعلم عن الشبكات ديناميكياً.
* ال Default Route: بيستخدم كـ Gateway of last resort، وده المسار اللي الـ Router بيلجأ له لو ملاقاش أي مطابقة تانية في الـ Routing table. الـ Prefix length بتاعته بتكون 0/.

***

## &#x20;Packet Forwarding

بمجرد ما الـ Router يحدد المسار، بيبدأ في عملية الـ Forwarding وهي نقل الـ Packet من Ingress interface لـ Egress interface.

### &#x20;(Decision Process)

1. الـ Router بيستلم الـ Data link frame وبيفك تغليف الـ IP packet.
2. بيفحص الـ Destination IP address في الـ Packet header ويقارنه بالـ IP routing table.
3. بيدور على الـ Longest matching prefix في الجدول.
4. بعدها بياخد واحد من 3 قرارات:
   * الForward to Directly Connected: لو الوجهة على شبكة متصلة مباشرة، بيبعتها للجهاز فوراً.
   * الForward to Next-Hop Router: لو الوجهة بعيدة، بيبعت الـ Packet للـ Router التالي المذكور في الـ Route entry.
   * الDrop the Packet: لو مفيش أي مطابقة في الجدول ومفيش Default route، بيتم مسح الـ Packet.

### &#x20;(Forwarding Mechanisms)

الـ Cisco routers بتدعم 3 طرق لنقل البيانات:

* الProcess switching: طريقة قديمة، الـ CPU بيعالج كل Packet لوحدها في الـ Control plane.
* الFast switching: بتستخدم Fast-switching cache لتخزين معلومات الـ Next-hop؛ أول Packet بس بيتعالج بالـ CPU والباقي بيتم توجيهه من الكاش.
*

    #### الـ Cisco Express Forwarding (CEF)

    دي أحدث وأسرع طريقة الـ Router بيستخدمها حالياً وهي الافتراضية في أجهزة Cisco. الفكرة فيها إنها مش بتستنى لما الـ Packet توصل عشان تقرر هتعمل إيه، لكنها بتجهز "الردود" مسبقاً:

    * جدول الـ Forwarding Information Base (FIB): ده نسخة جاهزة من الـ Routing table بس متظبطة بطريقة تخلي الـ Router يدور فيها بسرعة جداً. بمجرد ما الشبكة تستقر (Converged)، الجدول ده بيكون فيه كل المعلومات اللي الـ Router محتاجها عشان يوجه أي Packet.
    * جدول الـ Adjacency table: ده جدول تاني جنبه بيكون فيه معلومات الـ Layer 2 (زي الـ MAC addresses) للأجهزة المجاورة (Next-hops).
    * الميزة الكبيرة هنا إن الـ Forwarding بيحصل بناءً على "تغييرات الشبكة" (Change-triggered) مش بناءً على وصول أول Packet، وده بيخلي العملية سريعة جداً وبتقلل الضغط على الـ CPU

***

## &#x20;IP Routing Table

الجدول ده بيحتوي على قائمة بالشبكات المعروفة ومصادرها.

### components Route Entry

كل سطر في الجدول بيحتوي على معلومات محددة:

*
  * الـ Route source: بيقولنا "المسار ده جه منين؟"
  * &#x20;الـ Destination network: بيقول "إحنا رايحين فين؟"، وبيشمل عنوان الشبكة والـ Prefix length.
  * الـ Administrative distance (AD): بتقول "أصدق المصدر ده قد إيه؟"؛ لو الراوتر عرف نفس الشبكة من مصدرين، بيختار اللي الـ AD بتاعته أقل لأنه بيبقى "موثوق" أكتر.
  * قيمة الـ Metric: بتقول "الطريق ده هيكلفني كام؟"؛ لو عندي كذا طريق لنفس الشبكة ومن نفس المصدر، بختار الطريق صاحب الـ Metric الأقل لأنه بيكون "الأقصر" أو "الأسرع".
  * عنوان الـ Next-hop: بيقول "مين اللي هسلمله الـ Packet؟".
  * واجهة الـ Exit interface: بتقول "أرمي الـ Packet من أنهي بورت عندي؟" عشان تروح للوجهة.

### different between IPv4 و IPv6 Tables

* الIPv4 Routing Table: لسه محتفظ بهيكل Classful addressing، وبتلاقي فيه Parent route وتحته Child routes اللي بتكون Indented (مزاحة للداخل).
* الIPv6 Routing Table: الهيكل بتاعه بسيط جداً ومفيهوش Classes، وكل الـ Entries متساوية في التنسيق والمحاذاة.

***

## Static and Dynamic Routing

الشبكات غالباً بتستخدم مزيج من النوعين دول لتأمين التوجيه.

### Static Routing

* بيتم إعداده يدوياً (Manually configured).
* ممتاز للشبكات الصغيرة أو الـ Stub networks (الشبكات اللي ليها مخرج واحد بس).
* بيستخدم لتعريف الـ Default route للوصول لمزود الخدمة.
* بيتميز بأن الـ Security فيه عالي (Inherent) ومبيستهلكش موارد الـ CPU أو الـ Bandwidth.

### &#x20;Dynamic Routing

الـ Dynamic routing هو إن الراوترات تتكلم مع بعض وتتبادل المعلومات لوحدها.

* هدف الـ Dynamic routing: اكتشاف الشبكات البعيدة، وتحديث المعلومات أول بأول، واختيار أفضل مسار، وإيجاد مسار بديل لو المسار الحالي وقع.
* مكونات البروتوكول: بيعتمد على Data structures (جداول في الـ RAM)، و Messages (رسائل لاكتشاف الجيران وتبادل الأخبار)، و Algorithm (عمليات حسابية لاختيار أحسن طريق).
* مميزاته مقارنة بالـ Static: بيقدر يتعامل مع الشبكات الكبيرة (Scalable) وبيغير مساره تلقائياً لو حصل أي تغيير في التوصيلات.

### الفرق بين أنواع البروتوكولات (Classification)

#### 1. حسب مكان العمل (IGP vs EGP)

* Interior Gateway Protocols (IGPs): دي البروتوكولات اللي بنستخدمها عشان نربط الـ Routers داخل مؤسسة أو شركة واحدة (زي OSPF و EIGRP و RIP).
* Exterior Gateway Protocols (EGPs): فيه بروتوكول واحد بس هو الـ BGP، وده وظيفته يربط الشركات الكبيرة ببعضها أو يربط الـ ISPs ببعضهم عبر الإنترنت.

#### 2. حسب طريقة التفكير (Algorithm Used)

* الDistance Vector: الراوتر هنا بيعرف المسافة والاتجاه للشبكة من جيرانه بس، زي ما يكون بيسأل الناس في الشارع. مثال: RIPv2 و EIGRP.
* الLink-State: هنا كل راوتر بيبني "خريطة" كاملة لكل الشبكة وتوصيلاتها، وده بيدي رؤية أوضح. مثال: OSPF و IS-IS.
* الPath Vector: وده خاص بالـ BGP، وبيسجل المسار بالكامل عشان يضمن مفيش دواير مغلقة (Loops).

***

### ثانياً: مقاييس المسافة (Metrics)

الـ Metric هو "القيمة الرقمية" اللي البروتوكول بيستخدمها عشان يقيس الطريق ده "يكلفه" كام. الراوتر دايماً بيختار الطريق اللي الـ Metric بتاعه أقل

إليك الفرق بين البروتوكولات في القياس:

| **الـ Protocol** | **المقياس المستخدم (Metric)** | **فكرته ببساطة**                                                                                                                                            |
| ---------------- | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RIP              | Hop Count                     | <p>بيعد كام راوتر في السكة. لو طريق فيه راوترين وطريق فيه 3، هيختار الـ 2 حتى لو السكة أبطأ.</p><p><a class="button secondary"></a></p>                     |
| OSPF             | Cost                          | <p>بيعتمد على الـ Bandwidth (السرعة) التراكمية. السكة اللي فيها لينكات أسرع بيكون الـ Cost بتاعها أقل، فبيفضلها.</p><p><a class="button secondary"></a></p> |
| EIGRP            | Bandwidth & Delay             | ده بروتوكول "ذكي"، بيحسب المسافة بناءً على أبطأ سرعة في السكة والوقت اللي الداتا بتاخده (Delay).                                                            |

***

