### Template Oluşturma

Biraz da template database kavramı üzerinde duralım. 
Bir veritabanını default ayarları dışında oluşturmak ve bunun devamlılığını sağlamak istersek bunun için yeni bir `TEMPLATE` oluşturmamız gerekir. Oluşturmak istediğiniz standardı tasarladıktan sonra `template1 template_ismi` şeklinde yeni bir template oluşturabiliriz. Ve bu template ile veritabanlarımızı istediğimiz standartlarda oluşturabiliriz.
Default olarak bir postgresql kurduğunuzda 2 farklı template görürsünüz. Bunlardan `template0`'da değişiklik yapılamaz. Her oluşturduğunuz veritabanı aslında bu template0 standardı ile kurulur. Bu nedenle değiştirilemez. 
Fakat yeni bir standarta ihtiyacınız varsa, `template1` şablonunda gerekli değişikleri yapıp, yeni veritabanları bu şablonu kullanarak oluşturabilirsiniz. Örnek olarak;
Veritabanı oluşturabilmeniz için ya öncelikli bir kullanıcı olmalısınız ya da `CREATEDB` yetkisine sahip bir kullanıcınız olmalı. 

Öncelikle template1'e `\c template1` (connect anlamına gelir) diyerek bağlanıp bu template'te bir tablo oluşturalım.
```
postgres=# \c template1
You are now connected to database "template1" as user "postgres".
template1=# create table markalar (id int, marka_adi char(10));
CREATE TABLE
```
Daha sonra bu template'ten bir veritabanı oluşturup, oluşturduğumuz veritabanına bağlanarak `\dt` (description table) komutu ile tablonun otomatik bu veritabanında oluştuğunu görelim.

```
template1=# create database arabalar TEMPLATE template1;
CREATE DATABASE
template1=# \c arabalar 
You are now connected to database "arabalar" as user "postgres".
arabalar=# \dt
         List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | markalar | table | postgres
(1 row)
```
