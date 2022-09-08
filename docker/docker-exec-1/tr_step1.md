###  Seviye: Başlangıç  

Bu bölümde oluşturduğumuz bir Container'ın terminaline bağlanacağız ve çeşitli komutlar çalıştıracağız.

Container'ların kendine ait shell'i vardır. Çalışan bir container'a `docker exec komutu` ile bağlanabiliriz.

Örnek olarak, `docker container run --name websunucu -p 80:80 -d httpd` komutu ile busybox registry'sindeki default uygulamaya "websunucu" ismi verip 80:80 portunda detach modunda çalıştıralım ve en sağdaki "NAMES" sütununa dikkat edelim:

``` {.sh}
root@bulutbilisimciler:~# docker container run --name websunucu -p 80:80 -d httpd
>>3da5eb96ffa9449c06744323adf80b8cac159b860799dda2beae3496fd29b2e5
``` 

``` {.sh}
root@bulutbilisimciler:~# docker ps -a
>> CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS                     PORTS     NAMES
  f076aa4c49e8   busybox   "sh"      2 minutes ago   Exited (0) 2 minutes ago             websunucu
``` 

Ardından `docker container exec -it websunucu sh` komutu ile de "websunucu" ismini verdiğimiz bu container'ın shell'ine bağlanalım. Alpine tabanlı Linux dağıtımlarında shell'i "sh" komutu ile açarız. Ubuntu'da bu komut "bash" komutudur. Windows'da bu komut "powershell" komutudur. `-it` komutu, `--interactive` ve `--tty` komutlarının birleşimidir. Anlamı "bu container'a interaktif modda bağlan, komutlarımı bu container'ın içinde çalıştır ve bunu sağlamak için sözde bir terminal bağlantısı kur" demektir:

``` {.sh}
root@bulutbilisimciler:~#docker container exec -it websunucu sh
#

``` 
Gördüğümüz gibi komutu çalıştırdıktan sonra `#` simgesi ekranda belirdi. Artık bir Linux makine içinde ne yapabilirsek onu burada yapabileceğimizi biliyoruz.

Şimdi container'ların katmanlı yapılarından bahsedelim. Aynı image'ı kullanarak bir sürü farklı container kullanabiliriz. Her container sıfırdan başlatılır. Biz bir container'ın içinde bir şey değiştirdiğimizde, o şey image'da değişmez. Bunu Docker'ın sahip olduğu katmanlı dosya sistemi yapısı sağlar. 

Diyelim ki `hello-app` adında bir uygulamanın çalışacağı bir image yaratmak istiyoruz. Öncelikle kullanacağımız işletim sisteminin çekirdek olmayan hali olan base image'ı alıyoruz. Bu base image, ilk katman oluyor. Daha sonra `hello.sh` isimli uygulamayı base image'ın içine koyuyoruz ve burası da ikinci katman oluyor. `hello.sh` scripti bir shell uygulaması olduğu için başka bir şey eklememize gerek yok fakat bir Java uygulaması çalıştırıyor olsaydık, ikinci katmanda bir java runtime eklememiz gerekecekti. En son katmanda ise bu image çalıştırıldığında default olarak çalışacak uygulamayı belirliyoruz. Bu üç katmanı bir deste haline getiriyoruz ve buna bir `tag` atıyoruz, httpd adında. İşte tüm bu katmanları bir paket halinde bir araya getirebiliyoruz. Ve bu pakete de image adını veriyoruz. 

Docker bu image'ı `read-only` yani sadece okunabilir (R/O) vaziyette tutuyor ve üzerine 1 katman daha ekliyor, bu son katman `container yazılabillir katman` yani R/W katmanı. Docker bir image'dan container oluşturduğu zaman bu image'ın yeni bir kopyasını çıkarıp bundan bir container yaratmaz. Bunun yerine bu image read-only olarak yüklenir ve bunun üstüne bir yazılabilir katman ekler ve container böyle çalıştırılır. Container içinde yaptığımız tüm değişiklikler bu katmana yazılır ve sadece o container için geçerlidir. 

Aynı image'dan başka bir container oluşturacağımız zaman read-only layer'lar sabit tutulur ve üzerine boş bir R/W (yazılabilir) katmanı eklenir. Container içinde yaptığımız her işlem, yazılabilir katmanda saklanır. R/W katmanı sayesinde yeni bir dosya yarattığımızda, bu dosya base image'ın içinde gözükür. Bu dosyanın R/W katmanında tutulmasına rağmen base image'ın içinde gözükmesinin sebebi docker'ın `Union File System`idir. 

Biz ilk katmanda yer alan bir dosyada değişiklik yapmak istediğimizde, Union File System bu dosyanın bir kopyasını R/W katmanına kopyalar ve orijinal dosyayı gizler. Dosyada yapacağımız değişikliklerin burada gerçekleşmesini sağlar. Dosyanın orjinalinde değişiklik olmaz. 

Docker bunca zahmete şu yüzden giriyor: yeri geliyor aynı makine üstünde aynı image'dan günde onlarca container yarattığımız durumlar oluyor. Yaptığımız her değişiklik image'ların üstüne yazılsaydı, container başlatma sürelerimiz 1-2 saniyelerden 1-2 dakikalara çıkardı. Sanal makinaların başlatılma zahmetleri zaten bu şekilde olduğu için Docker piyasada şu anki konumuna sahip olabildi. Ayrıca biz bir base image'dan farklı farklı container'lar yarattığımız zaman, base image diskte defalarca tutulmuyor; ortak kullanılıyor. Bu sayede diskten de tasarruf edebiliyoruz.

Şimdi biraz komut çalıştıralım :)

Çalışmayan tüm container'ları silmek için `docker container prune` komutunu kullanabiliriz:

``` {.sh}
root@bulutbilisimciler:~# docker container prune
>> WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
Deleted Containers:
f10e4df260da4f48c1ef4e14fc324c6770fc3beaf2e55275e4e40be742f37f51
8447284a9213ba51968e1819a89e34c1b19f260e9e6ecb77a09e204fdf156518

Total reclaimed space: 0B
```


Yine `docker image prune -a` komutu ile sistemdeki tüm image'ları silebiliriz ve `docker image ls` komutu ile sistemdeki image'ları görüntüleyebiliriz:

``` {.sh}
root@bulutbilisimciler:~# docker image ls
>>  REPOSITORY                     TAG       IMAGE ID       CREATED        SIZE
httpd                          latest    b260a49eebf9   2 days ago     145MB
nginx                          latest    c919045c4c2b   3 months ago   142MB
```

Bir sonraki bölümde görüşmek üzere!
