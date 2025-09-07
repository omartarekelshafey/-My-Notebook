# CH 4

## Acquisition process

### Why We Do Acquisition

ليه ماينفعش نشتغل على الـ Artifact  علي طول\
أول حاجة، لو اشتغلت على  الجهاز الأصلي، أي Tool هتشغلها سواء Portable أو لأ هتسيب أثر في الـ Memory وبالتالي البيانات الأصلية هتتغير. عشان كده لازم نعمل Acquisition ونشتغل بعيد عن المكنة الأصلية.

كمان في  Forensics  أهم ركن فيه هو  (Hypothesis). كل محاولة Analysis بتأثر على الـ Evidence، وده سبب إضافي ليه ماينفعش نشتغل على الأصل.

كمان في الـ Business Context، مفيش مؤسسة هتديك السيرفر الأساسي تقعد تشتغل عليه 5 أيام وتوقف البزنس. اللي بيحصل إنك بتاخد Image وتكمل شغلك في المعمل&#x20;

وأخيرًا، الـ Acquisition بيسمحلك تعمل أكثر من نسخة (Cloning) من نفس المصدر. النسخة الأصلية تتخزن بدون مساس، وانت تشتغل على نسخة تانية.

***

## Most Important Task for Acquisition

أول خطوة إننا نحدد الـ Acquisition Point:

* عايز أعمل Acquisition لإيه؟
* إيه الـ Tool المناسبة؟

Preservation

بعد ما نسحب الـ Artifacts لازم نطمن إنها ما اتلعبش فيها.\
أبسط طريقة: Hash Calculation.\
ناخد Hash للـ Image أو الملف اللي اتسحب، وزميلك في المعمل يعمل نفس الحساب ويقارن القيم. لو متطابقة يبقى مفيش تغيير.

***

## Order of Volatility

الـ Acquisition بيتم حسب مبدأ مهم اسمه **Order of Volatility**، والمبدأ العام: "ابدأ بالحاجة اللي بتضيع بسرعة، وانتهي بالحاجة الأكثر ثبات".

الترتيب بيكون كالآتي:

1. CPU Registers
2. CPU Caches
3. RAM
4. Hard Disk
5. External Storage



## Types of Acquisition

### Live Acquisition

الـ Live Acquisition لازم يحصل في وقت محدد وغالبًا في موقع الجريمة، عشان كده اسمه "لايف".\
الـ Live Acquisition للحاجات اللي فيها Volatility يعني ممكن تضيع بسرعة، زي الميموري.\
مثال: لو البي سي أو اللاب توب اللي حصل منه الـ Breach اتساب شغال ساعتين أو اتقفل، الميموري كلها هتتفور، والرام كمان هتروح.\
عشان كده لازم أعمل Live Acquisition قبل ما أقفل الجهاز أو أفصل الكهرباء.

### Static Acquisition

الـ Static Acquisition هو اللي ممكن يحصل في أي وقت.\
أكبر مثال: الهارد ديسك.\
الجهاز اتقفل أو اتفصلت الكهرباء؟ البيانات المكتوبة على الديسك هتفضل موجودة.\
ومن هنا في نوع خاص من الـ Static Acquisition بنسميه **Dead Acquisition**، وده معناه إني مش محتاج الأوبريتنج سيستم خالص.\
مثال: حد جابلي هارد ديسك، أخدت منه Full Clone (Bit-wise Copy) من غير ما أتعامل مع الجهاز أو الأوبريتنج سيستم اللي عليه.

هوضح كل حاجه عن الصوره دلوقتي

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

## Disk Acquisition&#x20;

### Full Acquisition

معناها باخد الـ Component كامل زي ما هو.

* لو عندي 16GB RAM → هاخد الـ 16GB كاملين.
* لو عندي Hard Disk 1TB → هاخد الـ 1TB بالكامل.

#### &#x20;  Disk to Image

إن الهارد يكون فيزيكال لكن أعمل له Acquisition على شكل Logical File (Image File).\
الميزة:

* ينفع أنقله على USB.
* أرفعه على Shared Storage.
* أقدر أخزن أكتر من هارد كـ Files على هارد واحد كبير.

#### &#x20;  Disk to Disk

إن الهارد الفيزكال يتنقل لهارد فيزكال تاني زي ما هو.\
العيوب:

* مكلف أكتر.
* محتاج هارد مماثل.\
  الميزة:
* More Secure لأن النقل بيكون مباشر Disk لـ Disk.

***

### Partial Acquisition

هو إني باخد جزء معين بس من الـ Component بدل ما أخده كله.

