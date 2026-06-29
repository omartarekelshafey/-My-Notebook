# IDS/IPS Log Analysis

### IDS vs IPS Concept

الـ Firewall  بيبص على البيانات من بره (IPs & Ports)  بس. أما الـ IDS/IPS فبيتميز بقدرته على فحص محتوى بالكامل (Deep Packet Inspection) ليعرف هل موجود  (Malware/Exploits) ولا لا .

#### الفرق بينهم

* نظام الـ IDS (Intrusion Detection System): يكتفي بـ  Detection
* نظام الـ IPS (Intrusion Prevention System): يقوم بـ Detection & Prevention

### Following information should be investigated in details when analyzing IDS/IPS logs

### 1. Attack Direction

* Inbound (من الخارج للداخل): محاولة اختراق خارجي تستهدف أنظمتك، وتحتاج للتأكد من صمود الدفاعات.
* Outbound (من الداخل للخارج): مؤشر خطر أعلى، لأنها تعني غالباً أن جهازاً داخلياً أصيب بالفعل ويحاول التواصل مع سيرفر مخترق خارجي (C2).

### 2. Severity Level

مؤشر درجة الخطورة يحدد سرعة التحرك:

* تصنيفات الخطورة المرتفعة (High / Critical) تعني أن الحدث ذو أهمية قصوى ويتطلب استجابة فورية.
* التنبيهات المرتفعة تكون نسبة الإنذار الخاطئ (False Positive) فيها منخفضة جداً مقارنة بالتنبيهات المنخفضة.

### 4. Port & Service Verification

التحقق من وجود الثغرة في البيئة الفعلية:

* يجب فحص ما إذا كانت الخدمة أو البرنامج المستهدف بالهجوم يعمل فعلياً&#x20;
* إذا كانت تعمل: ترفع الخطورة لـ Critical ويجب فحص الجهاز بالـ EDR للتأكد من عدم حدوث  (`Infection`).
* إذا لم يرد المستهدف: لو تبين أن السيرفر لم يرسل أي رد (No Response) للمهاجم، يتم حظر الـ IP المهاجم على الـ Firewall فوراً كإجراء وقائي.

### 5. Action Taken (Detection vs. Prevention)

معرفة النتيجة النهائية للحزمة داخل الشبكة:

* حالة الـ Blocked: إذا قام النظام بمنع الهجوم ومفهوش حركات تانية، يمكنك أخذ وقتك في التحقيق بمرونة لأن الخطر المباشر تم صده.
* حالة الـ Detected: إذا قام النظام بكشف الهجوم فقط دون حظره، فهذا يعني أن الترافيك الخبيث وصل للهدف. يجب هنا مراجعة كافة الطلبات الشبيهة فوراً وتطبيق حظر يدوي على الـ Firewall لحماية السيرفر طالما تأكدت أنه ليس False Positive.

هل تحب نطبق المنهجية دي على لوج عملي ونشوف إزاي هنمشي على الخمس خطوات دول بالترتيب؟

### Attacks Detected by IDS/IPS

* &#x20;(Port & Vulnerability Scanning).
* &#x20;(Code Injection) , (Brute-Force).
* (DoS/DDoS).
* &#x20;(Trojan & Botnet activities).

