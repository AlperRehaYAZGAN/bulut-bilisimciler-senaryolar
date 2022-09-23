
`curl google.com` olarak istek yaparsak ve hiç bir kontrol belirtmezsek, cURL bunu HTTP GET isteği olarak yorumlar. 
Burada istek yapılan adresin kaynak kodu verilir.

```
$ curl google.com 

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8"> 
<TITLE>301 Moved</TITLE></HEAD><BODY> 
<H1>301 Moved</H1> 
The document has moved 
<A HREF="http://www.google.com/">here</A>. 
</BODY></HTML>

```

Bu çıktıyı bir dosyaya yazdırmak istersek `-o` parametresini kullanabiliriz.

```
$ curl -o burayayaz.html google.com 

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   219  100   219    0     0    585      0 --:--:-- --:--:-- --:--:--   585
```

burayayaz.html adlı dosyanın içerisine google.com adresine cURL ile yapılan GET isteğinin cevabı yazılmış oldu. Hatta dosyanın içeriğini de görelim:

```
$ cat burayayaz.html
 
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>      
```      
              
Gördüğünüz gibi burayayaz.html dosyasının içerisinde google.com adresinin kaynak kodu yazılmıştır.