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


