# bash script

```bash
 علشان اخلي الاسكربيت يتعمله run ب shell معين بكتب كده
#! بكتب ال shebang  وبعدها ال path   بتاع ال Shell  اللي انا عايزها 
#!/bin/bash
طب انا لو مش عارف مكان الshell معين فين اعمل ايه بتسخدم ال command هو بيروح يدور علي الshell اللي انت عايزه
مثلا بدور python3 تكتب كده
#!/bin/env python3
 stringاي حاجه جوه ال single quote  بتعامل معامله ال 
  stringاي حاجه جوه ال single quote  بتعامل معامله ال 
  علشان اعمل Access لvariable لازم استخدم ال $
```

<pre class="language-bash"><code class="lang-bash">ده ال syntax  علشان اكتب if
<strong>age=20
</strong>
if [ $age -ge 18 ]; 
then
  echo "welcome in men world"
fi
ده ال syntax  علشان اكتب else
age=10

if [ $age -ge 18 ];
 then
  echo "welcome in men world"
else
 echo "you are kid go out"
fi
ده ال syntax  علشان اكتب elif
age=10

if [ $age -ge 18 ];
 then
  echo "welcome in men world"
elif [ $age -ge 10 ]; 
then
 echo "you are kid go out"
fi

syntax for loop
for name in ahmed mohamed mostafa 
do
echo "hello $name "
done


</code></pre>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>



