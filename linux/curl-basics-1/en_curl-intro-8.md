Bu adres üzerine bu sefer POST metoduyla veri göndermeye çalışalım. Çıktıda `d` parametresiyle gönderilen user bilgileri; id, userName, password bilgileri bulunmaktadır. Authentication için gerekli bilgiler bu parametre ile gönderilir. `-H` parametresiyle de sayfaya HTTP isteği yapılırken kabul edeceği içerik türü(Content-Type) ve kabul(accept) türü gönderilmiştir. Burada "accept: **/* * " içerik olarak her mime type yani uzantı türünün her şey olabileceğini ifade eder. Content-Type: application/json ise gönderilen verinin json formatta olabileceğini anlatmaktadır.

```
$ curl -X POST "https://fakerestapi.azurewebsites.net/api/v1/Users" -H  "accept: */*" -H  "Content-Type: application/json; v=1.0" -d "{\"id\":0,\"userName\":\"testuser\",\"password\":\"abcdef\"}"

{"id":0,"userName":"testuser","password":"abcdef"}
```

Şimdi bu komutun sonuna `-v` parametresini ekleyelim. Bu şekilde oluşan trafik akışını, sertifika bilgilerini, istek yapılan adrese ait HTTP header bilgilerini, dönen durum kodunu ve cevap dönen sunucuya ait HTTP header bilgilerini görebiliriz. Aşağıdaki çıktıda olduğu gibi 200 OK kodu dönülmüş ve ortama ait bilgilere ilgili HTTP header bilgilerinden ulaşılmaktadır. 

```
$ curl -X POST "https://fakerestapi.azurewebsites.net/api/v1/Users" -H  "accept: */*" -H  "Content-Type: application/json; v=1.0" -d "{\"id\":0,\"userName\":\"testuser\",\"password\":\"abcdef\"}" -v

Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 20.50.2.11:443...
* TCP_NODELAY set
* Connected to fakerestapi.azurewebsites.net (20.50.2.11) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* successfully set certificate verify locations:
*   CAfile: /etc/ssl/certs/ca-certificates.crt
  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS handshake, Server key exchange (12):
* TLSv1.2 (IN), TLS handshake, Server finished (14):
* TLSv1.2 (OUT), TLS handshake, Client key exchange (16):
* TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS handshake, Finished (20):
* TLSv1.2 (IN), TLS handshake, Finished (20):
* SSL connection using TLSv1.2 / ECDHE-RSA-AES256-GCM-SHA384
* ALPN, server accepted to use http/1.1
* Server certificate:
*  subject: C=US; ST=WA; L=Redmond; O=Microsoft Corporation; CN=*.azurewebsites.net
*  start date: Mar 14 18:39:55 2022 GMT
*  expire date: Mar  9 18:39:55 2023 GMT
*  subjectAltName: host "fakerestapi.azurewebsites.net" matched cert's "*.azurewebsites.net"
*  issuer: C=US; O=Microsoft Corporation; CN=Microsoft Azure TLS Issuing CA 01
*  SSL certificate verify ok.
> POST /api/v1/Users HTTP/1.1
> Host: fakerestapi.azurewebsites.net
> User-Agent: curl/7.68.0
> accept: */*
> Content-Type: application/json; v=1.0
> Content-Length: 50
> 
* upload completely sent off: 50 out of 50 bytes
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Content-Type: application/json; charset=utf-8; v=1.0
< Date: Fri, 16 Sep 2022 21:17:07 GMT
< Server: Kestrel
< Transfer-Encoding: chunked
< api-supported-versions: 1.0
< 
* Connection #0 to host fakerestapi.azurewebsites.net left intact
```


Eğer yukarıda kullanılan komutun sonundaki parametrede tek bir v değilde iki v olursa; yani `-vv` parametresi kullanılırsa bu çıktıya ek olarak birde POST ile json formatta gönderilen bilgileri görebiliriz.

