---
description: >-
  Salam, bu yazıdan AD haqqında fundamental bilik sahibi olacağınızı ümid
  edirəm.
---

# Active Directory termin lüğəti

* Active Directory Basics
* Active Directory Services
* Active Directory DNS
* Active Directory Security \(Authentication, Security Protocols, Permissions\)

## Active Directory

Active directory şəbəkədəki istifadəçilərin, komputerlərin və digər object-lərin idarəetməsini mərkəzləşdirən servisdir. Əsas vəzifələrindən biri domain-də istifadəçi və komputerləri authenticate və authorize etməkdir. Məsələn domain istifadəçisi öz hesabına istifadəçi adı və şifrəsini yazaraq giriş etdikdə Active directory əmri ilə istifadəçinin daxil etdiyi məlumatların düzgünlüyü yoxlanılır. Əgər düzgündürsə, istifadəçi komputerə giriş qazanır.

**AD** - Active Directory ifadəsinin qısaldılmış versiyası.  
**AD DS** - Active Directory Domain Services windows serverdə bir role-dur.  
**Domain controller** - Active Directory Domain Service rolu-una sahib olan server. 

## Domain

Domain Active Directory içində container\(virtualizasiyadakı ilə eyni deyil\) və object-lərin məntiqi strukturuna deyilir. Onun aşağıdakı komponentləri mövcudur:

* User, group, computers və digər object-lər üçün struktur.
* Domenlərin içindəki resurslara giriş icazəsinin verilməsi üçün lazım olan təhlükəsizlik servisləri.
* User və computer-lərə təyin olunan Policy-lər.
* Domen-i tanımaq üçün DNS servisi. Hansısa domen-in üzvü olan bir komputerə giriş etdikdə onun DNS domen adını mütləq həmin komputer tanımalıdır.

## Domain tree

Artıq mövcud olan bir domenə child domain \(DNS-dəki subdomen məntiqi\) əlavə etsəniz siz domain tree yaratmış olursunuz. Məsələn bu ikisi bir domain tree-nin üzvü sayılır: test1.mydomain.local və test2.mydomain.local  
Parent domain və child domain arasında avtomatik olaraq trust yaranır

## Functional levels 

Functional level-lər domendə hansı imkanların olduğunu təyin edirlər. Windows server versiyaları kimi başa düşə bilərsiniz. Functional level nə qədər təzə olsa bir o qədər yeni texnologiyalardan istifadə etmək imkanınız yaranır.

Functional levels haqqında ətraflı məlumatı bu linkdən əldə edə bilərsiniz: [https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-functional-levels](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-functional-levels)

## Forest

Siz ilk dəfə Windows Server-ə Active Directory quraşdıranda həmçinin forest yaradırsınız. \(məs: _mydomain.local_ \). Forest özündə domain tree-ləri saxlayır. 

## FQDN - Fully Qualified Domain Name

FQDN dedikdə tam adres nəzərdə tutulur. Məsələn, əgər mənim komputerimin adı "mypc" və mənim hal-hazırda olduğum domenin adı "test2.mydomain.local" dırsa, mənim FQDN-im bu olacaq: "mypc.test2.mydomain.local".

## FSMO - Flexible Single Master Operation

Iki modu mövcuddur, multi master model və single master model. Əsas fərqlərindən biri performansdır. Single master modelin aşağıdakı role-ları mövcuddur:

* **Schema Master -** bütün forestə tətbiq olunan role-dur. Active Directory Schema-dakı bütün dəyişiklikləri idarə edir.
* **Domain Naming Master** **-** bütün forestə tətbiq olunan role-dur. Domenlərin əlavə edilib silinməsini idarə edir.
* **RID master -** Təyin edilmiş DC üzrə digər bütün DC-lərdən gələn RID Pool request-lərini idarə edir. 
* **PDC emulator -** Bu role şifrə dəyişikliklərini, user lockout-larını, group policy-lərini və clientlər üçün time serveri idarə edir.
* **Infrastructure master -** Tutalım test1.mydomain.local-ın istifadəçiləri test2.mydomain.local-ın security group-unun üzvləridir. Bu zaman istifadəçiləri təyin etmək üçün infrastructure master role-u istifadə olunur.

Onlar haqqında əlavə məlumatı bu keçiddən əldə edə bilərsiniz: [https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/fsmo-roles](https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/fsmo-roles)

## Objects

Active Directory ilə işlədiyiniz zaman birbaşa və ya dolayı yolla object-lərlə işləmiş sayılırsınız. Object dedikdə domendəki bir resursu bildirən atribut grupları nəzərdə tutulur. Object-lər SİD adlandırılan unique security identifier-inə birləşirlər ki, bu da domen-dəki digər resursla object-in icazə verilib verilməməsinə yarayır. Yeni Active Directory üzərində gələn default object tipləri aşağıdakılardır:

### **Organizational Unit**

OU eyni domendəki müxtəlif object-ləri özündə saxlaya bilən bir container-dir. User accounts, contacts, computers və groups-u organize etmək üçün organizational unit-lər istifadə olunur. Group policy object-lər OU-lara təyin oluna bilirlər. 

