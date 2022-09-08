###  Seviye: Başlangıç  
  
Burası Container yapılarını keşfetmeniz ve Docker' ı öğrenmeniz için oluşturulmuş playground ortamıdır.  

#### Docker Nedir?

Docker, açık kaynak bir Container motorudur. Daha iyi anlamak için mimarisini ve bileşenlerini inceleyelim:

![Docker Mimaisi](https://cdn.bulutbilisimciler.com/public/images/docker-infra.png)

+ **Docker Client**, docker komutlarını çalıştırdığınız komut satırı arayüzü aracıdır. Gelen talepleri Docker API üzerinden Docker Daemon' a iletir.
+ **Docker Host** üzerinde **Docker Daemon** çalışmaktadır. 
+ **Docker Daemon**,  API üzerinden gelen istekleri dinlemekte ve gerçekleştirmektedir. Tüm container süreçleri burada yönetilir.
+ **Docker Registry** ise açık kaynaklı olarak image' larınızı yükleyebileceğiniz ve **DockerHub**' da paylaşabileceğiniz bir kayıt defteri aracıdır. Docker içerisinde çalıştırabileceğiniz image' lar burada saklanır. DockerHub, docker tarafından hizmet veren herkesin kullanımına açık public bir kayıt defteridir.
+ **Docker Image**, container oluştururken kullandığımız template'lerdir. Çalışacak uygulamanızın ve uygulamanızın altyapısında çalışan gerekli işletim sistemi kütüphanelerinin bulunduğu bir yapıdır. Container' ların yeteneklerini ve ihtiaçlarını tanımlayan metadata verilerini de saklamaktadır.
+ **Docker Container**, docker image' lardan oluşturulan uygulamalardır. Docker Image'ın çalışan bir örneğidir. Uygulamayı çalıştırmak için gereken tüm paketleri containerlar bünyesinde tutmaktadır. Image bir şablondur ve containerlar da bu şablonun çalışan bir kopyasıdır. 


#### Container nedir?

Container'lar içlerinde uygulamayı, uygulamanın çalışmasını sağlayan sistem araçlarını (dependencies) ve sistem kütüphanelerini (libraries) barındırır. Bir "Container Engine" olan Docker ise sanal makine görevi gören ama sanal makine olmayan bu container'ları yaratmayı sağlar. Container'lar sanal makinelere benzetilebilir fakat bilinmelidir ki Container'lar sanal makineler kadar kaynak tüketmezler. Çünkü tüm işletim sistemi gereksinimlerini, üzerinde kurulu oldukları işletim sistemi ile ortak kullanırlar. Container'ların boyutları da çok küçüktür (ortalama 100MB). Sistem yönetimini oldukça kolay bir hale getirirken, kaynak israfını da dramatik bir şekilde azaltan Container teknolojisi, sektörde oldukça önemli bir yer edinmiştir.


#### Öğrenme Hedefleri

Dcoker Playground ortamını tamamladıktan sonra;

+ Container oluşturma, çalıştırma, silme, listeleme gibi işlemleri yapabileceksiniz.
+ Docker Image yapısına ve komutlarına hakim olacaksınız.
+ Dockerfile komutlarına hakim olacak ve katmanlı dockerfile dosyalarıyla çalışabileceksiniz.
+ Docker üzerinde Data Volume ve Bind Volume tanımlaması yapabilecek, bunları container içerisine bağlayabileceksiniz.
+ Docker Network objeleri üzerinde işlemler yapabileceksiniz.



## Temel Komutlar  
Bu bölümde temel Docker komutları üzerinde duracağız.

`docker` komutunu kullanarak docker komutlarına dair seçenekleri, yöentim komutlarını ve diğer tüm komutları açıklamalarıyla birlikte görüntüleyebilirsiniz:

- İlk Komut: `docker`  
```sh
>> Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default
                           "/root/.docker")
  -c, --context string     Name of the context to use to connect to the
                           daemon (overrides DOCKER_HOST env var and
                           default context set with "docker context use")
  -D, --debug              Enable debug mode
``` 


- İkinci Komut:  `docker images --help`
```sh
root@bulutbilisimciler:~# 
>> Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs

``` 


- Üçüncü Komut: `docker version`  
docker client ve docker engine hakkında detaylı bilgileri öğrenebilirsiniz. Aynı zamanda docker client'ın docker daemon ile sorunsuz bir şekilde iletişime geçtiğini test etmiş olacaksınız:

```sh
# docker version
>> Client:
 Cloud integration: v1.0.22
 Version:           20.10.12
 API version:       1.41
 Go version:        go1.16.12
 Git commit:        e91ed57
``` 


- Dördüncü Komut: `docker info`  
komutu ile docker yapınız hakkında detaylı bilgilere sahip olabilirsiniz. Docker üzerinde oluşturduğunuz container bilgileri (running, paused, stopped), image bilgileri, storage driver bilgileri, sistem üzerinde swarm'ı aktif edip etmediğinize dair bilgiler gibi genel bilgileri elde edebilirsiniz:

```sh
# docker info
>> Client:
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc., v0.7.1)
  compose: Docker Compose (Docker Inc., v2.2.3)
  scan: Docker Scan (Docker Inc., v0.17.0)
``` 


- Beşinci Komut: `docker -D info`  
komutu ile docker üzerinde debug modu aktif hale getirebilirsiniz:

```sh
# docker -D info
>> Client:
 Context:    default
 Debug Mode: true
 Plugins:
  buildx: Docker Buildx (Docker Inc., v0.7.1)
  compose: Docker Compose (Docker Inc., v2.2.3)
  scan: Docker Scan (Docker Inc., v0.17.0)
``` 

- Altıncı Komut: `docker container run hello-world`  
komutu  _hello-world_ isimli image ile yeni container oluşturur ve başlatır. Docker Daemon, Image' ın localde olup olmadığını kontrol eder. Image localde yer alıyorsa bu image'ı kullanarak yeni bir container oluşturur. Eğer image lokalde yoksa varsayılan kayıt defteri olan hub.docker.com adresinde _hello-world_ isimli image'ı sorgular. Burada image yer alıyorsa image'ı locale indirir ve bu image'ı baz alarak yeni bir container oluşturur ve çalıştırır. Böylece servis ayağa kalkmış olur:

```sh
# docker container run hello-world
>> Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
``` 


- Yedinci Komut: `docker search <imageName>`  
komutu ile istediğiniz image'ı hub.docker.com adresinde arayabilir ve detaylı bir liste elde edebilirsiniz:

```sh
# docker search centos
>> NAME                                         DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
   centos                                       The official build of CentOS.                   7190      [OK]
``` 

- Sekizinci Komut: `docker pull <imageName>` komutu ile belirtilen image'ı, hub.docker.com adresinden sisteminize çekebilirsiniz: Örneğin httpd image'ı için:

```sh
# docker pull httpd
>>Using default tag: latest
latest: Pulling from library/httpd
42c077c10790: Pull complete
77a357ba66a8: Pull complete
e9e2f87fc2ce: Pull complete
0b3c9bceb738: Pull complete
de91965861a5: Pull complete
Digest: sha256:f899e432292e4ee92772d35e43b2e3dcf30042b1c6385d33f00a9300c69ee729
Status: Downloaded newer image for httpd:latest
docker.io/library/httpd:latest
``` 


- Dokuzuncu komut: `docker images`  
komutuyla sistemdeki image'ları listeleyebilirsiniz:

```sh
# docker images
>>REPOSITORY                     TAG       IMAGE ID       CREATED        SIZE
httpd                          latest    b260a49eebf9    a seconds ago     145MB
``` 



- Onuncu komut: `docker container run --help`  
komutu ile container oluştururken kullanabileceğiniz parametrelere dair bilgi edinebilirsiniz:

```sh
# docker container run --help
>> Usage:  docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
      --add-host list                  Add a custom host-to-IP mapping
                                       (host:ip)
  -a, --attach list                    Attach to STDIN, STDOUT or STDERR
      --blkio-weight uint16            Block IO (relative weight),
                                       between 10 and 1000, or 0 to
                                       disable (default 0)
      --blkio-weight-device list       Block IO weight (relative device
                                       weight) (default [])
``` 

Docker'da container üzerinde yapacağımız işlemlere geçmeden önce, önemli bir kaç komuta bakalım. Öncelikle `docker container run` komutu,  `docker container create` ve `docker container start` komutunun birleşimidir.

Her image'da, o image'dan bir container create ettiğimiz zaman default çalışması için ayarlanmış bir uygulama vardır. Container, bu uygulama çalıştığı sürece ayakta kalır. Uygulama çalışmayı bıraktığında container da kapatılır.

Peki image'ın içinde sadece tek bir uygulama mı var? Hayır bir Docker image'ının içinde birden fazla uygulama olabilir. Sadece tek bir uygulama içermelidir gibi bir kural yok. Fakat Docker, container start edildiğinde default çalışması için yalnız tek bir uygulamanın ayarlanmasına izin verir. Bunun hangi uygulama olacağını container yaratılırken belirtebiliriz.

`docker container run -d -p 80:80 httpd` komutunu çalıştırırsak, httpd registry'sindeki default uygulamayı "80:80" portundan çağırırız. "-d" komutu sayesinde container'ı detach ederiz yani arkaplanda çalıştırırız. Yani loglarını/çıktılarını kendi shell'imizde görmeyiz ama container arkada çalışmaya devam eder:

``` {.sh}
root@bulutbilisimciler:~# docker container run -d -p 80:80 httpd
>> 
``` 

Gördüğünüz gibi herhangi bir çıktı alınmadı fakat container'ın arkaplanda çalıştığını biliyoruz. O halde çalışan/çalışmayan tüm container'larımızı görmek için `docker container ls -a` veya `docker ps -a` komutunu çalıştıralım. Bu iki komut da aynı görevi görür:

```sh
# docker container ls -a
>> CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS                       PORTS     NAMES
   940d1da952e5   httpd     "httpd-foreground"   5 seconds ago   Up 4 seconds   0.0.0.0:80->80/tcp   musing_ardinghelli
``` 

```sh
# docker ps -a
>> CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS                       PORTS     NAMES
   940d1da952e5   httpd     "httpd-foreground"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp   musing_ardinghelli
``` 

Container'ları silmek için ise `docker container rm` diyip container'ların ID'lerinin ilk 3-digit'ini girebiliriz. Bu komut çalışan container'ları silemez. Çalışan bir container'ı silmek için `docker container rm -f ilk3Digit` komutunu kullanabiliriz. 

```sh
# docker container rm 940
>> Error response from daemon: You cannot remove a running container 940d1da952e5d3ae548786286f3aa4f0cc38df67db867194b1fd1be1b3b882d3. Stop the container before attempting removal or force remove
``` 

```sh
# docker container rm -f 940
>> 940

``` 

Bu komutların ardından container listeleme yani `docker container ls -a` komutunu çalıştıralım ve ayakta container olmadığını görelim:

``` {.sh}
root@bulutbilisimciler:~# docker container ls -a 
>> CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

``` 

Bir sonraki bölümde görüşmek üzere!
