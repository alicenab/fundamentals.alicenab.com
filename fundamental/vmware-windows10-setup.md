---
description: >-
  Salam, bu yazıda "VMWare workstation pro" proqramı içində "Windows 10" tipli
  əməliyyat sistemini necə quraşdırmalı olduğunuzu öyrənəcəksiniz.
---

# VMWare-də Windows 10-u necə işlətmək olar?

&#x20;Birinci növbədə sizə əməliyyat sisteminin rəsmi mənbədən olan iso faylı lazım olacaq.

iso faylını ən rahat formada brauzerin user-agent-ini dəyişdirərək yükləyə bilərsiniz. Bunun üçün brauzerin add-on hissəsində "user-agent switch" axtarıb onu install etməyiniz lazım olacaq.

Məsələn firefox üçün bu add-on məsləhətlidir: [https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/](https://addons.mozilla.org/en-US/firefox/addon/user-agent-string-switcher/)

![](<../.gitbook/assets/0 (1).png>)

Add to Firefox etdikdən sonra brauzerin yuxarı sağ tərəfdəki hissəsində add-on-un iconunun görəcəksiniz.

[https://www.microsoft.com/en-us/software-download/windows10ISO](https://www.microsoft.com/en-us/software-download/windows10ISO)

Bu sayta daxil olduqdan sonra şəkildəki mərhələlərlə dəyişiklik edib F5 basaraq səhifəni refresh edin.

![](<../.gitbook/assets/1 (1).png>)

Yeni yaranmış səhifədə seçimlərinizi edib hər iki "Continue"-a klikləyin.

![](<../.gitbook/assets/2 (1).png>)

Bundan sonra yeni gələn səhifədə 64-bit versiyanı endirin:

![](<../.gitbook/assets/3 (1).png>)

"VMWare workstation pro 16" proqramına girdikdən sonra Home pəncərəsinə gəlib. "Create new Virtual Machine" seçmək lazımdır. Açılan pəncərədə "Typical" seçib  Next etmək lazımdır.

![](<../.gitbook/assets/4 (1).png>)

&#x20;Açılan pəncərədə "Installer disc image file (iso)" seçib, "Browse" clickləmək lazımdır. Açılmış pəncərədə internetdən yüklədiyimiz "Windows 10" iso faylını seçmək lazımdır

![](<../.gitbook/assets/5 (1).png>)

"Guest operating system" - Microsoft Windows, "Version" isə "Windows 10 x64" olaraq seçilir.

![](<../.gitbook/assets/6 (1).png>)

"Virtual machine name" hissəsinə hər hansı birşey yaza bilərsiniz.\
"Location" hissəsində virtual maşının 60GB məlumatının hansı qovluqda saxlanılacağını seçməyiniz lazım olacaq. Next-ə klikləyirik.

![](<../.gitbook/assets/7 (1).png>)

"Maximum disk size" 60 vermişəm. Əgər yeriniz məhduddursa 30 da verə bilərsiniz.\
"Store virtual disk as a single file" seçməyimizin səbəbi budur ki, virtual maşını hardansa harasa kopyalayanda çox vaxt getməsin. Next-ə klikləyirik.

![](<../.gitbook/assets/8 (1).png>)

Finish-ə klikləyirik.

![](<../.gitbook/assets/9 (1).png>)

Virtual maşını işə salmaq üçün "Power on this virtual machine" klikləyirik.

![](<../.gitbook/assets/10 (1).png>)

Burada "Press any key to boot from CD or DVD" yazısını gördüyünüz vaxt klavyaturada hansısa hərfə basmağınız lazım olacaq. Əgər gecikdinizsə, problem yoxdur. Yuxarıdakı "VM"-ə klikləyib "reset"-ə basaraq yenidən bu pəncərəyə qayıda bilərsiniz.

![](<../.gitbook/assets/11 (1).png>)

Açılan boot manager pəncərəsində "Windows 10 Setup (64-bit) seçirik.

![](<../.gitbook/assets/12 (1).png>)

![](<../.gitbook/assets/13 (1).png>)

![](<../.gitbook/assets/14 (1).png>)

![](<../.gitbook/assets/15 (1).png>)

![](<../.gitbook/assets/16 (1).png>)

![](<../.gitbook/assets/17 (1).png>)

![](<../.gitbook/assets/18 (1).png>)

![](<../.gitbook/assets/19 (1).png>)

![](<../.gitbook/assets/20 (1).png>)

![](<../.gitbook/assets/21 (2).png>)

![](<../.gitbook/assets/22 (1).png>)

![](<../.gitbook/assets/23 (1).png>)

![](<../.gitbook/assets/24 (1).png>)

![](<../.gitbook/assets/25 (1).png>)

![](<../.gitbook/assets/26 (1).png>)

![](<../.gitbook/assets/27 (1).png>)

![](<../.gitbook/assets/28 (1).png>)

![](../.gitbook/assets/29.png)

![](../.gitbook/assets/30.png)

![](../.gitbook/assets/31.png)

![](../.gitbook/assets/32.png)

Bu seçimləri "No" etmək lazımdır. Bunlar sayəsində Microsoft sizin komputerinizdən mütəmadi istəməyəcəyiniz məlumatları götürür. Buna yazdığınız mətnlərdən tutmuş yerləşdiyiniz yerə qədər daxildir.

![](../.gitbook/assets/33.png)

![](../.gitbook/assets/34.png)

![](../.gitbook/assets/35.png)

Budur, hazırdır!

Hörmətlə.