### **Users** 

İstifadəçi hesabları əsasən istifadəçilərə ona görə verilir ki, onlar domen resurslarına giriş edə bilsinlər. Bununla bərabər, sistem servislərinin və ya proqramların işləməsi üçün də istifadəçi yaradıla bilər. 

### **Computer** 

Domenə qoşulan komputeri bildirir.

### **Groups** 

İki tip qruplar mövcuddur: security və distribution. Security group vasitəsi ilə istifadəçiləri qruplaşdırılır ki, domen resurslarına giriş icazəsi vermək sadələşsin. Məsələn, əgər HR departamenti üçün yaradılmış qovluğa yalnız HR departamentinin giriş etməsini təmin etmək istəsəm, HR departament istifadəçilərinin hamısını bir security group-a atıb, həmin group-u həmin folder-ə apply edərəm. Bu hər bir HR əməkdaşı üçün ayrı-ayrı icazə verməyimin qarşısını alaraq işin effektivliyini artırır. Distribution qruplar isə email distribution list-lər üçün istifadə olunur

#### Group scope

Group scope onu göstərir ki, group domenə yoxsa forest-ə apply edilə bilər. 3 group scope mövcuddur:

1.  **Universal** - istənilən digər universal qruplardan, forest-in içindəki istənilən tree və ya domendən olan object-ləri özündə saxlaya bilər.
2. **Global** - Domendən object-ləri özündə saxlaya bilir. İstənilən domain tree və ya forest içində istifadə oluna bilər.
3. **Domain local** - İstənilən domendən object-ləri özündə saxlaya bilir ancaq yalnız yaradıldığı domen-ə apply edilə bilir.

### **Contacts** 

Contact email məqsədləri üçün istifadə olunur. Domenə contact olaraq giriş etmək vəya səlahiyyətləri contact ilə təhlükəsizləşdirmək mümkün deyil. 

### **Shared folder**

Shared folder-i Active Directory-də paylaşdığınızda bir object yaranır. Shared folder-ləri active directory-də paylaşmaq istifadəçilərin domen içində shared olan qovluqları və faylları tapmasını asanlaşdırır. 

### **Share printer**

Shared folder ilə eyni məntiqdə işləyir. Sadəcə printerlər üçündür.

## LDAP - Lightweight Directory Access Protocol

LDAP directory servislərinə giriş etmək üçün istifadə olunan crossplatform protokoldur. LDAP proqramlar və digər sistemlərin directory serverlərlə əlaqəsini təmin etmək üçün danışıq vasitəsi rolunu oynayır. Sadə dildə desək, LDAP Active Directoryə qoşulmaq və əlaqə qurmaq üçün bir yoldur.

## Active Directory Security

### Kerberos

Kerberos istifadəçiləri identifikasiya edərək domen resurslarına keçidini təsdiq etmək üçün işlədilən təhlükəsizlik protokoludur.

### Ticket Granting Ticket \(TGT\)

### Key Distribution Center \(KDC\)

KDC domain controllerdə çalışan və Kerberos protokolunda istifadə olunan session ticket paylama servisidir.

### Service Principal Names \(SPN\)

SPN servisin unikal identifieridir.

### NTLM 

NTLM istifadəçilərin autentikasiyası, tamlığı və konfidensiallığı üçün işlədilər təhlükəsizlik protokolları toplusudur.

### NTFS Permissions

NTFS səlahiyyətləri dedikdə qovluğa və ya fayla təyin edilən səlahiyyət nəzərdə tutulur. 5 default səlahiyyət tipi mövcuddur:

* **Full Control** – Aşağıdakıların hamısı
* **Modify** – faylları görmək və dəyişdirə bilmək üçün
* **Read & Execute** – faylları görmək və çalışdıra bilmək üçün
* **Read** – faylın içindəkiləri görmək üçün
* **Write** – fayl və qovluqların yaradılması, mövcud olan faylın içinin dəyişdirilməsi üçün

### Share Permissions

Share səlahiyyətləri dedikdə share olunmuş qovluğa istifadəçilərin səlahiyyətləri nəzərdə tutulur. 3 tipi mövcuddur:

* **Read** – qovluğa və alt qovluqlara baxmaq üçün lazımdır
* **Change** – oxumaq və dəyişdirmək üçün lazımdır
* **Full Control** – İstifadəçilərə dəyişdirmək, oxumaq, silmək yazmaq və digər bütün səlahiyyətləri verir.

### Discretionary access control list \(DACL\)

DACL verilmiş fayla və ya qovluğa hansı istifadəçinin buraxılıb buraxılmadığını təyin etmək üçündür.

### Access Control Entries \(ACE\)

DACL özü ACE-lərdən ibarətdir. ACE hansı istifadəçi hesabının resursa hansı səviyyədə icazəsi olduğunu müəyyən edir. Əgər heç bir ACE yoxdursa, sistem həmin object-ə olan bütün müraciətlə icazə vermir.

### System Access Control List \(SACL\)

SACL administratorlara təhlükəsizlik object-lərinə giriş cəhdlərini loglamağa imkan verir.

#### 



