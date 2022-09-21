### OWNER Yapma

`postgres` kullanıcısına geçerek sinem  kullanıcısnı **arabalar** veritabanının sahibi yapalım.

```
postgres=# alter database arabalar owner to sinem ;
ALTER DATABASE
```

### TABLESPACE

Tablespace verilerin aslında fiziksel olarak saklandığı yerdir. Bizim aynı veritabanı içerisindeki farklı verileri, farklı disklerde saklama ihtiyacımız varsa yeni bir tablespace oluşturabiliriz. Örneğin bazı tablolarda performans ihtiyacınız olduysa veya genelde veritabanı yöneticileri indexlerin performansını arttırmak için sunucuya yeni ve hızlı bir disk ekleyip tablespace oluşturarak tabloları veya indeksleri bu alanda tutar.
Ve bu şekilde verileri farklı lokasyonlarda, disklerde tutmuş olur.

Postgresql'de default olarak 2 alan vardır.
1) pg_default : Template1 ve template0 şablonlarının varsayılan tablo alanıdır. 
2) pg_global : Metadata verisinin tutulduğu yerdir. Paylaşımlı sistem katalog verileri saklanır.

Şimdi farklı bir tablespace oluşturmak için öncelikle kendimize ait bir lokasyonda klasör oluşturmamız gerekiyor. Bizim burada örneğin /data2 diye farklı bir diskimiz sunucu üzerinde mevcut. (Siz linux shell'de mkdir -p /data2 diyerek yeni bir path oluşturabilirsiniz.)

Daha sonra `hizlialan` adında bir `TABLESPACE` oluşturuyoruz. Aşağıdaki select sorgusuyla 3 farklı tablespace olduğunu görebilirsiniz.
```
postgres=# CREATE TABLESPACE hizlialan LOCATION '/data2';
CREATE TABLESPACE
postgres=# select * from pg_tablespace ;
  oid  |  spcname   | spcowner | spcacl | spcoptions 
-------+------------+----------+--------+------------
  1663 | pg_default |       10 |        | 
  1664 | pg_global  |       10 |        | 
 16478 | hizlialan  |       10 |        | 
(3 rows)
```

Tablespace oluşturduktan sonra **hizlialan** içerisinde personel isimli bir tablo oluşturalım.
```
postgres=# CREATE TABLE personel(id int, name text) TABLESPACE hizlialan ;
CREATE TABLE
```
Aşağıdaki komut ile veritabanındaki tablolar hakkında detaylı bilgi alabiliriz. Bu örnekte personel tablosunun tablespace kısmının default olmadığını hizlialan olduğunu görebilirsiniz.

```
postgres=# select * from pg_tables where tablename='personel';
 schemaname | tablename | tableowner | tablespace | hasindexes | hasrules | hastriggers | rowsecurity 
------------+-----------+------------+------------+------------+----------+-------------+-------------
 public     | personel  | postgres   | hizlialan  | f          | f        | f           | f
(1 row)
```