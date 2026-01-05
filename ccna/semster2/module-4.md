# module 4

Inter-VLAN Routing&#x20;Operation
---------------

### What is Inter-VLAN Routing?

النص بيتكلم عن نقطة جوهرية في الشبكات وهي إزاي نخلي الـ VLANs المختلفة تتكلم مع بعض.

في الطبيعي، الـ VLANs بتستخدم عشان تقسم شبكة الـ Layer 2 لأجزاء (Segmentation). وبغض النظر عن سبب التقسيم ده، القاعدة الثابتة هي إن الأجهزة (Hosts) اللي في VLAN معينة مستحيل تتكلم مع أجهزة في VLAN تانية بشكل مباشر.

عشان نكسر العزلة دي ونخلي الـ VLANs تشوف بعض، لازم نستخدم جهاز بيشتغل في Layer 3 (زي الـ Router أو الـ Layer 3 Switch) عشان يقوم بعملية (Routing). العملية دي بنسميها Inter-VLAN Routing.

***

**There are three inter-VLAN routing options:**

النص وضح إن فيه 3 طرق أساسية عشان نعمل الموضوع ده، وكل واحدة ليها استخدامها حسب حجم الشبكة:

**1. Legacy Inter-VLAN Routing (الطريقة القديمة)**

* الوصف: ده الحل التقليدي القديم.
* العيوب: مش عملي ومش بيستحمل التوسع (Does not scale well). ده لأنك كنت بتحتاج توصل كابل حقيقي (Physical Interface) من الراوتر لكل VLAN عندك، وده طبعاً إهدار للـ Ports.

**2. Router-on-a-Stick**

* الوصف: ده الحل الشائع والمقبول للشبكات الصغيرة والمتوسطة.
* الفكرة: بنستخدم كابل واحد (Trunk) بين السويتش والراوتر، وبنقسم الـ Interface بتاعة الراوتر لـ (Sub-interfaces) وهمية، كل واحدة بتمسك VLAN.

**3. Layer 3 Switch using SVIs**

* الوصف: ده الحل الأكثر كفاءة وقابلية للتوسع (Most Scalable).
* الاستخدام: مناسب جداً للمؤسسات المتوسطة والكبيرة.
* الفكرة: هنا مش بنحتاج راوتر خارجي، السويتش نفسه (Multilayer Switch) بيقوم بالدور ده عن طريق إنشاء واجهات وهمية اسمها SVIs (Switched Virtual Interfaces) لكل VLAN، والـ Routing بيتم جوا السويتش بسرعة عالية جداً.

### Legacy Inter-VLAN Routing

&#x20;(How it works):

* الحل ده كان بيعتمد على استخدام Router فيه كذا مخرج (Multiple Ethernet Interfaces).
* كل Interface في الراوتر بيتوصل بـ Switch Port موجود في VLAN مختلفة.
* الـ Router Interfaces دي هي اللي بتلعب دور الـ Default Gateways للأجهزة (Local Hosts) الموجودة في الـ Subnet الخاصة بكل VLAN.

&#x20;(Limitations):

* على الرغم إن الطريقة دي شغالة فعلياً (Works)، لكن فيها عيب كبير جداً وهو إنها Not Reasonably Scalable (غير قابلة للتوسع بشكل منطقي).
* السبب إن الرواتر عندها عدد محدود من الـ Physical Interfaces.
* فكرة إننا نخصص One Physical Interface لكل VLAN بتؤدي إننا نستهلك الـ Capacity بتاعة الراوتر وتخلص بسرعة جداً (Quickly Exhausts).

### Router-on-a-Stick Inter-VLAN Routing

&#x20;(The Main Advantage):

* الطريقة دي بتتغلب على قيود الـ Legacy method لأنها بتحتاج One Physical Ethernet Interface فقط عشان تعمل Routing للترافيك بين كذا VLAN موجودين في الشبكة.

&#x20;(Configuration):

* بنخلي الـ Interface بتاع راوتر (Cisco IOS) يشتغل كـ 802.1Q Trunk.
* بيتوصل بـ Trunk Port على سويتش (Layer 2 Switch).
* التريك هنا إننا بنستخدم Subinterfaces على الراوتر عشان نحدد الـ VLANs اللي محتاجة توجيه.

3\. يعني إيه Subinterfaces؟

* دي عبارة عن واجهات وهمية معمولة بالسوفت وير (Software-based virtual interfaces).
* كل مجموعة منها بتكون مرتبطة بـ Physical Interface واحد حقيقي.
* كل Subinterface بيتظبط بشكل مستقل (Independently Configured) بـ IP Address ورقم VLAN خاص بيه.

4\. حركة البيانات (Traffic Flow):

* لما الترافيك اللي عليه Tag يدخل للراوتر، بيتحول للـ VLAN Subinterface المناسب.
* الراوتر بياخد قرار التوجيه (Routing Decision) بناءً على الـ Destination IP.
* الراوتر بيحدد مخرج البيانات (Exit Interface). لو المخرج ده كان 802.1Q Sub interface، الراوتر بيحط Tag للبيانات برقم الـ VLAN الجديدة ويبعتها تاني من نفس الـ Physical Interface.

### Inter-VLAN Routing on a Layer 3 Switch

1\. المفهوم الأساسي:

* بنستخدم حاجة اسمها SVI (Switched Virtual Interface). دي عبارة عن واجهة وهمية (Virtual Interface) بتتعمل جوا الـ Layer 3 Switch.
* تنويه: الـ Layer 3 Switch بيتقال عليه كمان Multilayer Switch لأنه بيشتغل في Layer 2 و Layer 3 مع بعض، بس في الكورس هنا هنستخدم مصطلح "Layer 3 Switch".

2\. طريقة التشغيل (Operation):

