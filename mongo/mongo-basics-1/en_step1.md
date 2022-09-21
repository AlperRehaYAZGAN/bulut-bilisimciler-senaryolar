### MongoDB Administration  
Bu örnek ortamımızda  temel Mongodb obje kavramlarını ve CRUD işlemlerini öğreneceğiz.  

####  Seviye: Başlangıç

### MongoDB Nedir?
MongoDB, yüksek hacimli verilerin depolanması için kullanılan, ihtiyaç duyulan sorgulama ve indeksleme ile istenilen esnekliğe sahip belge tabanlı(document-oriented) ve açık kaynak NoSQL veritabanıdır.

MongoDB’de her kayıt bir döküman olarak ifade edilir. Ve bu dökümanlar json formatı şeklinde saklanır. Genel olarak unstructered ve semi-structured dediğimiz verileri saklamamıza yarar. İlişkisel veri tabanlarıyla kıyaslayacak olursak, her bir obje aşağıdaki gibi adlandırılır.

![SQLvsMongoDB](https://www.researchgate.net/profile/Smaqil-Burney/publication/340622952/figure/fig4/AS:880217438564360@1586871599608/SQL-vs-MongoDB-terms.png)

Günümüzde aktif olarak kullanılan pek çok programlama dili için driver desteği bulunması bakımından bugün NoSQL sistemler içerisinde en çok tercih edilenlerden biridir diyebiliriz.

Hadi gelin şimdi birlikte, mongodb'ye bağlanalım ve bir kaç temel komut öğrenelim.
Mongodb default olarak 27017 portunu kullanır. Ve mongo shell ekranından bağlanıyorsanız, sadece `mongosh` diyerek veritabanına bağlanabilirsiniz. Eğer farklı bir port kullanıyorsanız `--port` parametresiyle aşağıdaki gibi belirtebilirsiniz. 
```
[bulutuser@test]$ mongosh --port 27018
MongoDB shell version v5.0.9
connecting to: mongodb://127.0.0.1:27018/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("c293e48d-f9d6-4043-8e65-b944db886196") }
MongoDB server version: 5.0.9
================
MongoDB > 
MongoDB > show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
```
Gördüğünüz gibi veritabanına bağlanmak çok basit. Bir Mongodb kurduğunuz zaman `show dbs` komutunda da göreceğiniz gibi default üç veritabanı (şema) hazır olarak gelir.
Bunların detaylarına bakacak olursanız,

`admin` : Kök (root) veritabanıdır. Bir kullanıcı admin’e bir şekilde eklenirse, bütün veritabanları için bütün erişim haklarını miras alır. Ayrıca sadece admin’den uygulanabilen bazı komutlar mevcuttur; örneğin sistemdeki bütün veri tabanlarının listelenmesi ya da sunucunun kapatılması gibi.

`local` :  MongoDB servisinin replikasyon işlemlerindeki bilgilerini ve kendine özgü bilgileri barındırdığı veritabanıdır. Ve hiçbir zaman kopyalanamaz.

`config`: Sharded cluster bilgileri gibi temel configurasyon bilgileri tutulur.