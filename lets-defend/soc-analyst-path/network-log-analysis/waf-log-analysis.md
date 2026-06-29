# WAF Log Analysis

## what is the WAF&#x20;

* التكنولوجيا المستخدمة لحماية الـ Web-based applications هي الـ WAF.
* التحليل الخاص بـ Firewall logs أو الـ IDS/IPS logs لوحده مش كفاية علشان نكتشف الـ Web-based attacks، والسبب الرئيسي هو الـ SSL offload issue والقدرة على التحكم في الـ Data اللي موجودة في الـ Payload جزء من الـ Web request.
* عملية الـ SSL Offload تعني الـ Decryption لـ SSL-encrypted traffic، والهدف الأساسي منها هو تقليل الـ Load وزيادة الـ Performance، بالإضافة لعمل Decrypt للـ Encrypted traffic/request علشان المحتوى يبقى Visible و Controllable من الناحية الأمنية، وبكده الـ Invisible attack vectors في الـ Encrypted traffic بتبقى Detectable أو Preventable.
* الشبكات اللي فيها WAF، الـ Requests من الـ End users بتوصل للـ WAF الأول عبر الـ Internet، بعدين الـ WAF بيعمل Inspect للـ Request وياخد القرار إذا كان هيحصل له Transfer للـ Web Server ولا لأ.
* الميزة الكبيرة هنا للـ WAF هي قدرته على عمل SSL Off-load، وده بيساعد في فحص الـ Content الخاص بالـ HTTPS traffic، لأن الـ WAF اللي معندوش Capability لعمل SSL Offloading مش هيقدر يقدم Full effective protection لأنه مش هيعرف يعمل Inspect للـ Payload جزء من الـ HTTPS communication.

## How it work and WAF for Soc analyst&#x20;

* أنظمة الـ WAF عمومًا بتتعامل مع الـ Web access requests على الـ Public faced systems، وعشان كده الـ WAFs هي أول أنظمة بتعمل Detect للـ Web attacks، والـ WAF logs هي اللي بتساعد الـ SOC Analysts في الـ Detection لـ Suspicious activities.
* تعتبر الـ WAF logs هي الـ Source للـ Logs لرؤية كل الـ Web requests اللي حصلت، ولعمل Analyze للـ Detected web attacks أو الـ Blocked web attacks.
* أثناء فحص الـ Alerts اللي بتطلع من الـ Detected أو الـ Blocked attacks، لازم يتعمل Analyze للـ Reputation بتاعة الـ Source IP address اللي عمل الـ Log/alert، ولازم كمان يتعمل Investigate لأي Similar activities تانية الـ Source IP ده عملها في الـ Log sources التانية زي الـ IDS/IPS والـ Firewall.

## Sample log analysis

```
date=2022-01-26 time=19:47:26 log_id=20000008 msg_id=000018341360 device_id=FVVM08 vd="root" timezone="(GMT+3:00)Istanbul" timezone_dayst="GMTg-3" type=attack main_type="Signature Detection" sub_type="SQL Injection" severity_level=High proto=tcp service=https/tls1.2 action=Alert policy="Alert_Policy" src=19.6.150.138 src_port=56334 dst=172.16.10.10 dst_port=443 http_method=get http_url="?v=(SELECT (CHR(113)||CHR(120)||CHR(120)||CHR(118)||CHR(113))||(SELECT (CASE WHEN (1876=1876) THEN 1 ELSE 0 END))::text" http_host="app.letsdefend.io" http_agent="Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.9b1) Gecko/2007110703 Firefox/3.0b1" msg="Parameter(Password) triggered signature ID 030000136" signature_subclass="SQL Injection" signature_id="030000136" srccountry="Germany" attack_type="SQL Injection"
```

## &#x20;WAF Specific Fields&#x20;

* الـ http\_method الطريقة اللي استخدمها الattacker  في إرسال الـ Web request.
* الـ http\_url  الرابط المطلق اللي تم طلبه، وهنا واضح فيه الـ Payload الخبيث وجمل الـ SQL المستخدمة في الـ Injection.
* الـ http\_host : اسم الموقع أو الـ Application المستهدف من الهجوم.
* الـ http\_agent : بصمة المتصفح أو الأداة اللي المهاجم استخدمها وهو بيبعت الـ Request.
* الـ main\_type : الطريقة اللي الـ WAF قفش بيها الهجوم&#x20;
* الـ sub\_type و الـ attack\_type : تصنيف الـ Web attack اللي تم رصده بالظبط.
* الـ msg والـ signature\_id  تفاصيل الـ Rule اللي حصل لها Trigger، وهنا بتوضح إن الـ Parameter المستهدف كان اسمه Password.

