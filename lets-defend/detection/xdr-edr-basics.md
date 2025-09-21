# XDR/EDR Basics

## XDR/EDR Introduction

### Endpoint Detection and Response (EDR)

EDR ببساطة هو نظام حماية للمنطقة الأخيرة (الـ endpoints) في الشبكة، زي أجهزة الكمبيوتر والسيرفرات والموبايلات. شغله إنه بيراقب اللي بيحصل على الأجهزة دي، ولو لقى أي حاجة غريبة أو خطر، بيعرفها بسرعة وبيتصرف عشان يوقفها.

* File and Process Monitoring: بيراقب الملفات والبرامج اللي شغالة على الجهاز عشان يلقط أي تصرف مش طبيعي.
* Behavior Analysis: بيفهم التصرفات الطبيعية للمستخدمين والبرامج، ولو حصل حاجة شاذة، بيكتشفها على طول.
* Malware Detection: بيكتشف الفيروسات والبرامج الضارة وبيوقفها.
* Indicator of Compromise (IOC) Detection: بيستخدم معلومات عن هجمات سابقة عشان يلقط أي حاجة معروفة ومشبوهة.
* Event Log Analysis: بيحلل logsالأحداث على الجهاز عشان يفهم اللي حصل بشكل أعمق.
* Threat Intelligence Integration: بيستفيد من مصادر معلومات خارجية عشان يكون على علم بآخر التهديدات.
* Post-Monitoring Action Capabilities: بيديك الأدوات اللازمة عشان تتصرف بسرعة وتوقف أي هجمة.
* Network Monitoring: بعض أنظمة الـ EDR ممكن تراقب حركة الإنترنت على الجهاز.
* Data Protection and Encryption: بعضها بيقدر يحمي البيانات عن طريق التشفير.

### eXtended Detection and Response (XDR)

XDR هو النسخة الأقوى والأشمل من EDR. الفكرة هنا إنه مش بيركز على الأجهزة بس، لأ، ده بيجمع معلومات من كل حتة: الأجهزة، الشبكة، الكلاود، وكل مصادر الحماية التانية، وبيقدر يشوف الصورة الكاملة.

* Multiple Data Source Integration: بيجمع بيانات من مصادر مختلفة عشان يكون عنده رؤية واسعة.
* Threat Correlation and Analysis: بيربط بين البيانات دي عشان يفهم الهجمة بالكامل من أولها لآخرها.
* Automatic Threat Detection: بيستخدم الذكاء الاصطناعي عشان يكتشف الأخطار بشكل آلي.
* Threat Chain Analysis: بيتابع الهجمة من أول ما بدأت لغاية ما وصلت فين، وده بيساعد في فهم الهجمات المعقدة.
* Automatic Response Capabilities: بيقدر يتصرف لوحده عشان يوقف التهديدات من غير ما حد يتدخل.
* Threat Intelligence Integration: بيستخدم أحدث معلومات عن الأخطار عشان يحضر للمستقبل.
* Incident Management and Analysis: بيساعدك تدير وتحلل كل الأحداث الأمنية بشكل شامل.
* Comprehensive Reporting: بيقدم تقارير مفصلة عشان تفهم الوضع الأمني كله.

### What is the difference between iDS, IPS and EDR?

| **Primary Function**  | Detects malicious activity and alerts security personnel.          | Detects and prevents malicious activity.                                      | Detects, investigates, and responds to threats on endpoints.                                        |
| --------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Deployment**        | Typically out-of-band, monitoring network traffic passively.       | Inline, actively inspecting network traffic.                                  | Agent-based, deployed on individual endpoints (laptops, servers, etc.).                             |
| **Scope**             | Primarily network-focused; can also be host-based (HIDS).          | Primarily network-focused; can also be host-based (HIPS).                     | Endpoint-focused; provides deep visibility into endpoint activity.                                  |
| **Data Source**       | Network traffic, system logs.                                      | Network traffic.                                                              | Endpoint activity data (file access, process execution, network connections, registry changes).     |
| **Detection Methods** | Signature-based (known attacks), anomaly-based (unusual behavior). | Signature-based, anomaly-based.                                               | Behavioral analysis, machine learning, threat intelligence.                                         |
| **Response**          | Passive; relies on human intervention or other systems.            | Active; automated threat blocking and mitigation.                             | Automated or manual responses, including isolation, quarantine, remediation.                        |
| **Visibility**        | Limited visibility into endpoint activity.                         | Limited visibility into endpoint activity.                                    | Comprehensive visibility into endpoint activity.                                                    |
| **Focus**             | Identifying and reporting potential threats.                       | Preventing threats from reaching their target.                                | Investigating and responding to threats that have bypassed other defenses.                          |
| **Strengths**         | Early threat detection, security awareness, compliance.            | Proactive threat prevention, real-time protection.                            | Comprehensive endpoint visibility, advanced threat detection, rapid response, threat hunting.       |
| **Weaknesses**        | Passive monitoring, prone to false positives, evasion techniques.  | Can impact network performance, prone to false positives, evasion techniques. | Requires agent deployment, can be complex to manage, potential for performance impact on endpoints. |
| **Relationship**      | IDS can complement IPS by providing additional alerting.           | IPS builds upon IDS by adding prevention capabilities.                        | EDR complements IDS and IPS by focusing on endpoint protection and advanced threat detection.       |
| **Example Tools**     | Snort, Suricata, Zeek (formerly Bro)                               | Cisco Firepower, Palo Alto Threat Prevention, Check Point IPS                 | Microsoft Defender for Endpoint, CrowdStrike Falcon, SentinelOne                                    |



