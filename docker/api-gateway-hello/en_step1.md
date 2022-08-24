# Docker NGINX Hello World

## Bu Senaryoda ilk NGINX API Gateway uygulamanızı dağıtıma çıkartacaksınız.  

###  Seviye: Başlangıç

Docker Container Runtime uygulaması kendi uygulama motoru ile Container Paketi haline getirilmiş uygulamaları çalıştırabilmekte ve deploy(dağıtıma çıkarma) operasyonlarını kolaylaştırabilmektedir. Kodlama dünyasında açık kaynak yazılım ekipleri tarafından geliştirilen büyük projeler de artık Docker Image'ları haline getirilip push-to-deploy kavramınca ürüne dönüşmektedirler. Bizler de bu senaryomuzda sizlerle dış dünya tarafından erişime açılabilecek ve dış dünyadan gelen istekleri kendi iç servislerimize yönlendirecek bir İstek Yönlendiricisi (API Gateway) yazıp bu servisi basit Docker komutlarını uygulayarak bir servis haline getireceğiz.  

#### Talimatlar  

Uygulamalarımızı servis eder hale getirmek için sırasıyla aşağıdaki adımları gerçekleştirmemiz gerekmektedir.    

- ``docker --version`` komutunu çalıştırarak Docker servisinin çalıştığından emin olalım.  

- ``docker ps`` komutunu çalıştırarak güncel olarak çalışmakta olan servis var mı onu kontrol edelim ve hangi uygulamalar şu anda çalışmakta onları inceleyelim.  

- Docker servisimiz ayakta ve çalışmakta. Şimdi Docker Container Image'ı olan "[Docker NGINX Image](https://hub.docker.com/_/nginx)" uygulamamızı ``docker run --name bba-nginx -d -p 8080:80 nginx:1.22.0-alpine`` komutu ile ayağa kaldıralım.  

- Tebrikler ilk NGINX uygulamanızı çalıştırdınız! Şimdi çalıştırdığınız uygulamanın statü halini kontrol etmeniz için ``docker ps`` diyerek ayakta olan uygulamaları inceleyiniz.  

- Uygulamanızı "bba-nginx" ismine ait bir şekilde listede görüntüleyebiliyorsanız başarıyla uygulamayı ayağa kaldırmış ve hizmet veriyor hale getirmişsiniz demektir.  

- Çalışan uygulamaya erişmek için sağ yukarıda bulunan "Sunucuya Eriş" butonuna tıklayarak uygulamayı ayağa kaldırdığınız port olan "8080" port numarasını girerek servisinize erişebilirsiniz.  

- Tebrikler Nginx uygulamanıza erişebildiniz ve dış dünyaya hizmet veren bir uygulamayı 5 dakikadan kısa bir süre içerisinde dağıtıma(deploy) çıkarttınız.  

Bu eğitimle birlikte Docker ile ilk Nginx uygulamanızı Temel Docker Komutları kullanarak çalıştırdınız ve HTTP Web Servis uygulamalarının sunucu tarafında nasıl çalıştırılabildiğini incelediniz.  

Yeni Senaryolarla Öğrenmeye Devam.  







