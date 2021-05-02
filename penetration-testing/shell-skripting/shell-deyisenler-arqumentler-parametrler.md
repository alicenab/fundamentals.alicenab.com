# 1- dəyişənlər, arqumentlər, parametrlər

Bash skriptləri adətən \#! “shebang”-la başlayır. Faylın əvvəlindəki \#! işarələri, fayl execute olunduqda hansı interpreterlə işləyəcəyini təmin etmək üçün yararlı olur.  
Bash scriptlərini aşağıdakı iki üsulla çalışdırmaq mümkündür:  


```bash
bash faylın_adı.sh
./faylın_adı.sh
```

  
Həmçinin onu da nəzərinizə çatdırmaq istəyirəm ki, "faylın\_adı.sh" faylına execute icazəsi vermədən onu ikinci üsulda olduğu kimi işlətmək mümkün olmayacaq. “faylın\_adı.sh” faylına execute icazəsi vermək üçün aşağıdakı əmri daxil etmək kifayətdir:

```bash
chmod +x faylin_adi.sh
```

shell skript faylının içində \# işarəsindən sonra yazılan hər şey komment sayılır.  
Linuxda müxtəlif shell-lər mövcuddur. Onlara bash, zsh, ksh və s. misal gətirmək mümkündür. Onların hərəsi bir birindən xırda xüsusiyyətlərlə fərqlənirlər.