## EDR/XDR Installation and Configuration Process

تمام يا أنور ✌️\
أنا هظبطلك الكلام في شكل ملخص مرتب تقدر تحطه في **GitBook** من غير الحشو النظري الممل، واللي يدي Overview كامل عن SentinelOne Installation & Configuration.

***

## SentinelOne Installation & Configuration

### 1. Introduction

* SentinelOne بيوفر **EDR/XDR** للحماية والكشف والاستجابة.
* Hosted بالكامل على **Cloud** → مش محتاج Servers On-prem.
* بعد شراء الترخيص بتدخل على **Management Console** (Portal).

***

### 2. Interface Overview

#### Dashboard

* إحصائيات التهديدات والأنشطة الأخيرة.
* Status بتاع الـ Agents والسياسات.
* رسومات بيانية للـ Threat Trends.

#### Visibility&#x20;

* Threat Hunting & Investigation.
* تفاصيل عن الـ Attack Vectors, Tools, Affected Systems.

#### Sentinels

* إدارة الـ Endpoints.
* سياسات (Policies).
* Rules, Blocklists, Exclusions.
* Network & Device Control.
* Agent Installation Packages & Updates.

#### Incidents

* ملخص وتحليل للحوادث الأمنية.
* Source, Affected Devices, Attack Vectors, Severity.
* Recommended & Automated Response Actions.

#### Applications

* تفاصيل البرامج اللي شغالة على الأجهزة.
* Version, Vulnerabilities, Security Status.

#### Activity

* كل الأحداث والأنشطة (Threat Response, Updates, Logs, Network, Apps).
* البحث حسب وقت أو جهاز محدد.

#### Reports

* تقارير دورية أو لمرة واحدة.
* Threats, Agents, Compliance, Incidents.
* Customizable (وقت/منطقة/جهاز/نوع تهديد).

#### Settings

* إعدادات الـ Console, Users, Notifications, Syslog, System Settings.

***

### 3. First Configuration

#### Identify Sites & Groups

* Hierarchy: **Account > Site > Groups**.
* كل Site/Group ممكن يكون له سياسات وصلاحيات مختلفة.
* مثال: مؤسسة عالمية → Sites (دول) → Groups (أقسام IT, Sales…).

#### Set Policies

* Location: `SentinelOne > Account/Site/Group > Sentinels > Policy`.
* إعداد الـ Policies حسب المستوى (Account/Site/Group).

**Modes**

* **Detect Mode**: يراقب ويبلغ بس.
* **Protect Mode**: يمنع ويعزل تلقائي.

**Actions**

* **Kill & Quarantine**: إيقاف Process خبيث + عزل ملف.
* **Remediate**: إصلاح التغييرات (Users, Settings).
* **Rollback**: استرجاع قبل الهجوم (خصوصًا ضد Ransomware، ويندوز فقط).

***

### 4. Agent Policies

* **Anti-Tamper**: يمنع إزالة/تعديل الـ Agent.
* **Snapshots**: حفظ حالة النظام قبل/بعد الهجوم (Windows Shadowcopy).
* **Logging**: لوجات مفصلة للتحليل وIncident Response.
* **Scan New Agents**: Full Scan عند التثبيت الأولي.
* Notifications & UI Options للـ End Users.

***

### 5. Deep Visibility

* جمع بيانات موسعة لدعم Threat Hunting & IR.
* تفاصيل العمليات، الشبكات، الملفات، الذاكرة.
* حجم البيانات بيختلف حسب النسخة والإعدادات.

***

### 6. More Options

* **Decommissioning**: إزالة Agent نهائيًا (يدوي/تلقائي).
* **Remote Shell**: Powershell (Windows) / Bash (\*Nix) بإذن Admin.

