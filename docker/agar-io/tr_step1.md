# Docker ile Agar.io Oyununu Çalıştıralım  

## Bu Senaryoda Agar.io Çok Oyunculu Web Browser Oyununu Saniyeler içerisinde Çalıştırın  

###  Seviye: Başlangıç  

Docker Container Runtime uygulaması kendi uygulama motoru ile Container Paketi haline getirilmiş uygulamaları çalıştırabilmekte ve deploy(dağıtıma çıkarma) operasyonlarını kolaylaştırabilmektedir. Kodlama dünyasında açık kaynak yazılım ekipleri tarafından geliştirilen büyük projeler de artık Docker Image'ları haline getirilip push-to-deploy kavramınca ürüne dönüşmektedirler. Bizler de bu senaryomuzda sizlerle 2015 yılında çıkan ve 300 bin kişi tarafından canlı olarak oynanan bir oyun olan Agar.io oyununun açık kaynak replika projesi olan Ogar projesini birlikte saniyeler içerisinde çalıştıracağız ve isteyen herkesin bu uygulamaya erişebilmesini basit Docker komutlarını uygulayarak gerçekleştireceğiz.  

[Mimari](https://cdn.bulutbilisimciler.com/public/images/pg/bba-scenario-ogar.png)

#### Talimatlar  

Uygulamalarımızı servis eder hale getirmek için sırasıyla aşağıdaki adımları gerçekleştirmemiz gerekmektedir.  

- ``docker --version`` komutunu çalıştırarak Docker servisinin çalıştığından emin olalım.  

- ``docker ps`` komutunu çalıştırarak güncel olarak çalışmakta olan servis var mı onu kontrol edelim ve hangi uygulamalar şu anda çalışmakta onları inceleyelim.  

- Docker servisimiz ayakta ve çalışmakta. Şimdi Docker Container Image'ı olan "[Docker Ogar Image](https://hub.docker.com/r/alperreha/ogar3)" uygulamamızı ``docker run --name bba-ogar3 -p 8080:8080 -d alperreha/ogar3:1.0.4`` komutu ile ayağa kaldıralım.  

- Tebrikler Docker ile canlı oyun uygulamanızı çalıştırdınız! Şimdi çalıştırdığınız uygulamanın statü halini kontrol etmeniz için ``docker ps`` diyerek ayakta olan uygulamaları inceleyiniz.  

- Uygulamanızı "bba-ogar3" ismine ait bir şekilde listede görüntüleyebiliyorsanız başarıyla uygulamayı ayağa kaldırmış ve hizmet veriyor hale getirmişsiniz demektir.  

- Çalışan uygulamaya erişmek için sağ yukarıda bulunan "Sunucuya Eriş" butonuna tıklayarak uygulamayı ayağa kaldırdığınız port olan "8080" port numarasını veya o servisin önüne koyduğunuz yönlendirici servis olan (Gateway) "80" portunu girerek servisinize erişebilirsiniz.  

- Tebrikler Ogar Çok Oyunculu Web Browser oyun uygulamanıza erişebildiniz ve dış dünyaya hizmet veren bir uygulamayı 5 dakikadan kısa bir süre içerisinde dağıtıma(deploy) çıkarttınız.  

Bu eğitimle birlikte Docker ile Web Tarayıcı oyun uygulamanızı Temel Docker Komutları kullanarak çalıştırdınız ve HTTP Web Servis uygulamalarının sunucu tarafında nasıl çalıştırılabildiğini incelediniz.  

Yeni Senaryolarla Öğrenmeye Devam.  