#### Logical Partial Acquisition

باخد ملفات معينة عن طريق الأوبريتنج سيستم.\
مثال: في Email Forensics → بدل ما أخد السيرفر كله، هاخد Mailbox محدد.\
العيب:

* لو في ملفات Deleted مش هقدر أرجعها.
* أنا مش بعمل Copy من الميديا نفسها، أنا باخد ملفات Logical فقط.

#### Sparse Partial Acquisition

الفرق هنا إني باخد Sectors أو Blocks من الهارد بدل الملفات.\
الميزة:

* أقدر أرجّع الـ Deleted Files لأن السكتور اللي باخده بيحتوي على الداتا حتى لو كانت متعلم عليها إنها محذوفة.
* لازم أكون عارف أي Sectors أو Blocks محتاج أسحبها.

## Copying vs Cloning

عشان نفهم الفرق ما بين الـ Copying والـ Cloning، تخيل إن عندك ديسك فيه بيانات:

* لما تعمل Copying: الأوبريتنج سيستم بياخد الملفات اللي شايفها بس، مش هيعرف ينسخ الداتا اللي في الـ Unallocated Space.
* لما تعمل Cloning (Imaging): هنا بيت  نسخ  كل البايتس على الديسك زي ما هي، سواء الأوبريتنج سيستم شايفها أو لأ.\
  وده بيسمح نرجّع ملفات معمول لها Deleted لأن البايتس لسه موجودة.

***

## Disk to Image Acquisition

لما نعمل Disk to Image Acquisition، بيطلع عندنا أكتر من نوع من الـ Images:

### Raw Format

* بياخد البايتس زي ما هي، من غير Metadata أو Compression.
* الميزة: سريع جدًا وبيعمل Ignore لأي Error&#x20;

### Proprietary Formats

دي فورمات بتعملها شركات معينة، وهي Closed Source.\
المشكلة: محكومة بالأدوات بتاعة الشركة نفسها.

أمثلة:

* EWF  → Expert Witness Format (شركة EnCase).

IDIF→ used by i look investgator

* SGZIP → شركة pyFlag

### Advanced Forensic Format (AFF)

* Open Source، وأصبح الـ Standard في المجال.
* مدعوم من معظم الأدوات&#x20;

مميزاته:

* ممكن تعمله Compression.
* ممكن تضيف Metadata (معلومات عن الحالة/الـ Acquisition).
* ممكن تقسمه لأكتر من ملف (Splitting) عشان تسهّل النقل أو التخزين.

بيتكون من فايلين:

* .afd → Advanced Forensic Data.
* .afm → Advanced Forensic Metadata.

## Things to Consider During Acquisition

### Disk Size

أول حاجة لازم تاخد بالك منها السايز بتاع الديسك اللي هتعمل منه Image.\
ليه؟ عشان يبقى معاك ميديا كافية تسحب عليها الـ Image الجديدة.

### Compression

* لو هتستخدم Compression، لازم تتأكد إنه **Lossless Compression**.
*   ما ينفعش تستخدم **Lossy Compression** في الـ Forensics

    **Lossy Compression**بيشيل داتا شايفها مكررة.

    * ده يغير شكل الديسك الأصلي.
    * ممكن يضيع Deleted Files أو Hidden Files.
    * وكمان الخصم في المحكمة ممكن يشكك في مصداقية الـ Image.
* لذلك، لازم التول اللي بتستخدمها تكون بتعمل Lossless Compression زي inCase أو iLook.

### Time Factor

* خد بالك من الوقت اللي هتعمل فيه الـ Acquisition.
* أي كتابة بتحصل على الديسك بعد كده مش هتكون موجودة في الـ Image.
* الـ Image اللي اتاخدت بتكون  Backup Version.
* ما تشتغلش على الـ Image الأصلية، اعمل منها Clone، والـ Clone هو اللي تشتغل عليه.

### Multiple Acquisition Methods

* حاول تعمل Acquisition بطريقتين مختلفتين (Tools أو Formats).
* الهدف: لو حصل تشكيك في المحكمة، تقدر تثبت إن الطريقتين أدوا نفس النتيجة.
* ده يقلل احتمالية وجود خطأ لأقصى درجة.

### Encryption

* لو الديسك معمول له Encryption، لازم تتأكد إن الكيز معاك.&#x20;
* لازم تحفظ الكيز أو حتى الهاردوير اللي بيعمل Unlock.
* اتأكد إن أي Sector محمي أو Secure يتم أخده بالكامل

