---
hidden: true
---

# linux

تمام خلينا نركز على **`/mnt`** بس ونوضحها بطريقة أبسط.

***

#### تخيل معايا:

عندك شقة (النظام بتاعك)، وجواها أوض (زي `/home`, `/etc`, `/usr` …).\
لكن ساعات بتستضيف **ضيف مؤقت** (فلاشة، هارد خارجي، CD).\
مش هتدي الضيف أوضة دائمة في الشقة… فبتعمله **مكان مؤقت يقعد فيه**.

المكان المؤقت ده هو **`/mnt`**.

***

#### وظيفته:

* **/mnt** = نقطة ربط (mount point).
* أي جهاز تخزين خارجي أو partition إضافي عايز توصله بالنظام، لازم "تعلقه" (mount) في نقطة.
* النقطة دي ممكن تبقى في أي مكان، بس بالعرف في Linux بيستخدموا `/mnt` أو `/media`.

***

#### مثال عملي:

معاك فلاشة موجودة في `/dev/sdb1`.\
لو عايز تفتحها:

```bash
sudo mount /dev/sdb1 /mnt
```

دلوقتي كل ملفات الفلاشة هتلاقيها لما تكتب:

```bash
ls /mnt
```

ولما تخلص، تفصلها:

```bash
sudo umount /mnt
```

***

يعني باختصار:

* **`/mnt`** مش للتخزين الدائم.
* هو زي "موقف انتظار مؤقت" لأي جهاز أو partition بتوصله.

***

تمام 👌 خلينا نلخصلك الموضوع كله في نقاط واضحة، بحيث تقدر تكلم أي حد في آخر سيشن وانت واثق:

***

### 🔹 File Descriptors & Redirection (ملخص سريع)

#### 1. الـ File Descriptors الأساسية:

* **0 = STDIN** → المدخلات (الكيبورد أو أي input).
* **1 = STDOUT** → المخرجات العادية (تظهر عالشاشة).
* **2 = STDERR** → رسائل الأخطاء.

***

#### 2. إعادة التوجيه (Redirection):

* **`>`** = يوجّه STDOUT لملف (ويكتب من جديد).
* **`>>`** = يوجّه STDOUT لملف (ويضيف عليه).
* **`&>`** (في bash) = يوجّه STDOUT + STDERR لملف.

***

#### 3. Pipes (|):

*   البايب يوصل **STDOUT** لأمر تاني كـ **STDIN**:

    ```bash
    ps aux | grep ssh
    ```
*   لو عايز تدخل الأخطاء كمان جوه البايب:

    ```bash
    command 2>&1 | other-command
    ```



**we have 2 commands to list the services opened ports**

netstat -tupln

-t: Show TCP ports.-u: Show UDP ports.-p: Display the program/process ID (PID) and name associated with each port.-l: Show only listening sockets (ports open and waiting for connections).-n: Show numerical addresses/ports (e.g., 127.0.0.1:80 instead of localhost:http).



ss -tuna

-t: Show TCP sockets. -u:  Show UDP sockets. -n: Display numerical addresses/ports (no name resolution).  -a: Show all sockets (both listening and non-listening).

### 🔹 1) **الفاصلة المنقوطة (;)**

* بتخلي الأوامر تتنفذ **ورا بعض**، بغض النظر الأمر الأول نجح أو فشل.
* يعني التانية هتشتغل حتى لو الأولى وقعت.

مثال:

```bash
mkdir test; cd test; touch file.txt
```

* هنا هيعمل فولدر، وبعدها يدخل فيه، وبعدها يعمل ملف.
* حتى لو `mkdir test` فشل (مثلاً الفولدر موجود أصلاً)، باقي الأوامر هتتنفذ.

***

### 🔹 2) **الـ AND (&&)**

* هنا الشرط إن الأمر الأول لازم **ينجح (exit status = 0)** علشان التاني يتنفذ.
* لو الأول فشل → التاني مش هيتنفذ.

مثال:

```bash
mkdir test && cd test
```

* هيدخل على `test` **بس لو** `mkdir` نجح.
* لو الفولدر موجود أصلاً (mkdir فشل) → مش هينفذ `cd test`.

***

### 🔹 3) **البايب (|)**

* مختلف شوية:
  * هنا مش مجرد تنفيذ ورا بعض.
  * النتيجة (STDOUT) بتاعة الأمر الأول بتروح كمدخل (STDIN) للتاني.

مثال:

```bash
ls -l | grep ".txt"
```

* `ls -l` بيطلع كل الملفات.



*   الـ output بيروح لـ `grep` اللي هيصفي بس الملفات اللي فيها `.txt`.تمام ✅ عملتلك مقارنة سريعة بين **wget** و **curl** في جدول صغير كـ _Cheat Sheet_:

    | العنصر                                | **wget**                | **curl**                                          |
    | ------------------------------------- | ----------------------- | ------------------------------------------------- |
    | الهدف الأساسي                         | تحميل ملفات من الإنترنت | التعامل مع أي بروتوكول (HTTP, FTP, SMTP …) + APIs |
    | البساطة                               | بسيط وسهل للتحميل       | أعقد شوية بس أقوى                                 |
    | استكمال التحميل (resume)              | ✔️ مدعوم                | ✔️ مدعوم                                          |
    | تحميل recursive (موقع كامل)           | ✔️ موجود                | ❌ مش مدعوم                                        |
    | التعامل مع APIs (POST, JSON, Headers) | ❌ محدود جدًا            | ✔️ قوي جدًا                                       |



systemd = جديد، أسرع، أقوى. | sysvinit = قديم.

ip a = الجديد. | ifconfig = القديم.

man = quick reference. | info = detailed docs.

dpkg = direct .deb. | apt = مستودعات + dependencies.





