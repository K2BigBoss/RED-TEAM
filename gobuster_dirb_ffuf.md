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
