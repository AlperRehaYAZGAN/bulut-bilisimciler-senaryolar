## PostgreSQL

####  Seviye: Başlangıç

### PostgreSQL Nedir?
![](https://cdn.wmaraci.com/nedir/PostgreSQL.png)

PostgreSQL ya da Postgres, özgür ve açık kaynak kodlu, SQL destekli bir nesne ilişkisel veritabanı yönetim sistemidir.SQL dilinin güvenlik, depolanabilirlik ve ölçeklendirilebilme özelliklerinden faydalanan PostgreSQL, birçok alanda kullanılmaktadır.
Buradaki hiyerarşik yapı genelden özele gidecek olursak, **sunucu > veritabanı > şema > tablo** şeklindedir.

### Veritabanlarını Yönetme

Bu bölümde, veritabanlarının yönetimi hakkında temel komutları öğreneceğiz.

#### Veritabanı Oluşturma ve Görüntüleme

Öncelikle basit bir veritabanı yaratak başlayalım.
`create database bulutbilisimciler ;`
```
postgres=# create database bulutbilisimciler ;
CREATE DATABASE
``` 
Var olan veritabanlarını görüntülemek için iki farklı komut kullanabiliriz. Bunlardan ilki sistem view'ı olan pg_database tablosundan select çekmek olabilir.
İkicisi olarak ise  `\l` ' yi kullanabiliriz. Postgresql'in kısa yollarından biridir. Detaylı kısa yollar için `\?` ile tüm komutları bulabilirsiniz.
`SELECT datname FROM pg_database;`
```
      datname      
-------------------
 postgres
 template1
 template0
 bulutbilisimciler
(4 rows)
```