***

### 7. Identify Exclusions

*   types of Exclusions

    * **Hash**
    * **Path**
    * **Certificate**
    * **File Type**
    * **Browser**



تمام يا أنور 👌\
أنا هظبطلك الكلام في شكل **ملخص مرتب** تحطه في GitBook، من غير الحشو، بحيث يدي Overview كامل عن **Managing Endpoints with EDR/XDR (SentinelOne)**.

***

## Managing Endpoints with EDR/XDR

### 1. Importance of Endpoint Management

* **Deployment**: توزيع Agents يدويًا، عن طريق Group Policy، أو Remote Deployment Tools (زي SCCM).
* **Visibility**: متابعة حالة كل جهاز، السياسات المطبقة، والعمليات اللي شغالة.
* **Threat Detection**: كل Endpoint ممكن يبقى Vector للتهديدات → الإدارة بتسهل الكشف المبكر.
* **Response**: عزل الأجهزة المصابة ومنع الانتشار.
* **Policy & Updates**: ضمان تطبيق السياسات والتحديثات الأمنية باستمرار.

***

### 2. SentinelOne Endpoint Management

* **المكان**:\
  `SentinelOne > Account/Site/Group > Sentinels > Endpoints`
* تقدر تعمل:
  * مشاهدة الأجهزة المتصلة.
  * إدارة السياسات الخاصة بكل Endpoint.
  * الدخول على **Actions Menu** لكل جهاز (Isolation, Scan, Update, Uninstall…).
* تقدر تعمل **Star** للأكشنز اللي بتستخدمها كتير عشان تبقى سريعة الوصول.

***

### 3. SentinelOne Endpoint Agent Install

* **الخطوات**:
  1. الدخول على:\
     **SentinelOne > Account/Site/Group > Sentinels > Packages**.
  2. تختار الـ OS (Windows / Linux / macOS).
  3. تنزل الـ Package + Token الخاص بالموقع (Site).
  4. تشغل الـ Installer بـ Admin Rights.
  5. تدخل الـ Token وتضغط **Install**.
  6. تعمل **Reboot** عشان الـ Engines تشتغل بشكل كامل.
* بعد التثبيت الجهاز بيظهر في:\
  `Sentinels > Endpoints`.

***

### 4. SentinelOne Endpoint Agent Uninstall

* الـ **Anti-Tamper** بيمنع إزالة أو تعطيل الـ Agent من المستخدم.
* الإزالة بتتم فقط من الـ Console:\
  `Sentinels > Endpoints > Select Endpoint > Actions > Uninstall`.

***

تمام يا أنور ✌️\
هظبطلك الكلام في **ملخص مرتب** تحطه على GitBook يدي Overview عن **Data Sources & Log Integration in XDR**.

***

## Data Collection and Log Integration for XDR

### 1. Data Sources

* **Network Traffic Information**
  * IDS/IPS Logs, NetFlow, Network Monitoring Tools.
  * بيساعدوا في اكتشاف السلوك غير الطبيعي.
* **Endpoint Data**
  * من EDR: OS Events, Processes, File Activities.
* **Application Logs**
  * Logs من التطبيقات → كشف هجمات موجهة أو أنشطة Malware.
* **Cloud Services Logs**
  * من التطبيقات والخدمات السحابية → توسّع قدرات الـ XDR في الكشف.
* **Email Logs**
  * مفيدة لكشف Phishing, Malicious Attachments.
* **Sandboxing & Malware Analysis**
  * تحليل ديناميكي للملفات/الروابط المشبوهة.
* **Threat Intelligence**
  * IPs, Domains, Hashes خبيثة من مصادر خارجية.
  * تزود قدرة الكشف وتقلل الـ False Positives.

***

### 2. Log Integration

* **Automated Integration**
  * أغلب الـ XDR تدعم Integrations جاهزة عبر **APIs** مع منتجات أمنية، أجهزة شبكة وخدمات سحابية.
  * بتخلي جمع وتحليل البيانات أوتوماتيك.
* **Customized Integration**
  * للأنظمة أو التطبيقات المخصصة.
  * Manual API Integration أو Log Senders مخصصين.
  * بيستخدم في حالات مش مدعومة Out-of-the-box.

***

### 3. Data Enrichment, Storage & Querying

* **Enrichment**: ربط البيانات بمصادر إضافية (Threat Intel DBs, GeoIP, User Credentials).
* **Storage**: منصات XDR بتوفر تخزين واسع النطاق للـ Logs/Events.
* **Querying**: بحث سريع وفعال  أساسي في Threat Hunting & Incident Investigation.

***



\


### &#x20;
