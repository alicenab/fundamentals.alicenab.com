---
description: >-
  Salam, bu yazıda virtualizasiya, hypervisor-lar və fərqlilikləri,
  container-lər və container engine-lər haqqında məlumat alacaqsınız.
---

# Virtualization və containerization nədir?

## Virtualizasiya nədir?

Virtualizasiya bir komputer sisteminin içində eyni anda bir vəya bir neçə əməliyyat sisteminin fəaliyyət göstərməsinə deyilir. Komputer sahəsində insanların virtualizasiyadan istifadə etməsinin bir neçə səbəbi var. 

Adi desktop istifadəçilərinin virtualizasiyadan istifadə etmək səbəbi, başqa əməliyyat sistemində istifadəsi nəzərdə tutulmuş proqramları işlətməkdir. Bu zaman, desktop istifadəçiləri həm əlavə komputerdən istifadə etmək ehtiyacından, həm də hazırki əməliyyat sistemi ilə "dualboot" rejimdə digər əməliyyat sisteminə keçmək üçün komputeri söndürmək məcburiyyətindən xilas olurlar.

Həmçinin sistem administratorları üçün də virtualizasiyanın istifadəsi bir neçə əməliyyat sisteminin eyni anda istifadəsi şəraitini  yaradır. Ancaq sistem administratorların virtualizasiyadan istifadə etməyinin əsas səbəbi serverin resurslarını daha effektiv şəkildə istifadə etməkdir. Məsələn: Əgər 32gb ram-a sahib olan bir serveriniz varsa və sistemdə max 8gb ram işlədəcək oloan 3 fərqli sistemin işləməsi şərtdirsə, hər 3 sistemi ayrı-ayrı dəmir serverlərdə işlətmək həm maliyyət baxımından yüksək məbləğə başa gəlir, həm resurslardan düzgün istifadə etməmiş olursunuz, həm də idarəetməni çətinləşdirir. Bunun yerinə 32gb ram-a sahib olan serverdə hypervisor üzərində 3 virtual maşın işlətmək daha sərfəlidir. 

## Hypervisor nədir?

 Hypervisor virtual maşınları \(VM\) yaratmaq və işlətmək üçün istifadə olunan virtual maşın monitorinq \(VMM\) proqramlarıdır. Hypervisor host komputerin CPU, RAM və s. kimi resurslarını müxtəlif virtual maşınlar arasında virtual olaraq paylaşmağa imkan yaradır. 

Hypervisor-lar adətə uyğun olaraq 2 tipə bölünürlər: Tip 1 - "bare metal" və Tip2 - "hosted".

Tip1 - Bare metal hypervisorlar çox yüngül bir əməliyyat sistemi vasitəsi ilə virtual maşınları birbaşa hardware üzərində çalışdırırlar. Hosted hypervisorlar isə yüngül əməliyyat sistemləri yerinə ənənəvi proqramlar kimi işləyirlər. 

Məsələn \(Tip 2 - hosted hypervisor\): Fərz edin ki, siz sistem administratorsunuz və sizin dəmir serveriniz var. Həmin serverin üzərində virtual olaraq 3 fərqli əməliyyat sistemi işləməlidir. Biri var ki, həmin serverə windows server 2019 yazıb, onun üstündə vmware workstation pro 16 quraşdırıb, onun içində ayrıca 3 fərqli əməliyyat sistemi quraşdırasınız. Biri var ki, \(Tip 1 - bare metal hypervisor\) dəmir serverinizin üzərinə vmware esxi  6.7 yazasınız, və onun üstündə birbaşa 3 fərqli əməliyyat sistemi qaldırasınız.

Burada fərq ondan ibarət oldu ki, Tip 2 - dən fərqli olaraq siz windows server üçün ayrıca resurs xərcləməmiş oldunuz. Windows server 2019 yükləməyə ehtiyac qalmadı. 

## Container və Hypervisor fərqləri nədir? Container-lər əsasən nə üçün istifadə olunur?

