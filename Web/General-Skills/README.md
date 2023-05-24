# Gerneral Skills
[敏感檔案位置](#敏感檔案位置)  
## 敏感檔案位置
**robots.txt:** 用於告訴爬蟲機器人哪些檔案室不可檢索的(像是Google BOT不會把你網站的管理頁面放在網路上讓大家看的到)     
**sitemap.xml:** 一份你網站有哪些地址的清單     
**/.htaccess:** 用於更改伺服器組態的檔案  
**/.DC_Store:** 放在MAC處理檔案得東西  
### 例題
#### picoCTF 2021 Scavenger Hunt
http://mercury.picoctf.net:5080/  
CTRL+U可以打開網頁原始碼  
```html

<!doctype html>
<html>
  <head>
    <title>Scavenger Hunt</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="mycss.css">
    <script type="application/javascript" src="myjs.js"></script>
  </head>

  <body>
    <div class="container">
      <header>
		<h1>Just some boring HTML</h1>
      </header>

      <button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">How</button>
      <button class="tablink" onclick="openTab('tababout', this, '#222')">What</button>

      <div id="tabintro" class="tabcontent">
		<h3>How</h3>
		<p>How do you like my website?</p>
      </div>

      <div id="tababout" class="tabcontent">
		<h3>What</h3>
		<p>I used these to make this site: <br/>
		  HTML <br/>
		  CSS <br/>
		  JS (JavaScript)
		</p>
	<!-- Here's the first part of the flag: picoCTF{t -->
      </div>

    </div>

  </body>
</html>

```
依次打開myjs.js以及mycss.css，其中一個flag後面有提示，接著依序打開功能相對應，剛剛上面的那些路徑就可以把flag拼起來了

