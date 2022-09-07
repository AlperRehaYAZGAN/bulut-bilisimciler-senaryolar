### Bulut Bilişimciler Örnek Senaryolar  
Bu kaynak deposu Bulut Bilişimciler platformu için örnek senaryoları barındıran ve senaryo bilgilerini içeren depodur.   
https://github.com/katacoda/scenario-examples - Örnek senaryolar için.

#### Senaryolar  
Kolayca bilgisayarınıza kurup çalıştırabilmeniz için hazır config dosyalarının bulunduğu senaryo listesi:  
- 1-http-hello-world: Docker HTTP Hello World  
- 2-api-gateway-hello-world: Nginx Hello World  
- 3-api-gateway-multi-service: Traefik ve arkasında bir dosya depolama servisi; bir tane de hello world uygulamanızı Gateway üzerinden aynı domainden erişin.  
- 4-agar-io: Web Browser'ı ile  oynanabilen çok oyunculu bir balon oyunu açık kaynak replika projesi [Agar.io](https://agar.io)  
- 5-databases: Basit bir komutla ayağa kaldırabileceğiniz Postgresql veritabanı sunucusu
- 6-wordpress: Basit bir komutla servis verebileceğiniz Wordpress uygulaması  
  


#### Kullanım  

- Git deposunu lokal alanınıza çekin.  
```sh
$ git clone https://gitlab.bulutbilisimciler.com/bb-public/scenarios bulut-bilisim-demo
```  

- Proje dizinine gidin.  
```sh
$ cd bulut-bilisim-demo
```  

- İstediğiniz demo klasörüne gidin.  
```sh
$ cd docker/agar-io
```  

- İlgili proje ile ilgili adımların bulunduğu bilgilerinin bulunduğu dosyayı inceleyin.  
```sh
$ cat index.json
```  
  
- Senaryo step dosyalarını inceleyerek adımları gerçekleştirin.  
```sh
$ cat tr_step1.md
```  

- Senaryoların tadını çıkarın...