```
$ curl -X POST "https://fakerestapi.azurewebsites.net/api/v1/Users" -H  "accept: */*" -H  "Content-Type: application/json; v=1.0" -d "{\"id\":0,\"userName\":\"testuser\",\"password\":\"abcdef\"}" -vv

Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 20.50.2.11:443...
* TCP_NODELAY set
* Connected to fakerestapi.azurewebsites.net (20.50.2.11) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* successfully set certificate verify locations:
*   CAfile: /etc/ssl/certs/ca-certificates.crt
  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS handshake, Server key exchange (12):
* TLSv1.2 (IN), TLS handshake, Server finished (14):
* TLSv1.2 (OUT), TLS handshake, Client key exchange (16):
* TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS handshake, Finished (20):
* TLSv1.2 (IN), TLS handshake, Finished (20):
* SSL connection using TLSv1.2 / ECDHE-RSA-AES256-GCM-SHA384
* ALPN, server accepted to use http/1.1
* Server certificate:
*  subject: C=US; ST=WA; L=Redmond; O=Microsoft Corporation; CN=*.azurewebsites.net
*  start date: Mar 14 18:39:55 2022 GMT
*  expire date: Mar  9 18:39:55 2023 GMT
*  subjectAltName: host "fakerestapi.azurewebsites.net" matched cert's "*.azurewebsites.net"
*  issuer: C=US; O=Microsoft Corporation; CN=Microsoft Azure TLS Issuing CA 01
*  SSL certificate verify ok.
> POST /api/v1/Users HTTP/1.1
> Host: fakerestapi.azurewebsites.net
> User-Agent: curl/7.68.0
> accept: */*
> Content-Type: application/json; v=1.0
> Content-Length: 50
> 
* upload completely sent off: 50 out of 50 bytes
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Content-Type: application/json; charset=utf-8; v=1.0
< Date: Fri, 16 Sep 2022 21:16:28 GMT
< Server: Kestrel
< Transfer-Encoding: chunked
< api-supported-versions: 1.0
< 
* Connection #0 to host fakerestapi.azurewebsites.net left intact
{"id":0,"userName":"testuser","password":"abcdef"}
```


PUT metodu kullanarak HTTP isteği yaparsak POST  metoduna benzer şekilde veri göndeririz. Ancak POST metodu ile var olan veriyi görüntülemek için hedefte adına kayıtlı olan bilgileri kullanarak istek yapıp, ilgili veriyi getiriyoruz. PUT ile ilgili parametreleri göndererek yeni bir veri yaratıyoruz. 
Aşağıdaki örnekte de id, userName, passwprd bilgileri `-d` parametresi yardımıyla https://fakerestapi.azurewebsites.net/api/v1/Users/{id} adresine gönderilmiştir. Burada yer alan {id} bizim gönderdiğimiz parametrelerin etkileyeceği kullanıcı id'si olmalı. Biz oraya 3 yazarsak Users sayfası altındaki id'si 3 olan kullanıcıya gidip bizim gönderdiğimiz verileri yazacaktır.

```
$ curl -X PUT "https://fakerestapi.azurewebsites.net/api/v1/Users/3" -H  "accept: */*" -H  "Content-Type: application/json; v=1.0" -d "{\"id\":1,\"userName\":\"user1\",\"password\":\"deneme\"}"

{"id":1,"userName":"user1","password":"deneme"}
```

Yine yukarıdaki POST örneğinde bahsettiğim üzere `-v` ve `-vv` parametreleri ihtiyaca göre kullanılabilir.


Şimdi "https://fakerestapi.azurewebsites.net/api/v1/Users/" adresi altında id'si 3 olan kullanıcı bilgilerini görüntüleyelim.

```
$ curl -X GET -H "accept: */*" "https://fakerestapi.azurewebsites.net/api/v1/Users/3"

{"id":3,"userName":"User 3","password":"Password3"}
```



DELETE metodu ile HTTP isteğinde bulunup, id'si 3 olan kullanıcıyı sildirelim.

```
$ curl -X DELETE "https://fakerestapi.azurewebsites.net/api/v1/Users/3" -H  "accept: */*"
```
Yukarıda görüntülediğimiz id'si 3 olan kullanıcıyı yeniden görüntülemeye çalıştığımızda artık bu kullanıcının silinmiş olması gerekmektedir. Bu URL adreste bunu denediğinizde halen sonuca ulaşabilirsiniz çünkü bunlar gerçek adres değil sadece API denemesi yapmak için sunulan adreslerdir. Ama gerçek bir URL'e bu isteği yaptığınızda size 404 Not Found tarzı hata mesajı dönmesi gerekmektedir.
