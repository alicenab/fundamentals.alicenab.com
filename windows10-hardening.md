---
description: 'Salam, bu yazıda sadə qaydada "Windows hardening" etməyi öyrənəcəksiniz.'
---

# Windows 10 əməliyyat sisteminin möhkəmləndirilməsi \(WORKGROUP komputerlər üçün\)



Dərsi yeni formatdan çıxmış sistemdə izah edəcəm.

Format zamanı yaranmış istifadəçimizin adı "istifadeci" dir. Bizə lazımdır ki default olaraq deaktiv gələn "Administrator" istifadəçisini aktivləşdirək. Windows-da localgroup-lar var istifadəçiləri qruplaşdırmaqçün. Səlahiyyətli istifadəçilərin qrupunun adı "Administrators", digərlərinin isə "Users"-dir. Bizə lazımdır ki, Format vaxtı default olaraq "Administrators" qrupuna add olunan "istifadeci" istifadəçisini oradan çıxarıb, "Users" localgroup-una add edək. Əməliyyatları etmək üçün "cmd"-ni administrator istifadəçisi ilə çalışdırmaq lazımdır.

![](.gitbook/assets/0%20%283%29.png)

"net user" komandası ilə sistemdə hansı istifadəçilərin olduğunu görürük. Şəkildən də gördüyünüz kimi, sistemdə "Administrator" və "istifadeci" istifadəçiləri mövcuddur hal-hazırda. "Administrator" istifadəçisi haqqda məlumat əldə etmək üçün "net user Administrator" əmrini çalışdırıram. "Account active" hissəsində gördüyüm kimi, status "No"-dur. Aktivləşdirmək üçün "net user Administrator /active:yes" əmrini icra edirəm. Bundan sonra, həm "Administrator" həm də "istifadeci" istifadəçisinin şifrələrini dəyişirəm. PS: Siz asan şifrə qoymayın və fərqli şifrə qoyun.

![](.gitbook/assets/1%20%283%29.png)

Sistemdə hansı "localgroup"-ların olduğunu görmək üçün əmr sətrinə "net localgroup" yazıram. Çıxan yazıdan istədiyim "Administrators" və "Users" nəticələrini görə bilirəm. Hal-hazırda "Administrators" localgroup-unun içində hansı istifadəçilərin olduğunu görmək üçün, "net localgroup Administrators" yazıram. Çıxan nəticədən belə məlum olur ki, Hal-hazırda "Administrators" localgroup-unda "Administrator" və "istifadeci" istifadəçiləri var. "net localgroup Administrators istifadeci /delete" yazaraq "istifadəçi" istifadəçisini "Administrators" localgroup-undan silirəm. Ancaq belə qalsa "istifadeci" istifadəçisi sistemə login ola bilməyəcək. Login olmasını da təmin etmək məqsədi ilə onu "Users" localgroup-una əlavə etmək lazımdır. Bunun üçün "net localgroup Users istifadeci /add" komandasını icra etmək kifayətdir. "net localgroup Users" əmrini icra edərək həmin localgroup-un içində həqiqətən də "istifadeci" istifadəçisinin olmasını təsdiqləmək mümkündür.

![](.gitbook/assets/2%20%282%29.png)

  
User account control-un maksimum səviyyəyə çəkilməsi üçün axtarış hissəsində "uac"-a girib çıxan pəncərədəki səviyyə çubuğunu yuxarı çəkmək kifayətdir.

![](.gitbook/assets/3%20%281%29.png)

  
Bundan sonra sıra gəlir "Firewall"-ı sazlamağa, bura bütün profillərin loglanmasını aktivləşdirməkdir məqsədimiz. Bunun sayəsində komputerdə şübhəli hal olarsa, keçmiş loglara baxaraq vəziyyəti öyrənmək mümkündür.

![](.gitbook/assets/4%20%281%29.png)

Bu addımdan sonra sıra gəlir "Windows Security" sazlamalarına:

real-time protection - \[On\]  
cloud-delivered protection - \[On\]  
automatic sample submission - \[On\]  
tamper protection - \[On\]  
controlled folder access - on \(set up for OneDrive if possible\)  
Firewall: Domain network:on, Private network:on, Public network:on  
App & browser control -&gt;  
 -&gt; Reputation-based protection:  
    -&gt; Check apps and files \[On\]  
    -&gt; SmartScreen for Microsoft Edge \[On\]  
    -&gt; SmartScreen for Microsoft Store apps \[On\]  
    -&gt; Potentially unwanted app blocking: \[On\] -&gt; Block apps, block downloads.  
 -&gt; Exploit Protection -&gt;  
    -&gt; Control flow Guard \(CFG\) \[On\]  
    -&gt; Data Execution Prevention \(DEP\) \[On\]  
    -&gt; Force randomization for images \(Mandatory ASLR\) \[On\]  
    -&gt; Randomize memory allocations \(Bottom-up ASLR\) \[On\]  
    -&gt; High-entropy ASLR \[On\]  
    -&gt; Validate exception chains \(SEHOP\) \[On\]  
    -&gt; Validate heap integrity \[On\]  
    -&gt; Programm Settings:  
       -&gt; \[Remove All Programs\]  
Device Security -&gt;  
 -&gt; Core isolation details -&gt;  
 -&gt; Memory Integrity \[On\]  

Bu hissədə olan sazlamaların izahlarını, group policy pəncərələrinin details hissəsindən oxuya bilərsiniz:

Windows düyməsi və r basıb açılan pəncərədə gpedit.msc yazırıq.

  
gpedit.msc -&gt; Computer Configuration -&gt; Administrative Templates -&gt;  
 -&gt; Windows Components -&gt; Windows Defender Antivirus -&gt;  
 \* Real-time Protection -&gt; Turn on behavior monitoring \[On\]  
            -&gt; Scan all downloaded files and attachments \[On\]  
            -&gt; Monitor file and program activity on your computer \[On\]  
 \* Security Intelligence Updates -&gt;  
            -&gt; Define the number of days before ... \(both of them\): \[Enable\] \[1 day\]  
             -&gt; Allow security intelligence updates when running on battery power \[Enable\]  
 \* Network Inspection System -&gt;  
            -&gt; Turn on definition retirement \[On\]  
            -&gt; Turn on protocol recognition \[On\]  
 \* MAPS -&gt;  
            -&gt; Join Microsoft MAPS \[Enabled\]\[Advanced Maps\]  
             -&gt; Block at First Sight \[Enabled\]  
 \* MpEngine -&gt;  
            -&gt; Configure extended cloud check \[Enable\]\[30\]  
            -&gt; Select cloud protection level \[Enabled\]\[Zero tolerance blocking level\]

Son olaraq, powershell-i administrator səlahiyyətləri ilə açıb açağıdakı əmrləri icra etmək lazımdır:  
Set-MpPreference -PUAProtection 1  
gpupdate

Komputerə restart atdıqdan sonra, komputerin sahibi "istifadeci" istifadəçisinə daxil olaraq komputeri işlədə bilər.

Hörmətlə.