Container texnologiyası əsas iki problemi aradan qaldırdı .Proqramistlər və clientlər arasında belə bir məsələ var taxidən. 

**Birinci problem** budur ki, tutalım müştəri də proqramist də linux istifadəçisidir. Proqramist bir python proqramı yazır, o proqramı yazarkən aaa və abc kitabxanalarından istifadə edir. Proqramı yazıb bitirdikdən sonra onu müştəriyə göndərir. Ya ümumiyyətlə müştəriyə deməyi yadından çıxardır ki, hansı kitabxanalardan istifadə edib, ya da bir hissəsini deməyi yaddan çıxardır. Nəticədə müştəridə proqram çalışmır. Python üçün bu problemi həll etməyin ən gözəl yollarından biri virtual environment-lərdir. Ancaq bütün proqramlaşdırma dilləri üçün belə bir imkan yoxdur. Nəticədə belə bir dialoq ortaya çıxır:

**Müştəri** - "Salam, Məmməd Məmmədov, sizin təzə yazıb verdiyiniz proqram mənim komputerimdə işləmir."  
**Proqramist** - "Mən proqramı yazmışam, məndə problemsiz işləyir. Sizdə necə işləmir?"   
**Müştəri** - "Faktiki olaraq işləmir."  
**Proqramist** - "Ola bilsin XX paketini yükləmədiyiniz üçündür, onu yükləyin açılacaq."

Nəticə etibarı ilə, proqramist qərara gəlir ki, proqramı hər hansı container \(məsələn docker\) şəklində müştəriyə ötürsün. Final olaraq müştəri proqramı problemsiz işlədir. 

**İkinci problem** isə bundan ibarətdir ki, tutalım siz proqramistsiniz və başqa ölkədəki bir şəxs üçün freelance proqram yazırsınız. Proqrami linux üzərində yazmısınız ancaq qarşıdakı şəxsin nə linuxdan başı çıxır nə də linux server qaldıracaq bir hardware-i var. Çarə kimi, proqramı yazırsınız container üzərində və göndərirsiniz müştəriyə. O isə bir neçə sadə əməiyyatdan sonra sizin proqramınızı işlədə bilir.

Üçüncü fərqlilik isə bundan ibarətdir ki, ola bilsin sizin containerdə yazılmış 3 fərqli proqram təminatınız var, bunların üçü də müxtəlif əməliyyat sistemləri üzərində müxtəlif servislərdə işləyirlər və bir-biri ilə əlaqədədirlər. Siz böyük ölçülü əməliyyat sistemlərini komputerə quraşdırmaq məcburiyyətindən azad olursunuz. Çox az resurs sərf edərək yalnız öz proqramınıza lazım olan hissələrdən istifadə edib proqramınızı çalışdırırsınız.

![](../.gitbook/assets/virtual-vs-container.png)



#### **Hypervisorlar:**

* Virtual resursların \(CPU, RAM və s. \) paylaşılaraq istifadə olunması
* Bir dəmir server üzərində bir neçə əməliyyat sistemi quraşdırmaq mümkündür \(Type 1\)
*  Bir əməliyyat sisteminin üzərində bir neçə əməliyyat sistemi quraşdırılaraq \(Type 2\)

#### **Containerlər:** 

* Əməliyyat sistemindən asılı olmayaraq, proqram təminatlarının müstəqil şəkildə çalışmasına şərait yaradır. Başqa sözlə desək, məsəlçün linuxda yazdığınız hər hansı kodu heç bir dəyişiklik etmədən windows-da da çalışdıra bilərsiniz.
* İstənilən əməliyyat sistemi üzərində çalışa bilər. Tək ehtiyacı olan şey container engine-dir.
* Yazılmış proqram təminatının işləməyi üçün lazım olan hər şey container-in içində olduğu üçün çox portable-dırlar. 

{% hint style="info" %}
Container engine-lərə misal: Docker, RKT, CRI-O və LXD
{% endhint %}

Hörmətlə.

