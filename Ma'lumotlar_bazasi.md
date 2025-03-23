**1. Veb-ilovani skanerlash va zaifliklarni aniqlash**   
Birinchi qadam – IP manzilni skanerlash va veb-ilovaning qanday texnologiyalar asosida ishlayotganini aniqlash.  

1. Lokal tarmoqdagi (LAN) IP manzillar va MAC manzillarini aniqlash uchun tarmoqni skanerlash.   
```
netdiscover -r 192.168.1.0/24
```

```
netdiscover -i wlan0 -r 192.168.0.0/16
```

2. Ochiq portlar va xizmatlarni aniqlash (Port Scanning).   
```
nmap -sC -sV -A -p- <IP-manzil>
```

3. Xizmatga bog‘liq zaifliklarni aniqlash.
 -  **FTP zaifligini aniqlash:**
```
nmap --script ftp-vuln* -p 21 [IP-manzil]
```
 - **SMB zaifligini aniqlash:**   
```
nmap --script smb-vuln* -p 445 [IP-manzil]
```
 - **HTTP zaifligini aniqlash:**
```
nmap --script http-vuln* -p 80 [IP-manzil]
```
