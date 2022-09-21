### Yetkilendirme
Öncelikle veritabanımızda sinem isimli bir kullanıcı oluşturalım, yeni kullanıcıları postgres gibi yetkisi olan bir kullanıcıyla oluşturabiliriz. `\q` komutunu **quit** anlamına gelir veritabanından çıkmak için kullanabiliriz.
Veritabanına önceden postgres ile bağlıydık, çıkış yaptıktan sonra artık sinem kullanıcısıyla  giriş yapabilmek için, psql komutunda `-U (username), -d (dbname), -h (hostname/ip)` parametrelerini kullanmamız gerekiyor.

```
arabalar=# create user sinem with password 'test123';
CREATE ROLE
arabalar=# \q
[postgres@absol00sdt0 ~]$ psql -U sinem -d arabalar -h 10.10.x.x
Password for user sinem: 
psql (13.5)
Type "help" for help.
arabalar=> select * from araba ;
ERROR:  permission denied for table araba
```
Yukarıdaki çıktıda gördüğümüz gibi bize **'ERROR:  permission denied for table araba'** hatası veriyor. Çünkü **arabalar** veritabanında, sinem kullanıcısının `SELECT` yetkisi bulunmuyor.
Şimdi `GRANT` ile sinem kullanıcısına, **arabalar** veritabanındaki markalar tablosu için `SELECT`  ve bayi1 şeması için `USAGE` yetkisi verelim. Ardından sorguyu tekrardan çalıştıralım.

Yetki verme işlemini postgres veya yetkili başka bir kullanıcı ile yapmanız gerekmektedir. Ve yetkiyi vereceğiniz ilgili veritabanına bağlı olmalısınız. Aşağıdaki örnekte arabalar veritabanına postgres kullanıcısı ile yeniden bağlanılmıştır. (Linux shell'de yeniden psql diyerek bağlanabilir ve \c arabalar diyerek veritabanına geçebilirsiniz.)
```
arabalar=# grant select on markalar to sinem;
GRANT
arabalar=# \dn   (Bu komut mevcut şemaları listeler.)
  List of schemas
  Name  |  Owner   
--------+----------
 public | postgres
 bayi1  | postgres
(2 row)
arabalar=# grant usage on SCHEMA bayi1 to sinem; 
GRANT

arabalar=> select * from markalar ;
 id | marka_adi 
----+-------
(0 rows)
```
Gördüğünüz gibi select attığınızda artık hata almıyorsunuz. Bu yetkiler detaylandırılabilir. 
