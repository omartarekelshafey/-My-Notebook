# proxy log analysis

### Overview

مفهوم الـ Proxy هو عبارة عن وسيط (Bridge) بين الأجهزة الداخلية (Endpoints) وشبكة الإنترنت. الشركات بتستخدمه عشان تحسن سرعة الإنترنت، وتتحكم في المرور بشكل مركزي، وترفع مستوى الأمان.

#### Types of Proxies

* نوع الـ Transparent Proxy: السيرفر المستهدف بيقدر يشوف الـ IP الحقيقي للجهاز اللي بعت الطلب.
* نوع الـ Anonymous Proxy: السيرفر المستهدف مش بيشوف الـ IP الحقيقي، وبيظهرله الـ IP بتاع الـ Proxy بس، فبيحمي هوية المستخدم.

#### Sample Log Analysis&#x20;

عند تحليل اللوج ده: `action="blocked" url="https://android.prod.cloud.netflix.com/" urlsource="Local URLfilter Block" profile="Wifi-Guest" srcip=192.168.209.142`

* التحليل: جهاز داخل شبكة الـ Guests حاول يدخل على موقع Netflix، والـ Proxy منعه عشان الـ URL ده موجود في قائمة الحظر المحلية الخاصة بالشركة.

### Log Analysis & Logic

الـ Proxy بيتحكم في خدمات زي HTTP, HTTPS, FTP بناءً على سياسات محددة (Policies). المنطق الأساسي اللي شغال بيه هو إنه بيشوف الـ URL المطلوب ويكشف عليه في قاعدة بيانات التصنيفات (Category Database)، لو التصنيف خطر بيعمل Block، ولو سليم بيعمل Pass. كمان ممكن يطبق Implicit Deny لمنع الوصول لأي شبكة مش مسموح بيها صراحة

### Detection & Investigation

&#x20;ال Proxy logs   بتساعدنا في ايه :

\- Connections to/from suspicious URLs

\- Infected system detection

\- Detection of tunneling activities

<br>
