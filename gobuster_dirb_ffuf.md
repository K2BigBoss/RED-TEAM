Kali Linux-da mavjud wordlistlar:   
```
/usr/share/wordlists/dirb/
```   
Eng ko‘p ishlatiladigan wordlistlar:   
 - **common.txt** — Eng keng tarqalgan kataloglar
 - **big.txt** — Kengroq va chuqurroq skan uchun
 - **small.txt** — Tezkor skan uchun kichikroq ro‘yxat

**Gobuster**  

```
sudo apt install gobuster
```

**1. Asosiy kataloglarni aniqlash:**
```
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt
```

**2. Fayl kengaytmalarini (masalan: .php, .html, .txt) aniqlash:**   
```
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt -x php,html,txt
```   

**3. HTTP bosh (header) ma'lumotlarini ko‘rsatish:**   
```
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt -v
```

**4. HTTP Basic auth bilan tekshirish:**   
```
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt -U user -P password
```

**DIRB**    
```
sudo apt update && sudo apt install dirb
```   

**1. Oddiy skan (asosiy kataloglarni aniqlash)** (Agar so‘zlar ro‘yxati (wordlist) kiritilmasa, standart wordlist (common.txt) ishlatiladi.)   
```
dirb http://target.com
```   

**2. Maxsus wordlist bilan skan**   
```
dirb http://target.com /usr/share/wordlists/dirb/big.txt
```

**3. Fayl kengaytmalari (masalan, .php, .html, .txt) bilan skan**   
```
dirb http://target.com /usr/share/wordlists/dirb/common.txt -X .php,.html,.txt
```    

**4. Basic Authentication (foydalanuvchi va parol) bilan skan**   
```
dirb http://target.com /usr/share/wordlists/dirb/common.txt -u user:password
```   

**5. Skanni davom ettirish (404 xatolarni inkor qilish)** (Ko‘pincha noto‘g‘ri sahifalar (404) skanni to‘xtatadi, bunga yo‘l qo‘ymaslik uchun)   
```
dirb http://target.com /usr/share/wordlists/dirb/common.txt -N 404
```   

**FFUF**   
```
sudo apt update && sudo apt install ffuf
```   
**1. Oddiy katalog fuzzing (directory busting).**
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```
 
**2. Maxsus fayl kengaytmalarini qidirish.**   
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php,.html,.zip,.bak,.old
```   

**3. HTTP so‘rov boshini (header) o‘zgartirish.** (Bu buyruq WAF (Web Application Firewall) yoki boshqa cheklovlarni aylanib o‘tishga yordam beradi.)   
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -H "User-Agent: Mozilla/5.0"
```    

**4. Parametr fuzzing (GET so‘rovlarida).**   
```
ffuf -u "http://target.com/index.php?FUZZ=1" -w /usr/share/wordlists/parameters.txt
```   
http://target.com/index.php?user=1  
http://target.com/index.php?admin=1  
http://target.com/index.php?debug=1  
http://target.com/index.php?test=1      

**5. Subdomain fuzzing (yashirin subdomainlarni qidirish).** (Bu buyruq yashirin subdomainlarni (masalan, admin.target.com) topishga yordam beradi.)    
```
ffuf -u http://FUZZ.target.com -w /usr/share/wordlists/dns/subdomains-top1million-5000.txt -H "Host: FUZZ.target.com"
```   

**6. Status kodlarni filtrlash.**   
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200,301
```

**7. FFUF orqali zaifliklarni aniqlash.**   
 - **LFI (Local File Inclusion) fuzzing** (/etc/passwd, ../../../../../etc/passwd qatorlarini sinab ko‘radi.)  
```
ffuf -u "http://target.com/page.php?file=FUZZ" -w /usr/share/wordlists/lfi.txt
```
 - **RCE (Remote Command Execution) fuzzing** (Bu buyruq ping, whoami, ls kabi buyruqlarni sinab ko‘radi.)   
```
ffuf -u "http://target.com/shell.php?cmd=FUZZ" -w /usr/share/wordlists/commands.txt
```   

**8. FFUF ni optimallashtirish (tezlashtirish va filtrlar)**   
 - Tezlikni oshirish (-t parametri yordamida bir vaqtda qancha so‘rov yuborilishini belgilaydi.):
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -t 100
```   
 - Bo‘sh javoblarni chiqarib tashlash (Bo‘sh (zero length) javoblarni yashirish):
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -fs 0
```
 - Xatolik kodlarini yashirish (403 kabi ruxsat berilmagan javoblarni yashirish):
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt -fc 403
```   

**9. Admin panel qidirish.**   
```
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/admin.txt
```

**10. Login bypass qilish uchun fuzz qilish**   
```
ffuf -u http://target.com/login -X POST -d "user=admin&FUZZ=1" -w /usr/share/wordlists/parameters.txt
```
is_admin=1  
admin=true  
role=admin  


