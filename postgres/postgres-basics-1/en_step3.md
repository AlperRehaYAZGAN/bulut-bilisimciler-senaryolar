### Schema (Şema) Oluşturma 
Schema veritabanındaki tablo, view ve stored procedure gibi objeleri gruplamaya yarar. Bir objeyi bir şema altında yaratabilirsiniz veya bir şemanın altına transfer edebilirsiniz. Ayrıca şema bazlı yetki de verebilirsiniz. Yani user sadece izin verdiginiz şemanın altındaki objeleri görebilir diğerleri göremez. Normalde obje sayılarının fazlalığı yönetimi ve izinlerini oldukça zorlaştıracaktır. Her bir objeyi tek tek yetkilendirmek yerine şema bazında yetkilendirme yapmak daha uygun olacaktır. Postgresql default olarak oluşturduğunuz her objeyi, şema belirtmediğiniz sürece `public` şeması altında oluşturur.

Bir şema oluşturmak için aşağıdaki komutu kullanabiliriz. Aşağıdaki komut dizisine göre;
**bayi1** isimli bir şema yaratıldı ve **arabalar** veritabanında **markalar** isimli bir tablo oluşturularak bu şemaya eklendi. Böylece hem public hemde bayi1 şemasında markalar isminde 2 farklı tablomuz olmuş oldu.

```
arabalar=# create schema bayi1;
CREATE SCHEMA
arabalar=# create table bayi1.markalar(id int);
CREATE TABLE
```