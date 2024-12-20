# Natas 6
The natas 6 is the first of the series that gives us the source code:

```php
<html>  
<head>  
<!-- This stuff in the header has nothing to do with the level -->  
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">  
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />  
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />  
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>  
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>  
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>  
<script>var wechallinfo = { "level": "natas6", "pass": "<censored>" };</script></head>  
<body>  
<h1>natas6</h1>  
<div id="content">  
  
<?  
  
include "includes/secret.inc";  
  
    if(array_key_exists("submit", $_POST)) {  
        if($secret == $_POST['secret']) {  
        print "Access granted. The password for natas7 is <censored>";  
    } else {  
        print "Wrong secret";  
    }  
    }  
?>  
  
<form method=post>  
Input secret: <input name=secret><br>  
<input type=submit name=submit>  
</form>  
  
<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>  
</div>  
</body>  
</html>
```

The page ask us for a secret. 
The source code include the code contained in "/includes/secret". if you visit that page  you can see that there it is created the variable $secret.

```php
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```


So as before i intercepted the post request using burp and modify it.
The final request to obtain the password is:
```http
POST / HTTP/1.1
Host: natas6.natas.labs.overthewire.org
Content-Length: 27
Cache-Control: max-age=0
Authorization: Basic bmF0YXM2OjBSb0p3SGRTS1dGVFlSNVd1aUFld2F1U3VOYUJYbmVk
Accept-Language: en-US,en;q=0.9
Origin: http://natas6.natas.labs.overthewire.org
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.140 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://natas6.natas.labs.overthewire.org/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

secret=FOEIUWGHFEEUHOFUOIU&submit=submit
```

and the site answers: 
*Access granted. The password for natas7 is bmg8SvU1LizuWjx3y7xkNERkHxGre0GS*