## &#x20;HTTP Response Codes&#x20;

الـ Response codes بتساعد الـ Analyst يفهم إيه اللي حصل للـ Request لما وصل للـ Web Server، ودي التصنيفات الأساسية ليها:

* الـ Informational responses من (100–199)
* الـ Successful responses من (200–299): زي كود 200 (OK)، وده معناه إن الـ Request تم استقباله بنجاح والـ Response رجع للمستخدم.
* الـ Redirection messages من (300–399): زي كود 301 (Permanent Redirect)، وده معناه إن الـ Request حصل له Redirect لمكان تاني.
* الـ Client error responses من (400–499): زي كود 403 (Forbidden) ومعناه إن الوصول للداتا المطلوبة غير مسموح به، أو كود 404 (Not Found) ومعناه إن الـ Content المطلوب مش موجود.
* الـ Server error responses من (500–599): زي كود 503 (Service Unavailable) ومعناه إن الـ Server مش قادر يرد حاليًا.

بتطبيق الكلام ده على الـ Sample WAF Log اللي اتكلمنا عنه:

* الـ Connection request القادم من الـ IP address رقم `19.6.150.138` والمتجه للـ Port رقم `443` الخاص بالـ Host رقم `172.16.10.10` (الموجود خلف الـ WAF) تم التعرف عليه كـ Malicious بسبب الـ Expressions اللي في الـ URL، وبناءً عليه الـ WAF طلع Alert.
* الـ Policy المطبقة اسمها "Alert\_Policy" والـ Action بتاعها مضبوط على "Alert"، وده معناه إن الـ WAF شغال في الـ Monitoring mode (وضع المراقبة فقط وليس الحجب).
* بناءً على الـ Action ده، نقدر نستنتج إن الـ Request وصل بالفعل (reached) للـ Destination host (الـ Web Server)، وهنا لازم الـ Analyst يروح يشوف الـ Response code بتاع الـ Web server علشان يحدد هل الـ SQL Injection نجحت ولا لاء.

لو الـ Attack اللي الـ WAF بلغ عنه كان الهدف منه هو الـ Vulnerability detection (البحث عن ثغرات)، لازم الـ Analyst يركز في تفاصيل الـ Vulnerability دي ويقارنها بالـ Environment بتاعته:

* مقارنة الـ Technology: لو الـ Web application بتاعك شغال بـ ASP والـ Attack اللي مرصود عبارة عن Scan مخصص لـ PHP application، فمن الطبيعي إن الثغرة دي مش هتشتغل عندك والـ Impact هيكون منعدم.
* الـ Best Practice للـ Mitigation: بالرغم من إن الـ Scan ممكن يكون مش مؤثر على الـ Technology بتاعتك، إلا إن التصرف الصحيح هو اتخاذ إجراء ضد الـ IP address اللي بيعمل الـ Scanning activity.
* مكان الحجب (Blocking Location): أفضل إجراء يتم اتخاذه هنا هو عمل Block للـ Inbound requests بتاعة الـ IP ده عند أول جهاز أمني في الـ Gateway (زي الـ Perimeter Firewall)، وهو المكان اللي الـ Traffic الخارجي بيتفاعل مع الشبكة بتاعتك فيه لأول مرة.

## We can help use WAF logs when analyzing the following detections

&#x20;Detection of known web vulnerabilities

\- Detection of variety of web attacks like SQL Injection, XSS Attack, Code Injection, Directory Traversal

\- Detection of suspicious method usage such as PUT, DELETE

\- Top requesting IP address information

\- Most requested URL information

### الـ HTTP Request Methods الأساسية في الـ Web Traffic

الـ Request Method بتوضح إيه هو نوع الإجراء أو العمل اللي الـ Request بيطلبه داخل الـ Web language، وأهم الـ Methods دي هي:

* الـ GET: تُستخدم لاسترجاع الداتا (Retrieve data) من الـ Server.
* الـ POST: تُستخدم لإرسال الداتا (Send data) إلى الـ Server (مثل رفع الصور أو الفيديوهات أو بيانات الـ Forms).
* الـ DELETE: تُستخدم لحذف الداتا أو الملفات الموجودة على الـ Server.
* الـ PUT: تُستخدم لإرسال داتا إلى الـ Server، والداتا المرسلة دي بتقوم بعمل Create أو Update للملفات.
* الـ OPTIONS: تُستخدم لمعرفة وتحديد الـ Methods اللي الـ Server بيقبلها وبيسمح بيها (Tells which methods the server accepts).

<br>
