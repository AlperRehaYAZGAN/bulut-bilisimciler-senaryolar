# Docker HTTP Hello World  

## Bu Senaryoda ilk HTTP Hello World Uygulamanızı Gerçekleştireceksiniz.  

###  Seviye: Başlangıç

Docker kendi "Deamon" ismi veirlen ana motoru ile birlikte Container Servislerini oluşturmakta yönetmekte ve son verebilmektedir. Bu sebeple uygulama geliştiricisi tarafından kodlanan ve dağıtıma çıkmaya hazır olan kodlar bu ana motor-Deamon- ile iletişime geçip paket haline getirilerek basit komutlar ile dağıtıma çıkabilmektedirler. Sizlerle şimdi dış dünya tarafından erişilebilmesi için HTTP Web Servisi yazacağız ve bu servisi basit Docker komutlarını öğrenerek herkes tarafından erişilebilir bir hale getireceğiz.  

[Mimari](https://cdn.bulutbilisimciler.com/public/images/pg/bba-scenario-hello-world.png)  


#### Talimatlar  

Uygulamalarımızı servis eder hale getirmek için sırasıyla aşağıdaki adımları gerçekleştirmemiz gerekmektedir.    

- ``docker --version`` komutunu çalıştırarak Docker servisinin çalıştığından emin olalım.  

- ``docker ps`` komutunu çalıştırarak güncel olarak çalışmakta olan servis var mı onu kontrol edelim ve hangi uygulamalar şu anda çalışmakta onu inceleyelim.  

- Docker servisimiz ayakta ve çalışmakta. Şimdi Docker Halka Açık Mağazasından Kavram İspatı(Proof-of-Concept) Container Image'ı olan "[Docker HTTP Hello World](https://hub.docker.com/r/crccheck/hello-world)" uygulamamızı ``docker run -d --rm --name bba-http-test -p 8080:8000 crccheck/hello-world`` ayağa kaldıralım.  

- Tebrikler ilk uygulamanızı çalıştırdınız! Şimdi çalıştırdığınız uygulamanın statü halini kontrol etmeniz için ``docker ps`` diyerek ayakta olan uygulamaları inceleyiniz.  

- Uygulamanızı "bba-http-test" ismine ait bir şekilde listede görüntüleyebiliyorsanız başarıyla uygulamayı ayağa kaldırmış ve hizmet veriyor hale getirmişsiniz demektir.  

- Çalışan uygulamaya erişmek için sağ yukarıda bulunan "Sunucuya Eriş" butonuna tıklayarak uygulamayı ayağa kaldırdığınız port olan "8080" port numarasını girerek servisinize erişebilirsiniz.  

- Tebrikler uygulamanıza erişebildiniz ve dış dünyaya hizmet veren bir uygulamayı 5 dakikadan kısa bir süre içerisinde dağıtıma(deploy) çıkarttınız.  

Bu eğitimle birlikte Docker ile ilk uygulamanızı Temel Docker Komutları kullanarak çalıştırdınız ve HTTP Web Servis uygulamalarının sunucu tarafında nasıl çalıştırılabildiğini incelediniz.  

Yeni Senaryolarla Öğrenmeye Devam.  







