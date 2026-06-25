# VPN Log

تُعد تقنية الـ VPN هي التقنية التي تسمح للمستخدمين بالدخول إلى الـ Internal Network عن بُعد، وكأنهم موجودون في المكتب بالضبط. وبالنسبة لأي SOC Analyst، تُعد الـ VPN Logs من أهم المصادر لأنها تكون دائماً Publicly Exposed، لذلك فهي هدف أساسي للـ Attackers.

***

### VPN Deployment Methods

تعتمد المؤسسات غالباً على طريقتين لتشغيل الـ VPN:

1. طريقة الـ Integrated: وتكون مدمجة كـ Module داخل الـ Firewall.
2. طريقة الـ Standalone: وتعتمد على أجهزة مخصصة للـ VPN فقط، وتُسمى Dedicated VPN Appliances.

***

### VPN Log Analysis and Key Fields

عند تحليل الـ VPN Logs، نركز على ثلاثة عناصر أساسية: الـ Source IP، والـ Username، والـ Result، وهل الدخول نجح أم فشل.

#### Sample VPN Log

```
date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1653134913959078891 tz="+0300" logid="0101039424" type="event" subtype="vpn" level="information" vd="root" logdesc="SSL VPN tunnel up" action="tunnel-up" tunneltype="ssl-web" tunnelid=462105151 remip=13.29.5.4 user="letsdefend-user" reason="login successfully" msg="SSL tunnel established"
```

#### Key Log Fields Explained

* حقلا التاريخ والوقت `date` / `time`.
* نوع الـ Log الفرعي `subtype`، وفي حالتنا يكون `vpn`.
* نوع الـ Tunnel المستخدم `tunneltype`، مثل SSL أو IPSec.
* عنوان الـ IP الخارجي للمستخدم `remip`.
* اسم المستخدم الذي أجرى Authentication، وهو `user`.
* سبب أو نتيجة المحاولة `reason`، مثل `login successfully`.

***

### Critical Analysis: From Remote IP to Tunnel IP

يجب أن ينتبه الـ SOC Analyst إلى نقطة مهمة جداً، وهي الـ Internal IP Assignment:

* مرحلة الـ Connection: يبدأ الـ User بالتواصل مع الـ Firewall من خلال الـ `remip` الخاص به، وهو الـ Public IP.
* مرحلة الـ Tunneling: بعد نجاح الـ Login، يمنح الـ VPN Gateway المستخدم عنوان Internal IP يُسمى `tunnelip`.
* مرحلة الـ Traffic Logs: أي تحرك للمستخدم بعد ذلك داخل الشبكة سيظهر في الـ Traffic Logs باستخدام الـ `tunnelip`، وليس الـ `remip`.

***

### SOC Analysis Scenarios

يستخدم الـ SOC Analyst الـ VPN Logs لاكتشاف أنواع كثيرة من الـ Threats:

* هجمات الـ Brute-force Attacks: عند وجود محاولات Failed Login كثيرة من نفس الـ IP أو على أكثر من Account.
* تحقيقات الـ Phishing: إذا وقع موظف في Phishing Email، يجب مراجعة الـ VPN Logs الخاصة به للتأكد من عدم دخول شخص غريب باستخدام بياناته من دولة أخرى (Geo-fencing).
* مراقبة الـ Unusual Activity: مثل تسجيل الدخول في أوقات غير معتادة (Unusual Time Periods) أو من أجهزة غير معروفة.
* ربط الـ Logs: عبر مطابقة الـ `srcip` في الـ Firewall Traffic Logs مع الـ `remip` في الـ VPN Logs، للتأكد من أن الـ HTTPS Traffic الظاهر هو بالفعل SSL-VPN.
