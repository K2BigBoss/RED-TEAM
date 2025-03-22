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
