### Minio Kurulumu

Bu bölümde, Bulut Bilişimciler interaktif platformumuzda bir dağıtık veri saklama çözümü olan S3 Obje tabanlı MinIO çözümünü ayağa kaldıracağız.MinIO obje tabanlı bir veri saklama çözümü olup yaygın olarak açık kaynak çözümlerde kullanılmaktadır. 

![MinIO Mimaisi](https://min.io/resources/img/home/features/scalability.svg)

+ **Kurulum için gerekli dosyaların temin edilmesi**, Docker-Compose çoklu sayıda container bileşenini tek bir konfigürasyon dosyası altında çalıştırma ve bir bütün olarak haberleştirme ve paketleme çözümüdür. Bu adımda gerekli olan dosyalarımızı ilgili klasöre indireceğiz.

- `cd /`  
  
- `mkdir /minio` : cd komutu, ile ilgili dizin altına gidiyoruz
  
- `cd /minio` : mkdir komutunu bir dizin oluşturmak için kullanıyoruz

- `pwd` : hangi dizinde olduğumu yazdırıyoruz. ("/minio" çıktısını görmelisiniz)  

- `ls  -lrt` : Bu dizinde kaç tane dosya olduğunu görmek için çalıştırıyoruz. ("total 0" çıktısını görmelisiniz)  
  
Şimdi ihtiyacımız olan dosyaları `wget` komutu ile  minio ortamlarından çekeceğiz. (`wget`  komutunu kullanarak web servislerine istek gönderebilirsiniz.)  
  
- `wget -O docker-compose.yaml https://github.com/minio/minio/blob/master/docs/orchestration/docker-compose/docker-compose.yaml?raw=true` : bu komut çıktısı aşağıdaki gibi olmalıdır.  

```
Connecting to github.com (140.82.121.4:443)
Connecting to github.com (140.82.121.4:443)
Connecting to raw.githubusercontent.com (185.199.111.133:443)
saving to 'docker-compose.yaml'
docker-compose.yaml  100% |********************************|  1579  0:00:00 ETA
'docker-compose.yaml' saved
```

- Şimdi ise bütün bu servisimizin önünde gateway görevi üstlenecek Nginx servis dosyalarını da indiriyoruz.  
  
- `wget -O nginx.conf https://github.com/minio/minio/blob/master/docs/orchestration/docker-compose/nginx.conf?raw=true`  
  
```
Connecting to github.com (140.82.121.3:443)
Connecting to raw.githubusercontent.com (185.199.111.133:443)
saving to 'nginx.conf'
nginx.conf           100% |********************************|  3071  0:00:00 ETA
'nginx.conf' saved
```  
  
- Şimdi dizindeki dosya sayımızı kontrol ediyoruz.  
  
- `ls  -lrt` : Bu komut çıktısında aşağıdaki çıktıyı elde etmelisiniz.  
  
```
total 8
-rw-r--r--    1 root     root          1579 Aug 12 06:04 docker-compose.yaml
-rw-r--r--    1 root     root          3071 Aug 12 06:04 nginx.conf
```  
