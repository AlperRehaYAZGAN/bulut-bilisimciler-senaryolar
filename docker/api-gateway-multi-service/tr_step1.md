# Docker Çoklu Servis Gateway Uygulaması

## Bu Senaryoda Birden Fazla Servisinize Gelen İstekleri Nasıl Yönlendirebileceğinizi Demoyla Öğreneceksiniz.  

###  Seviye: Başlangıç

Docker Container Runtime uygulaması kendi uygulama motoru ile Container Paketi haline getirilmiş uygulamaları çalıştırabilmekte ve deploy(dağıtıma çıkarma) operasyonlarını kolaylaştırabilmektedir. Kodlama dünyasında açık kaynak yazılım ekipleri tarafından geliştirilen büyük projeler de artık Docker Image'ları haline getirilip push-to-deploy kavramınca ürüne dönüşmektedirler. Bizler de bu senaryomuzda sizlerle Mikroservis mimarilerinde gelen isteği kendi iç servislerinize nasıl kolayca yönlendirebileceğinizi gerçekleştirmeniz için önemli bir kavram olan API Gateway kavramını [Traefik](https://traefik.io/) kullanarak gerçek bir senaryo ile öğreneceksiniz.  

[Mimari](https://cdn.bulutbilisimciler.com/public/images/pg/bba-scenario-gateway.png)


#### Talimatlar  

Uygulamalarımızı servis eder hale getirmek için sırasıyla aşağıdaki adımları gerçekleştirmemiz gerekmektedir.    

- ``docker --version`` komutunu çalıştırarak Docker servisinin çalıştığından emin olalım.  

- ``docker ps`` komutunu çalıştırarak güncel olarak çalışmakta olan servis var mı onu kontrol edelim ve hangi uygulamalar şu anda çalışmakta onları inceleyelim.  

- Docker motorumuz ayakta ve çalışmakta. Şimdi sizlere bu demo için özel olarak hazırlanmış bir kaynak deposunu çağırıp uygulamanızı başlatmanız için kod deposunu uzak kaynaktan ```git clone https://github.com/AlperRehaYAZGAN/bulut-bilisim-akademi-demo.git bba-demo``` komutuyla kodu indirelim.  

- İndirdiğimiz klasör dizinine ``cd bba-demo/3-api-gateway-multi-service`` diyerek gidelim.  

- Ardından sizlerle gerçekleştirmek istediğimiz mimari için ``docker-compose up -d`` komutunu çalıştıralım ve servisimizin çalışır duruma gelmesini bekleyelim.  

- Tebrikler ilk birden fazla servisi içeren uygulamalar topluluğunuzu çalıştırdınız! Şimdi çalıştırdığınız uygulamaların statü halini kontrol etmeniz için ``docker ps`` diyerek ayakta olan uygulamaları inceleyiniz.  

- Bu senaryo dahilinde bir adet hello-world uygulaması; bir adet dosya saklama servisi; bir tane de bu iki servise yönlendirme işlemi yapan bir Traefik API Gateway yazarak toplamda 3 adet uygulama ayağa kaldırmış oldunuz. ``docker ps`` komut çıktısını incelediğinizde bu kaynakları listede görüntüleyebiliyorsanız başarıyla uygulamaları ayağa kaldırmış ve hizmet veriyor hale getirmişsiniz demektir.  

- Çalışan uygulamaya erişmek için sağ yukarıda bulunan "Sunucuya Eriş" butonuna tıklayarak bütün uygulamalara yönlendirme işlemini gerçekleştiren API Gateway uygulamasını ayağa kaldırdığınız port olan "80" port numarasını girerek servisinize erişebilirsiniz.  

- Şimdi alt servis olan iki servise erişebilmek için sırasıyla ``/minio`` ve ``/hello`` uç noktalarına gitmeyi deneyerek farklı sunuculara nasıl ortak bir giriş noktasından erişebileceğinizi gerçekleştiriniz.  

- Tebrikler API Gateway uygulamanıza erişebildiniz ve bütün bu süreci Docker Temel Komutlarını kullanarak 5 dakikadan kısa bir süre içerisinde gerçekleştirdiniz.

Bu eğitimle birlikte Docker teknolojisini ve Bulut Bilişim kavramlarını kullanarak uygulamalar topluluğunuzu nasıl kolay birşekilde deploy(dağıtım) haline getirebileceğiniz konusunda senaryo gerçekleştirip incelediniz.  

Yeni Senaryolarla Öğrenmeye Devam.  


