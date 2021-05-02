---
description: shell scripting-də şərt və döngü operatorları
---

# 2 - şərt və döngü operatorları

`if`, `fi`, `then`, `else` komandaları, verilmiş şərt doğru olarsa, kodun çalışmasını təmin edən kombinasiyalardır. Şərtlər `[]` işarələri arasında verilməlidir. `[` və `]` işarələrindən həm əvvəl həm də sonra boşluq buraxılmalıdır.

If statement-ləri özündən sonra testlər qəbul edir:

hər hansı bir dəyişənin dəyərinin bərabərliyinin yoxlanması üçün iki fərqli yol seçmək olar:

`[ "$test" = 5 ]` dəyişəni cüt dırnaq içərisinə alıb 1 cüt kvadrat mötərizədən istifadə etmək. `[[ $test == 10 ]]` dəyişəni cüt dırnaqsız yazıb ümumi ifadəni cüt kvadrat mötərizədən istifadə edərək bağlamaqla.

Əgər ifdən sonra yazacağımız şeyi ifadə adlandırası olsaq,

`! ifade` Əgər ifade `False` olarsa True qaytarır. `( $test )` Əgər ifade `True` olarsa `True` qaytarır.

`ifade1 && ifade2` Hər iki ifadə `True` olarsa True qaytarır. `ifade1 || ifade2` İki ifadədən biri `True` olduqda `True` qaytarır.

Fayl tip testləri:

```text
Aşağıdakı testlər yalnız mövcud olan fayllar üçün True dəyəri qaytarırlar:

 -d file      True - əgər özündən sonra gələn fayl qovluq olarsa.
 -e file      True - əgər fayl mövcud olarsa
 -L file      True - əgər fayl symbolic link-dirsə
 -O file      True - əgər faylın sahibi hal-hazırki effektiv istifadəçi id-sidirsə.
 -r file      True - əgər fayl readable-dırsa.
 -s file      True - əgər faylın ölçüsü sıfırdan yuxarıdırsa.
 -w file      True - əgər fayl writable-dırsa. 
 -x file      True - əgər fayl executable
```

[https://ss64.com/bash/test.html](https://ss64.com/bash/test.html)

Faylın modification date-i ilə bağlı şərt operatorları:

```bash
file1 -nt file2     True - əgər file1 file2-dən yeni olarsa
file1 -ot file2     True - əgər file1 file2-dən köhnə olarsa
```

String-lərlə bağlı şərt operatorları

```text
    -z String      True - əgər stringin ölçüsü sıfır olarsa.
    -n String      True - əgər stringin ölçüsü sıfır olmazsa.
    String1 = String2     True - əgər stringlər bərabərdirsə.
    String1 != String2    True - əgər stringlər bərabər deyilsə.
```

Numeric tests 



```text
Numeric tests
    ARG1 -eq ARG2   True - əgər ARG1 ARG2-yə bərabər olarsa.
                    [[ 5 -eq 05 ]] && echo "5 equals 05"
    ARG1 -ne ARG2   True - əgər ARG1 ARG2-yə bərabər olmazsa.
                    [[ 6 -ne 20 ]] && echo "6 is not equal to 20"
    ARG1 -lt ARG2   True - əgər ARG1 ARG2-dən kiçik olarsa.
                    [[ 8 -lt 9 ]] && echo "8 is less than 9"
                    [[ 3 < 4 ]] && echo "3 is less than 4"
    ARG1 -le ARG2   True - əgər ARG1 ARG2-dən kiçik vəya bərabər olarsa.
                    [[ 3 -le 8 ]] && echo "3 is less than or equal to 8"
    ARG1 -gt ARG2   True - əgər ARG1 ARG2-dən böyük olarsa.
                    [[ 5 -gt 10 ]] || echo "5 is not bigger than 10"
                    [[ 4 > 2 ]] && echo "4 is greater than 2"
    ARG1 -ge ARG2   True - əgər ARG1 ARG2-yə bərabər və ya ondan böyük olarsa.
```

Bu nümunədə, -z ilə $1-in, yəni birinci arqumentin boş olub olmamasını yoxlayırıq, əgər boş olarsa, komputer then-in içinə girib oxumağa başlayır növbəti kodları. if ilə başlayan kod blokları fi ilə bitməlidir.

```bash
#!/bin/bash
if [ -z $1  ]
then
        echo "Arqument daxil olunmayib."
fi
exit 0

```

Aşağıdakı kod isə, çalışdırıldığı zaman daxil edilən arqumentin olub olmamasını yoxlayır, əgər varsa, həmin arqumentin qovluq olub-olmamasını yoxlayır.

```bash
#!/bin/bash
if [ -z $1  ]
then
        echo "Arqument daxil olunmayib."
elif [ -d $1 ]
then
        echo "Daxil etdiyiniz $1 bir qovluqdur."
else
        file $1
fi
exit 0
```



