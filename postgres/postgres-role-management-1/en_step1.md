### Postgresql ROLE Komutu

Bu senaryoda veritabanında kullanıcı ve role oluşturmayı öğreneceğiz.

Öncelikle varsayalım ki  **arabalar** isimli bir veritabanı ve içerisinde **bayi1** isimli bir şemamız mevcut ve bu şemada **markalar** isimli tablomuz var.
```
postgres=# create database arabalar;
CREATE DATABASE
postgres=# \c arabalar 
You are now connected to database "arabalar" as user "postgres".
arabalar=# create schema bayi1;
CREATE SCHEMA
arabalar=# create table bayi1.markalar(id int);
CREATE TABLE
```
Şimdi de bir **role** oluşturalım. Burada `with inherit`'i kullanma amacımız rolün yetkilerini bu role sahip olacak diğer kullanıcılara kalıtımla aktarmak. Alttaki komut ile **muhasebeciler** isimli bir rol oluşturup, bu role bayi1 şemasındaki tüm tablolarda select, insert, update yetkisini `all privileges` diyerek tanımlıyoruz.
```
arabalar=# create role muhasebeciler with inherit ;
CREATE ROLE
arabalar=# grant all privileges on all tables in schema bayi1 to muhasebeciler;
GRANT
```
Son olarak da gizem isimli bir kullanıcı oluşturarak kullanıcımıza **muhasebeciler** rolünü atayalım.
```
arabalar=# create user gizem with password 'test123';
CREATE ROLE
arabalar=# grant muhasebeciler to gizem;
GRANT ROLE
```
Artık gizem kullanıcısı muhasebecilerin sahip olduğu tüm yetkilere sahip. Hadi bu yaptıklarımızı bir tabloda kontrol edelim. `\du` ile user bilgilerini görebiliriz.
Burada `muhasebeciler` bir `role` olduğu için loggin yetkisi bulunmuyor. `gizem ` kullanıcısı ise `muhasebeciler` role'ine dahil bir kullanıcı. Aşağıdaki gibi bir çıktı görmelisiniz.
```
arabalar=# \du
                                           List of roles
     Role name      |                         Attributes                         |    Member of    
--------------------+------------------------------------------------------------+-----------------
gizem              |                                                            | {muhasebeciler}
muhasebeciler      | Cannot login                                               | {}
postgres           | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

Şimdi kullanıcının yetkisini almayı ve silmeyi öğrenelim. `Revoke` verilen yetkiyi alır. `Drop` ise sistemden ilgili objeyi/kullanıcıyı kaldırmaya yarar. Aşağıdaki komutlarla bu işlemleri yapabilirsiniz.

Biz bu komutla bayi1 şemasına ait tüm tablolardaki tüm yetkileri gizem kullanıcısından alıp, sonrasında bu kullanıcıyı siliyoruz.
```
arabalar=# revoke all privileges on all tables in schema bayi1 from gizem;
REVOKE
arabalar=# 
arabalar=# drop user gizem;
DROP ROLE
```
Başka bir yöntem de şu olabilir. Örneğin sinem kullanıcısı için tüm yetkilerini postgres kullanıcına atayıp (reassing) ve owner'lığını aşağıdaki gibi alabiliriz.
```
postgres=# reassign owned by sinem to postgres ;
REASSIGN OWNED
postgres=# drop owned by sinem;
DROP OWNED
```

Bu senaryodaki öğreneceklerimiz bu kadar :)