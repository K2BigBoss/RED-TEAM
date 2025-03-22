**Reconnaissance**  
`nmap -sV 10.129.1.193`  

![image](https://github.com/user-attachments/assets/d4b5a5f1-cc1f-49e9-a43c-cc3fa038a1cf)  

Port 80 ochiq bo‘lgani uchun brauzer orqali 10.129.1.193 IP-manzilini tekshirib chiqamiz, ammo foydali narsani topa olmaymiz.  

![image](https://github.com/user-attachments/assets/e0ffbe0d-c885-42ba-95b9-7b9182b5ea06)  

Zaiflikdan foydalanish uchun Metasploit Framework dan foydalanamiz. Biz `Nostromo <= 1.9.6` versiyasidagi masofadan kod bajarish (RCE) zaifligini ekspluatatsiya qiluvchi modulni topdik. Ushbu muammo nostromo nhttpd ning `http_verify` funksiyasidagi directory traversal tufayli yuzaga keladi, bu esa tajovuzkorga maxsus yaratilgan HTTP so‘rovi orqali masofadan kod bajarishga imkon beradi.  

