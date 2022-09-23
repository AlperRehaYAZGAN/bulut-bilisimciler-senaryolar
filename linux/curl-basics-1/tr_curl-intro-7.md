Bu istekte ise https://self-signed.badssl.com/ adresine GET metoduyla HTTP isteği gerçekleştirilmiş ve cevap başarıyla dönmüş oldu. 



HTTP isteklerini cURL ile gerçekleştirebiliriz. 

 - `-I` parametresiyle istek yapılan adrese ait HTTP header bilgilerine ulaşabiliriz, ayrıca sayfa durum kodu da bizlere verilir.
 - `-i` parametresiyle yapılan isteğe karşı dönen cevap bilgisi verilir ve ayrıca istek yapılan adresin HTTP header bilgileri dönülür.
 - `-v` parametresiyle HTTP isteği yapılan adres ve hangi porttan isteğin gerçekleştirildiği, kaynak adresin HTTP header bilgileri, cevap dönen kaynak adrese ait HTTP header bilgileri ve isteğe karşılık dönen cevap bilgilerine ulaşılabilir.


Şimdi teker teker bu parametrelerin kullanımına bakalım.


`-I` parametresiyle aşağıdaki gibi bilgilere ulaşmaktayız:

```
$ curl -I google.com

HTTP/1.1 301 Moved Permanently
Location: http://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Fri, 16 Sep 2022 14:00:00 GMT
Expires: Sun, 16 Oct 2022 14:00:00 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 219
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
```


`-i` parametresiyle aşağıdaki gibi bilgilere ulaşmaktayız:

```
$ curl -i google.com

HTTP/1.1 301 Moved Permanently
Location: http://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Fri, 16 Sep 2022 14:00:44 GMT
Expires: Sun, 16 Oct 2022 14:00:44 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 219
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```


`-v` parametresiyle aşağıdaki gibi bilgilere ulaşmaktayız:

```
$ curl -v google.com

*   Trying 172.217.20.78:80...
* TCP_NODELAY set
* Connected to google.com (172.217.20.78) port 80 (#0)
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 301 Moved Permanently
< Location: http://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Date: Fri, 16 Sep 2022 14:01:34 GMT
< Expires: Sun, 16 Oct 2022 14:01:34 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 219
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< 
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```


Request(istek) URL adresi "https://fakerestapi.azurewebsites.net/api/v1/Users" olsun. GET metodu üzerinden `-X` parametresiyle bize bu URL adresinin sunduğu verileri aşağıdaki örnekte olduğu gibi alabiliriz.

```
$ curl -X GET "https://fakerestapi.azurewebsites.net/api/v1/Users"

[{"id":1,"userName":"User 1","password":"Password1"},{"id":2,"userName":"User 2","password":"Password2"},{"id":3,"userName":"User 3","password":"Password3"},{"id":4,"userName":"User 4","password":"Password4"},{"id":5,"userName":"User 5","password":"Password5"},{"id":6,"userName":"User 6","password":"Password6"},{"id":7,"userName":"User 7","password":"Password7"},{"id":8,"userName":"User 8","password":"Password8"},{"id":9,"userName":"User 9","password":"Password9"},{"id":10,"userName":"User 10","password":"Password10"}]
```