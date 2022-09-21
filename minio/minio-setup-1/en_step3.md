Şimdi ise artık sistemimizi Docker kullanarak ayağa kaldırıyoruz.  
  
**Container ayağa kaldırma**, Container bileşenleri docker-compose kullanarak ayağa kaldırılacaktır.
  
- `docker-compose pull` komutu ile indirilen dosyalar üzerinden daha önce oluşturulmuş bir container kümesi ayağa kaldırmak için gerekli docker imajlarını indirmek için çalıştırıyoruz. Ekran çıktısı:
```
# cd /minio/
# docker-compose pull
[+] Running 0/5
 ⠼ minio2 Pulling                                                          4.5s
 ⠼ minio4 Pulling                                                          4.5s
 ⠼ nginx Pulling                                                           4.5s
 ⠼ minio3 Pulling                                                          4.5s
 ⠼ minio1 Pulling                                                          4.5
```  
  
- `docker images` komutu  ile indirilen imajları görebilirsiniz. Ekran çıktısı aşağıdaki gibi olmalıdır.  

```
# docker images
REPOSITORY            TAG                            IMAGE ID       CREATED         SIZE
quay.io/minio/minio   RELEASE.2022-08-11T04-37-28Z   f4bb411271e8   8 hours ago     220MB
nginx                 1.19.2-alpine                  6f715d38cfe0   24 months ago   22.1MB
```  
  
- `docker-compose up -d` komutu  ile /minio klasörü altında ilgili konfigürasyonları kullanarak container ayağa kaldırılmaktadır. `-d` ile daemon olarak çalıştırıyoruz. Ekran çıktımız aşağıdaki gibi olmalıdır.  
  
```
# docker-compose up  -d
[+] Running 14/14
 ⠿ Network minio_default     Created                                       0.0s
 ⠿ Volume "minio_data3-1"    Created                                       0.0s
 ⠿ Volume "minio_data3-2"    Created                                       0.0s
 ⠿ Volume "minio_data4-1"    Created                                       0.0s
 ⠿ Volume "minio_data4-2"    Created                                       0.0s
 ⠿ Volume "minio_data1-1"    Created                                       0.0s
 ⠿ Volume "minio_data1-2"    Created                                       0.0s
 ⠿ Volume "minio_data2-1"    Created                                       0.0s
 ⠿ Volume "minio_data2-2"    Created                                       0.0s
 ⠿ Container minio-minio1-1  Started                                       0.6s
 ⠿ Container minio-minio2-1  Started                                       0.7s
 ⠿ Container minio-minio3-1  Started                                       0.7s
 ⠿ Container minio-minio4-1  Started                                       0.4s
 ⠿ Container minio-nginx-1   Started                                       0.9s
```  
  
- `docker ps -a` komutu  ile çalışan container'lar görülebilir. Ekran çıktısı aşağıdaki gibi olmalıdır.  
  
```
# docker ps -a
CONTAINER ID   IMAGE                                              COMMAND                  CREATED         STATUS                   PORTS                                      NAMES
ee94b48b6d05   nginx:1.19.2-alpine                                "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes             80/tcp, 0.0.0.0:9000-9001->9000-9001/tcp   minio-nginx-1
c3515e9bd463   quay.io/minio/minio:RELEASE.2022-08-11T04-37-28Z   "/usr/bin/docker-ent…"   2 minutes ago   Up 2 minutes (healthy)   9000-9001/tcp                              minio-minio4-1
a235d2ae1535   quay.io/minio/minio:RELEASE.2022-08-11T04-37-28Z   "/usr/bin/docker-ent…"   2 minutes ago   Up 2 minutes (healthy)   9000-9001/tcp                              minio-minio1-1
4847d9c6d0ea   quay.io/minio/minio:RELEASE.2022-08-11T04-37-28Z   "/usr/bin/docker-ent…"   2 minutes ago   Up 2 minutes (healthy)   9000-9001/tcp                              minio-minio2-1
8b1c978745cf   quay.io/minio/minio:RELEASE.2022-08-11T04-37-28Z   "/usr/bin/docker-ent…"   2 minutes ago   Up 2 minutes (healthy)   9000-9001/tcp                              minio-minio3-1
```  
  
- Interaktif session üzerinde bulunan port kısmına `9001` yazıp aşağıdaki isim ve şifre ile arayüze bağlanabilirsiniz.  
  
```
Username: minioadmin
Pasword: minioadmin
```  

- Açılan "minio" ekranından şifre ve kullanıcı bilgilerini girerek S3 web-console erişebilirsiniz. Açılan ekranda "Bucket" oluşturabilir. Dosya bırakıp test edebilirsiniz. 
 
 