* الـ SVIs بتتعمل بنفس الطريقة اللي بنعمل بيها الـ Management VLAN Interface.
* لازم الـ SVI تتعمل لـ VLAN تكون موجودة فعلياً على السويتش.
* على الرغم من إنها Virtual، لكن الـ SVI بتقوم بنفس وظيفة الـ Router Interface بالظبط.
* وظيفتها تحديداً: بتعمل معالجة للبيانات في الطبقة التالتة (Layer 3 processing) لأي packets مبعوتة من أو إلى أي بورت في السويتش تابع للـ VLAN دي.

3\. مميزات الـ Layer 3 Switch (Advantages): النص ذكر مميزات قوية جداً للطريقة دي مقارنة بالـ Router-on-a-Stick:

* أسرع بكتير (Much Faster): لأن كل حاجة بتتم عن طريق الـ Hardware Switching and Routing.
* مش محتاج وصلات خارجية (No external links): مش محتاج توصل كابل من السويتش للراوتر عشان تعمل Routing.
* Bandwidth أعلى: مش محدود بـ Link واحد، لأنك تقدر تستخدم Layer 2 EtherChannels كـ Trunk links بين السويتشات عشان تزود السرعة.
* Latency أقل بكتير: لأن البيانات مش محتاجة تخرج برا السويتش عشان يتعملها Routing لشبكة تانية.
* الأكثر انتشاراً: بتستخدم بشكل شائع جداً في الـ Campus LANs أكتر من الراوترات.

4\. العيب الوحيد (The only disadvantage):

* الـ Layer 3 Switches سعرها أغلى (More Expensive).

Troubleshoot Inter-VLAN&#x20;Routing
-------------

#### 1. مشكلة اختفاء الـ VLANs (Missing VLANs)

* إيه هي المشكلة:
  * إن الـ VLAN المطلوبة مش موجودة (يا إما متعملتش أصلاً، أو اتمسحت بالغلط، أو مش مسموح لها تعدي في الـ Trunk link).
  * معلومة مهمة: لو مسحت VLAN، كل البورتات اللي كانت تبعها بتبقى Inactive (غير نشطة)، وتفضل كدة لحد ما تنقلهم لـ VLAN تانية أو تكرتها من جديد.
* نكتشفها إزاي (Verification):
  * استخدم الأمر: `show vlan [brief]` عشان تشوف الـ VLANs الموجودة.
  * استخدم الأمر: `show interfaces switchport` أو `show interface [id] switchport` عشان تتأكد من تبعية البورت للـ VLAN.
  * جرب تعمل `ping`.
* نحلها إزاي (How to Fix):
  * اعمل (Create) أو (Re-create) للـ VLAN لو مش موجودة (وده هيرجع البورتات تشتغل تلقائي).
  * تأكد إن الـ Host Port محطوط في الـ VLAN الصح.

***

#### 2. مشاكل الـ Trunk Port (Switch Trunk Port Issues)

* إيه هي المشكلة:
  * في سيناريو الـ Router-on-a-Stick، السبب الأكثر شيوعاً هو إن الـ Port الواصل بالراوتر معمول له كونفيجريشن غلط (Misconfigured trunk port).
  * يعني البورت ده مش شغال كـ Trunk.
* نكتشفها إزاي (Verification):
  * استخدم الأمر: `show interface trunk` عشان تتأكد إن البورت شغال Trunk. (لو البورت مظهرش في النتيجة، يبقى هو مش Trunk).
  * لو مظهرش، افحص الكونفيجريشن بالأمر: `show running-config interface X` عشان تشوف هو واخد إعدادات إيه.
* نحلها إزاي (How to Fix):
  * تأكد إن الـ Trunks معمولة صح.
  * تأكد إن البورت فعلاً Trunk Port ومعمول له Enabled.

***

#### 3. مشاكل الـ Access Port (Switch Access Port Issues)

* إيه هي المشكلة:
  * البورت الواصل بالـ PC واخد VLAN غلط.
  * أو البورت مش معمول له Enabled أو مش Access.
  * أو الجهاز (Host) نفسه واخد IP في Subnet غلط.
  * علامة مميزة: تلاقي الـ PC واخد IP و Mask و Gateway صح، بس مش عارف يعمل Ping على الـ Gateway.
* نكتشفها إزاي (Verification):
  * استخدم الأوامر: `show vlan brief` أو `show interface X switchport` أو `show running-config interface X` عشان تتأكد البورت تبع أنهي VLAN.
  * على جهاز الكمبيوتر استخدم `ipconfig` عشان تراجع إعدادات الـ IP.
* نحلها إزاي (How to Fix):
  * عين الـ VLAN الصح للـ Access Port.
  * تأكد إن البورت شغال كـ Access Port و Enabled.

***

#### 4. مشاكل إعدادات الراوتر (Router Configuration Issues)

* إيه هي المشكلة:
  * غالباً بتكون في إعدادات الـ Subinterfaces.
  * يا إما الـ IPv4 Address مكتوب غلط.
  * أو الـ Subinterface مربوط بـ VLAN ID غلط (مثلاً `G0/0/0.10` مربوط بـ VLAN 20 بدل 10).
* نكتشفها إزاي (Verification):
  * استخدم الأمر: `show ip interface brief` عشان تشوف حالة الـ Subinterface.
  * عشان تعرف كل Subinterface تبع أنهي VLAN، استخدم الأمر `show interfaces`.
  * نصيحة: الأمر اللي فات بيطلع كلام كتير، فالنص بينصح تستخدم Filters زي:
    * `include Gig`
    * `include 802.1Q`
* نحلها إزاي (How to Fix):
  * صحح الـ IPv4 Address للـ Router Subinterface.
  * تأكد إن الـ Subinterface مربوط برقم الـ VLAN ID الصحيح.
