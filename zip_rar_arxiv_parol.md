**Arxivdan Chiqarish**   
```
sudo apt update && sudo apt install unrar
```
```
sudo apt update && sudo apt install p7zip-full
```  

|       Arxiv turi      |      Ochish uchun vosita      |              Asosiy buyruq            |
|-----------------------|-------------------------------|---------------------------------------|
| ZIP                   | `unzip`                       | `unzip fayl.zip`                      |
| RAR                   | `unrar`                       | `unrar x fayl.rar`                    |
| 7z (7-Zip)            | `7z`                          | `7z x fayl.7z`                        |
| tar                   | `tar`                         | `tar -xvf fayl.tar`                   |
| tar.gz / tgz          | `tar`                         | `tar -xvzf fayl.tar.gz`               |
| tar.bz2               | `tar`                         | `tar -xvjf fayl.tar.bz2`              |
| tar.xz                | `tar`                         | `tar -xvJf fayl.tar.xz`               |     

**1. ZIP arxivlarining parolini buzish (fcrackzip yordamida)**   
```
fcrackzip -u -D -p /usr/share/wordlists/rockyou.txt secret.zip
```

**2. RAR arxivlarining parolini buzish (rarcrack yordamida)**   
```
sudo apt update && sudo apt install rarcrack
```

```
rarcrack secret.rar --type rar --threads 8
```

**3. ZIP va RAR parollarini John the Ripper yordamida buzish**   
 - ZIP faylni buzish:
```
zip2john secret.zip > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
 - RAR faylni buzish:
```
rar2john secret.rar > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

**4. 7z (7-Zip) fayllarining parolini buzish**   
```
7z2john secret.7z > hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```   

**5. Hashcat yordamida tezkor buzish (GPU orqali)**   
```
zip2john secret.zip > hash.txt
hashcat -m 13600 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```
(-m 13600 - ZIP hash turi (ZIP uchun 13600 kodi).)  
(-a 0 - Wordlist rejimi.)  
