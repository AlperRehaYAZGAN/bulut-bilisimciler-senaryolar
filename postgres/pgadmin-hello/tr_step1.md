# Docker ile Postgresql Veritabanına Giriş  

## Bu Senaryoda Postgresql Veritabanını Saniyeler İçerisinde Çalıştırın  

###  Seviye: Başlangıç  

Docker Container Runtime uygulaması kendi uygulama motoru ile Container Paketi haline getirilmiş uygulamaları çalıştırabilmekte ve deploy(dağıtıma çıkarma) operasyonlarını kolaylaştırabilmektedir. Bütün bu süreçleri kendi ana motoru ile yapan Docker sektörde bütün alanlarda hizmet veren uygulamaları destekleyen ve onları hizmet veren hale getirmiştir. Bu senaryomuzda sizlerle birlikte çok basit komutlarla [Postgres](https://www.postgresql.org/) veritabanını kuracağız ve admin arayüzü desteği veren [PgAdmin](https://www.pgadmin.org/) uygulaması ile veritabanına erişeceğiz.

[Mimari](https://cdn.bulutbilisimciler.com/public/images/pg/bba-scenario-pgadmin.png)

#### Talimatlar  

Uygulamalarımızı servis eder hale getirmek için sırasıyla aşağıdaki adımları gerçekleştirmemiz gerekmektedir.  

- ``docker --version`` komutunu çalıştırarak Docker servisinin çalıştığından emin olalım.  

- ``docker ps`` komutunu çalıştırarak güncel olarak çalışmakta olan servis var mı onu kontrol edelim ve hangi uygulamalar şu anda çalışmakta onları inceleyelim.  

- Docker motorumuz ayakta ve çalışmakta. Şimdi sizlere bu demo için özel olarak hazırlanmış bir kaynak deposunu çağırıp uygulamanızı başlatmanız için kod deposunu uzak kaynaktan ```git clone https://github.com/AlperRehaYAZGAN/bulut-bilisim-akademi-demo.git bba-demo``` komutuyla kodu indirelim.  

- İndirdiğimiz klasör dizinine ``cd bba-demo/5-databases`` diyerek gidelim.  

- Ardından sizlerle gerçekleştirmek istediğimiz mimari için ``docker-compose up -d`` komutunu çalıştıralım ve servisimizin çalışır duruma gelmesini bekleyelim.  

- Tebrikler ilk Postgres servisinizi çalıştırdınız! Şimdi çalıştırdığınız uygulamaların statü halini kontrol etmeniz için ``docker ps`` diyerek ayakta olan uygulamaları inceleyiniz.  

- Bu senaryo dahilinde bir adet Postgres veritabanı ve veritabanına arayüz üzerinden erişmek için PgAdmin uygulamasını çalıştırdınız. ``docker ps`` komut çıktısını incelediğinizde bu kaynakları listede görüntüleyebiliyorsanız başarıyla uygulamaları ayağa kaldırmış ve hizmet veriyor hale getirmişsiniz demektir.  

- Veritabanına giriş şifreleriniz docker-compose.yaml dosyasının içerisinde tanımlanmaktadır. Dilerseniz oradan bakabilirsiniz veya değiştirebilirsiniz.  
(PgAdmin Kullanıcı Adı:"user@domain.com" PgAdmin Şifre:"1020304050"; Postgresql Kullanıcı Adı:"mysuperuser" Postgresql Şifre:"mysecretpass") uygulamaya erişmek için sağ yukarıda bulunan "Sunucuya Eriş" butonuna tıklayarak uygulamayı veritabanı arayüz programı olan PgAdmin'i ayağa kaldırdığınız port olan "8080" port numarasını girerek servisinize erişebilirsiniz.  

- Tebrikler ilk veritabanı sisteminizi çalıştırdınız ve erişebildiniz. Şimdi PgAdmin arayüzüne giriş yaparak veritabnaı sistemini tanıyıp geliştirmeler yapabilirsiniz.  

Bu eğitimle birlikte Docker ile Veritabanı Sistemlerinden Postgresql Servisini Temel Docker Komutları kullanarak 5 dakikadan kısa bir süre içerisinde dağıtıma(deploy) çıkarttınız ve sunucu tarafında nasıl çalıştırılabildiğini incelediniz.  

Yeni Senaryolarla Öğrenmeye Devam.  







