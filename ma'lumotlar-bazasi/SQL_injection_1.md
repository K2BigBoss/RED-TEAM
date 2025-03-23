**Previse HackTheBox Walkthrough**  

**Network Scanning**   

```nmap -A 10.129.95.185```

Ochiq portlar:
 - 22 running SSH
 - 80 running a website   

![image](https://github.com/user-attachments/assets/b38fa1db-8558-4d52-9373-2c0ca9e4c446)   

**Enumeration**  
Veb-sayt topildi. Ba'zi sahifalarni ko'rib chiqqach, unga kirish uchun autentifikatsiyadan o'tishim kerakdek tuyuldi.  
![image](https://github.com/user-attachments/assets/be0962f3-48ae-488a-85ec-30c6cb402036)   

Keyin biz gobuster yordamida veb-saytdagi mavjud PHP sahifalarini sanab o'tdik.   
```
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt --url http://10.129.95.185/ -x php
```

![image](https://github.com/user-attachments/assets/45220777-70f7-4a36-8fe2-ffacffd5cd35)   

Biz nav.php deb nomlangan sahifani topdik, u veb-sayt uchun navigatsiya sahifasi bo'lib chiqdi. Xuddi shu sahifada biz hisob yaratish sahifasini ko'ramiz.

![image](https://github.com/user-attachments/assets/147b17e4-5788-460e-998c-ab1b2a9e05ed)   

Hisob yaratish sahifasini biroz tekshirgandan so'ng, biz barcha sahifalar kirishdan himoyalangan va foydalanuvchi tizimga kirishi kerak degan xulosaga keldik. Shunday qilib, biz kirish nazoratini chetlab o'tish uchun HTTP javobini buzishga harakat qildik. Buning uchun biz burpda so'rovni oldik.   
![image](https://github.com/user-attachments/assets/8e185ba7-db89-4018-af79-85313cb04699)   