Skript faylının işə düşməsi halında, komment-lər \(yəni \# işarəsi ilə başlayan sətirlər\) işə düşmür.  
Kommentlərdən kod yazarkən həmin hissəni nəyə görə yazdığınızı digər şəxslər başa düşsün deyə, vəya,  
ümumi proqramın istifadə qaydalarını izah etmək üçün istifadə edə bilərsiniz.

Dəyişənlər \(variables\):  
Dəyişən nədir?  
İstifadəçi tərəfindən daxil olunan dəyəri\(hərf,rəqəm və s.\), komputerin RAM yaddaşında boş olan bir əraziyə sizin təyin etdyiniz adla etikətləyir. Yəni, siz dəyişənə bir dəyər təyin etdyinizdə, məsələn:

```bash
menimYasim=13
```

  
Komputer 13 ədədinin yaddaşda neçə bit yer tutacağını təyin edir, bundan sonra komputerin RAM yaddaşının boş olan bir hissəsində həmin ölçü qədər yaddaş ərazisini rezervləyir. Rezervlədiyi yeri və həmin yerin adresini götürüb, sizin daxil etdiyiniz ədədi \(yəni 13-ü\) ikilik say sistemində komputerin RAM-ında rezervlədiyi yerdə yadda saxlayır. Bundan sonra siz həmin dəyişəni, məsələn "menimYasim" dəyişənini çağırdıqda, komputer artıq "menimYasim"-a aid olan ədədin RAM-dakı adresi və "menimYasim"-in ölçüsünü bildiyi üçün bildiyi üçün, həmin adresə müraciət edərək, sizin istədiyiniz əməliyyatı edir.

Dəyişənlərin adı hərf və ya \_ işarəsi ilə başlaya bilər. Bunlardan sonra isə, hər hansı rəqəm gələ bilər.  
Shell, bütün dəyişənləri default olaraq string tipində tanıyır.  
Dəyişəni tanımlayarkən, = \(bərabərdir\) işarəsinin hər iki tərəfində də boşluq buraxmamağa diqqət etmək lazımdır. Bərabərliyin sol tərəfində yazdığımız ad tamamilə bizim istəyimizə bağlı olsa da, linux əmrləri ilə eyni olamasına diqqət yetirmək lazımdır. Kodun oxunması zamanı komputer ilkin olaraq bərabərliyin sağ tərəfini oxuyur, onu hesablayıb cavabını çıxardır bundan sonra isə həmin cavabı bərabərliyin sol tərəfindəki dəyişənə təyin edir.

Dəyişənin tanınmasına nümunə olaraq aşağıdakı misalı göstərmək olar:



```bash
menimAdim="Ali"
```

Beləliklə artıq "menimAdim" dəyişəninin dəyəri "Ali"-dir.

Bir də konstant dəyişənlər mövcuddur. Konstant\(sabit\) dəyişən, ilkin təyin olunan qiymətini heçvaxt dəyişmir. Ölçü vahidləri ilə bağlı iş görərkən konstant dəyişənlərdən istifadə etmək mümkündür.  
Konstant dəyişənləri aşağıdakı formada təyin etmək mümkündür:



```bash
declare -r pi=3.14
```

Gəlin "eded1" və "eded2" dəyişənlərinə\(variables\) yeni dəyərlər\(values\) təyin edək:



```bash
eded1=6
eded2=2
```

Sadə toplama, çıxma, vurma və bölmə riyazi hesablamalarını aşağıdakı formada etmək mümkündür:

```bash
eded3=$((eded1+eded2))
eded4=$((eded1-eded2))
eded5=$((eded1*eded2))
eded6=$((eded1/eded2))
```

Bəli, təxmin etdiyiniz kimi, riyazi hesablamaları `$(( ))` içində etmək lazımdır.

Ədədin kvadrata yüksəldilməsi və modulunun\(bölmə əməliyyatından sonraki qalığa deyilir\) çıxarılması isə aşağıdakı formda həyata keçir:

```bash
eded7=$((eded1**eded2))
eded8=$((eded1%eded2))
```

Dəyişəni stdout-a yəni ekrana \(terminalın çıxışına, terminalda ekranda gördüklərimiz\) vermək üçün, aşağıdakı əmrləri yazmaq kifayətdir:

```bash
echo "$eded3"
echo "$eded4"
echo "$eded5"
echo "$eded6"
echo "$eded7"
echo "$eded8"
```

Bash skriptlərinin sonu adətən

```bash
exit 0
```

əmri ilə bitir. "exit 0" əmri skriptin müvəffəqiyyətlə və səhvsiz başa çatdığını göstərir.  
sonu "exit 0" ilə bitən hər hansı bir skripti çalışdırdıqdan sonra, terminalda

```bash
exit 0
```

yazdıqda sizə cavab "0" verirsə, deməli həmin kod səhvsiz çalışıb bitib.

Əgər çalışdırıldıqda terminala alt-alta yazılmasını istədiyiniz bir neçə sətir varsa, hər bir sətri ayrıca "echo" komandası ilə ekrana çıxartmaq yerinə, kodun daxilində:



```bash
cat << END
hemin setirleri
bu cur
alt-alta
yaza bilersiniz
END
```

\* İstifadəçidən inputun alınma yolları

Skripti işə saldıqda, arqumentlər istifadə oluna bilər. Arqument nədir? Skripti çalışdırarkən faylın adından sonra yazılan istənilən şey arqument sayılır. Məsələn:

```bash
menimSkriptim.sh test test2 test3
```

bu terminal əmrində test, test2 və test3 "menimSkriptim.sh" skriptinin arqumentləri sayılır.

Kodun daxilində, skriptin arqumentlərinə $1 $2 $3 və s. çağıraraq əlçatmaq mümkündür. Məsələn aşağıdakı kodu:

```bash
#!/bin/bash
echo $1 $2 $3
```

aşağıdakı əmr ilə çalışdırıldığını fərz edək:

```bash
./test.sh a bb ccc dddd
```

Bu zaman terminalda aşağıdakı stdout yazısını görəcəyik:  
`a bb ccc`

əmr-dən də məlum olduğu kimi, bizim 4 arqumentimiz var idi: a, bb, ccc, dddd.  
ancaq kodun daxilində onlardan üçünü çağırmışdıq: $1, $2, $3  
Buna görə də, dddd arqumenti ekrana yazılmadı.

Skript kodun daxilində  
`$#` - skript çalışdırılarkən daxil edilən arqumentlərin sayını ;  
`$@` - skript çalışdırılarkən daxil edilən arqumentlərin siyahısını özündə daşıyır.

Məsələn, aşağıdakı "skript.sh" adlanmış kod faylını nəzərdə tutaq:

```bash
#!/bin/bash
echo "Arqumentlerin sayi: " $#
echo "Arqumentlerin siyahisi: " $@
```

Bu kod faylı aşağıdakı əmrlə çalışdırıldığı zaman:  
`./skript.sh qq www eeee rrrrr`

Terminala bu yazılar çıxacaq:

`Arqumentlerin sayi: 4  
Arqumentlerin siyahisi: qq www eeee rrrrr`

İstifadəçidən daxil olunası yazını arqument yolundan başqa READ əmri vasitəsi ilə də almaq mümkündür:

```bash
#!/bin/bash
echo "Istifadeci adi ve sifresinizi daxil edin: "
read -t 3 -p 'Istifadeci adi: ' istifadeciAdi
read -t 3 -sp 'Sifre: ' istifadeciSifresi
# -t timeout ucundur, verilmis saniye erzinde daxiletme olmasa failure qaytarib novbeti setre kecir.
# -p yeni setre kecmeden istifadeciden daxiletme isteyir.
# -s istifadecinin daxiletmesini ekrana yazmamaq ucun istifade olunur. Sifreler ucun elverislidir.
#buradaki `echo ""` emri bir setir asagi dusmek ucun istifade olunub.
echo ""
echo "Ad soyad ata adi: "
# read vasitesi ile eyni vaxtda bir nece meluamati almaq mumkundur:
read istifadeciAdi istifadeciSoyadi istifadeciAtaAdi
echo "Sizin adiniz: $istifadeciAdi"
echo "Sizin soyadiniz: $istifadeciSoyadi"
echo "Sizin atanizin adi: $istifadeciAtaAdi"
exit 0
```

İstifadəçidən məlumatı almağın digər yolu isə stdin vasitəsi ilə başa gəlir. Linuxda pipe\(\|\) komandası çox istifadə olunduğuna görə, fayllarla işləyərkən bu metod çox köməyə çatır.

adlar.list adında, içində aşağıdakı məlumatlar olan bir fayl olduğunu fərz edək:

`filankesov5 filankes5 filankesoglu5  
filankesov1 filankes1 filankesoglu1  
filankesov3 filankes3 filankesoglu3  
filankesov4 filankes4 filankesoglu4  
filankesov2 filankes2 filankesoglu2`

Xüsusi bir kod vasitəsi ilə, bütün ad soyad ata adı məlumatlarını oxuyub, onlardan adları əlifba sırasına görə sıralaya bilərik:



```bash
#!/bin/bash
# ASA melumatindan Adlari siralayan kod
# Istifade qaydasi:
# Icinde ASA melumatlari olan fayl bu koda pipe olunmalidir.
# Burada cut əmri vasitəsi ilə delimiter(ayırıcı) olaraq boşluq(spacebar) təyin edərək, ad soyad və ata adını bir # # birindən ayırmışıq. -f field deməkdir. ad soyad və ata adı bizə 3 field verir:
# 1) soyad
# 2) ad
# 3) ata adi
# bizə bunların arasından adı sıralamaq lazım olduğuna görə, 2-ci field lazımdır. Adları sıralamaq üçün sort # # əmrindən istifadə etmək mümkündür.
cat /dev/stdin | cut -d" " -f 2 | sort
exit 0
```

Həmin kodu aşağıdakı şəkildə işlətmək lazımdır:  
`cat adlar.list | ./test.sh`

Kod çalışdırıldıqda aşağıdakı nəticəni əldə edəcəyik:

`filankes1  
filankes2  
filankes3  
filankes4  
filankes5`

