# correlation

#### 🧩 Rule-Based Threat Detection

* بيربط **حدث واحد بشرط واحد**.
* يعني: لو حصلت حاجة محددة → اعمل إنذار.
* مثال:
  * "لو في 3 فشل متتالي في تسجيل الدخول من نفس المستخدم → Alert."
  * هنا القاعدة مربوطة بـ **نوع Log واحد** (محاولات الدخول).

***

#### 🧩 Correlation-Based Threat Detection

* بيربط **أحداث متعددة من مصادر مختلفة** عشان يشوف الصورة الكبيرة.
* مثال:
  * "User عمل Login ناجح من مصر، وبعد 10 دقايق نفس الحساب عمل Login من أمريكا."
  * هنا SIEM بيربط بين **Logs من أنظمة مختلفة** (Authentication logs + GeoIP).
  * مثال تاني: "Firewall قال إن في اتصال غريب، وفي نفس الوقت الـ Endpoint قال إن فيه Process مشبوه."

***

📌 الفرق الأساسي:

* **Rule-Based** = حدث واحد + شرط مباشر.
* **Correlation-Based** = بيربط أحداث مختلفة من أكتر من مصدر → يطلع سيناريو ممكن يكون هجوم.

تحب أديك مثال عملي بالخطوات إزاي SIEM بيعمل correlation؟

***

## 🧩 **Basic Components of the Correlation Rule**

الـ **Correlation Rule** هو "عقل" الـ SIEM اللي بيربط الأحداث المختلفة ويحوّلها لسيناريوهات تهديد واضحة. عشان يشتغل صح، لازم نفهم مكوناته الأساسية:

***

### 1️⃣ **Source of Events and Data**

* ده الأساس: الـ SIEM بيجيب بياناته منين؟
* كل مصدر Logs بيضيف جزء من الصورة:
* **Network Logs** → محاولات اتصال، بورتات مفتوحة، حركة مرور مشبوهة.
* **System Event Logs** → محاولات دخول، تغييرات في الـ OS.
* **Application Logs** → أفعال المستخدمين (Login/Download/Delete).
* **Security Devices** → Firewall, IDS/IPS, Antivirus.
* **Threat Intelligence** → مؤشرات خارجية للهجمات (IP Malicious, Hashات معروفة).

📌 **أهمية الجزء ده**:

* بيحدد مدى وضوح الصورة عندك.
* لو جبت Logs كتير مالهاش لازمة → Noise / False Positives.
* لو قصّرت → مش هتشوف الهجوم كامل.

🧩 **مثال**:\
Firewall يقول: IP مشبوه → Windows يقول: نفس الـ IP حاول يدخل → Antivirus يقول: نفس الـ IP نزّل ملف غريب.\
📌 كل مصدر أضاف جزء للقصة.

***

### 2️⃣ **Basic Principle of Correlation Rule**

* هو المنطق اللي بيجاوب: **الـ Rule يشتغل إزاي؟**
* الفكرة = ربط أحداث متعددة ببعض عشان يطلع سيناريو تهديد.

📌 **مكوناته**:

* **Correlation of Events** → تجميع أكتر من حدث مرتبط.
* **Timestamp** → التوقيت مهم (مين حصل قبل مين).
* **Triggering** → يتفعل لما الشروط كلها تتحقق.
* **Response** → يدي Alert أو Action.
* **Improvement** → يتظبط مع الوقت عشان يقلل الإنذارات الغلط.

🧩 **مثال**:\
"3 Failed Logins → بعدها Login ناجح → بعدها محاولة تحميل ملف حساس."\
ده يديك سيناريو Brute Force → Data Theft.

***

### 3️⃣ **Conditions and Matching Conditions**

* الشروط هي اللي بتقول للـ Rule: "إشتغل دلوقتي."

📌 **أنواعها**:

* **Condition** → شرط واحد (Ex: User دخل Password غلط 3 مرات).
* **Matching Conditions** → أكتر من شرط مع بعض.

🔗 **Operators**:

* **AND** → لازم كل الشروط تتحقق.
* **OR** → يكفي واحد يتحقق.

📌 **Priority & Order** → أولوية تنفيذ الـ Rules لو أكتر من واحد اتفعل.

🧩 **مثال**:

* Condition1: أكتر من 5 Failed Logins.
* Condition2: بعدها Login ناجح من نفس IP.
* Condition3: يحصل كله في 5 دقايق.

***

### 4️⃣ **Triggering the Correlation Rule**

* اللحظة اللي الـ Rule بيتحوّل فيها من "مجرّد منطق" → لإنذار أو Action.

📌 **إزاي بيشتغل؟**

* لو الشروط كلها اتحققت + الأحداث مرتبطة بنفس الـ User/IP → Rule يتفعل.
* يتنفّذ Response: Alert للـ SOC، Block للـ IP، أو Action تاني.
* أولوية (Priority) عشان لو فيه Rules كتير.

🧩 **مثال**:\
بعد تحقق كل الشروط، الـ SIEM يطلع Alert:\
&#xNAN;**"Possible Brute Force Attack Detected on User: Admin"**.

***

