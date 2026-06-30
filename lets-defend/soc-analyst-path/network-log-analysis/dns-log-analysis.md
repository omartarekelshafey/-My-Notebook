# DNS log analysis

## SOC Analysts and DNS Logs

ال SOC Analysts بيستخدموا الـ DNS Logs عشان يعملوا Check على الـ Domains اللي اتعملها Request وامتى بالظبط خلال فترة الـ Incident Investigation لأي System. وإحنا بنعمل Check على الـ Logs دي، لازم نخلي بالنا من النقط دي:

* نقطة الـ Categories: هل الـ System عمل Domain Requests في Categories المفروض ميعملش Access ليها؟
* نقطة الـ Risk: هل الـ System عمل Domain Requests بتعتبر Risky Categories؟
* نقطة الـ Data Leak: هل كان فيه أي محاولات لعمل Access لـ Known Services (زي Google Drive أو One Drive، إلخ) وقت حالات الـ Data Leak وخلافه؟
* نقطة الـ Threat Intelligence: هل فيه أي Systems بتعمل Requests لـ Domains جبناها من مصادر الـ Threat Intelligence Resources؟
* نقطة الـ Encrypted DNS: عمليات الـ Investigation على الـ DNS Logs لازم تتعمل عشان نعمل Detect لو فيه Access لخدمات الـ DNS Over TLS (DOT) أو الـ DNS over HTTPS (DOH).

## Categories of DNS Logs

سجلات الـ DNS Logs بتتقسم لـ 2 Categories من وجهة نظر الـ SOC Analyst:

1. النوع الأول هو الـ DNS Server Events: دي ببساطة الـ Audit Events اللي بتحصل على الـ Server اللي عليه الـ DNS Records. الـ Events دي بتتحفظ في مسار محدد في الـ Eventlog على الـ Windows Servers. عمليات زي الـ Adding، الـ Deleting، أو الـ Editing للـ Records ممكن نعملها Monitor في الـ Logs دي.
2. النوع التاني هو الـ DNS Queries: دي Logs صعبة شوية في عملية الـ Collect والـ Analyze. سيرفرات الـ DNS Servers مش بتحتفظ بالـ Logs دي كـ Default، ولازم نعملها Enable عشان تبدأ تحتفظ بيها. الـ Queries اللي بتطلع دايركت من الـ DNS Service برضه بتبقى صعبة في الـ Analyze. بس عموماً دي الـ Records اللي ممكن تلاقي فيها مين الـ Systems اللي بتعمل Query للـ Domains الموجودة في الـ IOCs اللي معانا. باختصار، الـ Applications اللي بتقدم DNS Server Services زي Microsoft DNS و Bind DNS و Dnsmasq بتسجل الـ DNS Queries اللي بتستقبلها لما بنطلب منها كده.

## A sample DNS log analysis

{ "timestampt": 1591367999.306059, "source\_ip": "192.168.4.76", "source\_port": 36844, "destination\_ip": "192.168.4.1", "destination\_port": 53, "protocol": "udp", "query": "testmyids.com", "qtype\_name": "A",&#x20;

DNS LOGS FIELDS

* وقت وتاريخ الطلب (Date-Time): متسجل هنا في الـ `timestampt`.
* الـ IP والـ Port بتاع الجهاز اللي طلب (Querying IP, Port): وهو الـ `source_ip` والـ `source_port`.
* نوع الـ Query (أو الـ Query Type): وهنا نوعه `A` (يعني بيسأل عن الـ IPv4 بتاع الـ Domain).
* الـ Domain المطلوب (The requested domain): وهو في المثال `testmyids.com`.



أي  (Network Device) أو  (Database) أو سيرفرات لـ Applications تانية بتكون واضحة في تصرفاتها، والـ Manufacturer بتكون معرفة مجموعة بالـ Domains الطبيعية اللي السيرفرات دي بتكلمها. بره مجموعة دي، الـ Analyst لازم يدور في الـ Logs على 5 حاجات مشبوهة:

1. ال (First time visited domains): domains جديدة تماماً مفيش أي حد في الشبكة كلمها قبل كده.
2. ال  (Domains or subdomains over a certain character size): الـ domains اللي فيها عدد حروف ضخم وغير مفهوم.
3. فحص الـ Domain IOC Controls: مقارنة الـ domains بالـ IOCs اللي معانا.
4. &#x20;محاولات تشفير الـ DNS traffic عشان يهرب من الرقابة.

