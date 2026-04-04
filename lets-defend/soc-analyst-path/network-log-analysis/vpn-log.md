# vpn Log

تعتبر الـ VPN هي التكنولوجيا اللي بتسمح للـ Users إنهم يدخلوا على الـ Internal Network من بعيد وكأنهم موجودين في المكتب بالظبط. وبالنسبة لأي SOC Analyst، الـ VPN Logs دي من أهم المصادر لأنها دايماً Publicly Exposed، يعني هي هدف أساسي للـ Attackers.

***

### VPN Deployment Methods

بتعتمد المؤسسات في الغالب على طريقتين عشان تشغل الـ VPN:

1. طريقة الـ Integrated: ودي بتكون مدمجة كـ Module جوه الـ Firewall.
2. طريقة الـ Standalone: ودي بتعتمد على أجهزة مخصصة للـ VPN بس واسمها Dedicated VPN Appliances.

***

### VPN Log Analysis and Key Fields

لما بنحلل الـ VPN Logs، بنركز على تلات حاجات أساسية: الـ Source IP، والـ Username، والـ Result (هل الدخول نجح ولا فشل).

#### Sample VPN Log

Plaintext

```
date=2022-05-21 time=14:06:38 devname="FG500" devid="FG5HSTF109K" eventtime=1653134913959078891 tz="+0300" logid="0101039424" type="event" subtype="vpn" level="information" vd="root" logdesc="SSL VPN tunnel up" action="tunnel-up" tunneltype="ssl-web" tunnelid=462105151 remip=13.29.5.4 user="letsdefend-user" reason="login successfully" msg="SSL tunnel established"
```

#### Key Log Fields Explained

* كلمة التاريخ والوقت `date` / `time`.
* كلمة نوع الـ Log الفرعي `subtype` وفي حالتنا بيكون vpn.
* كلمة نوع الـ Tunnel المستخدم `tunneltype` زي SSL أو IPSec.
* عنوان الـ IP الخارجي للمستخدم `remip`.
* اسم المستخدم اللي عمل Authentication هو الـ `user`.
* كلمة سبب أو نتيجة المحاولة `reason` (مثلاً login successfully).

***

### Critical Analysis: From Remote IP to Tunnel IP

لازم الـ SOC Analyst ياخد باله من نقطة مهمة جداً وهي الـ Internal IP Assignment:

* مرحلة الـ Connection: الـ User بيبدأ يكلم الـ Firewall من الـ remip بتاعه (الـ Public IP).
* مرحلة الـ Tunneling: بعد ما الـ Login ينجح، الـ VPN Gateway بتدي للمستخدم Internal IP داخلي اسمه tunnelip.
* مرحلة الـ Traffic Logs: أي تحرك للمستخدم بعد كدة جوه الشبكة هيظهر في الـ Traffic Logs بالـ tunnelip ده مش بالـ remip.

***

### SOC Analysis Scenarios

بيستخدم الـ SOC Analyst الـ VPN Logs عشان يكتشف أنواع كتير من الـ Threats:

* هجمات الـ Brute-force Attacks: لو لقيت محاولات كتير Failed Login من نفس الـ IP أو على كذا Account.
* تحقيقات الـ Phishing: لو فيه موظف وقع في Phishing Email، لازم نراجع الـ VPN Logs بتاعته عشان نتأكد إن مفيش حد غريب دخل ببياناته من دولة تانية (Geo-fencing).
* مراقبة الـ Unusual Activity: الدخول في أوقات غريبة (Unusual Time Periods) أو من أجهزة غير معروفة.
* ربط الـ Logs: مطابقة الـ srcip في الـ Firewall Traffic Logs مع الـ remip في الـ VPN Logs عشان نتأكد إن الـ HTTPS Traffic اللي ظاهر هو فعلاً SSL-VPN.
