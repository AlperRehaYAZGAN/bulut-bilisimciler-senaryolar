###  Seviye: Başlangıç

+ Sistem güncelleme, paket Komutları, Kurulumları ve Yönetimi

Linux kullanırken mutlaka bilinmesi gerekenler arasında; sistemi güncelleme, program kurma ve kurulu programları kaldırma gibi işlemleri yerine getirmek vardır. 

İlk olarak sistemi güncelleme işlemi ile başlayalım. Linux sistemleri, kullanıcının ihtiyacı olduğunda, programa kolayca ulaşabilmesini sağlayacak program paketlerini içinde bulunduran kendi paket depolarına(repository) sahiptirler. Farklı Linux dağıtımları için bu paketler farklılık gösterebildiği için farklı Linux dağıtımlarının da kendi paketleri üzerinde işlem yapabilmek için farklı komutları vardır.

++ CentOS dağıtımlarında manuel paketler `rpm` aracı ile; repo paketleri `yum` aracı ile yüklenirler ve repolar **/etc/yum.repos.d** dosyasında bulunur.

++ Debian dağıtımlarında manuel paketler `dpkg` aracı ile; repo paketleri `apt` aracı ile yüklenirler ve repolar **/etc/apt/sources.list** dosyasında bulunur.

Şimdi Debian üzerinde sistem güncellemesi yaparken en sık kullandığımız komutlara bakalım.

`apt-get update` komutu güncelleme işleminden önce nelerin güncellenmesi gerektiğine bakarak sistemde güncellenmesi gereken doğru paketlerin güncellenmesini sağlıyor. Kısacası bu komutun amacı sadece depolarda yer alan yenilikleri kontrol etmektir:
``` {.sh}
bulutbilisimciler@playground:~$ apt-get update
>>> Reading package lists... Done
```  

`apt-get upgrade` komutu ise `apt-get update` komutunun depolardan kontrol edip bildirmiş olduğu ve güncellenmesi gereken paketleri son versiyonlarına günceller.

**NOT**: `apt-get dist-upgrade` komutu ise `apt-get upgrade` komutundan farklı olarak sadece güncelleme yapmakla kalmaz; sistemdeki gereksiz paketleri de siler.

Debian üzerinde `dpkg` ve `apt` araçlarının aldıkları parametrelerle ve argümanlarla devam edelim.

`dpkg -l` komutu sistemdeki paketleri listeler:
``` {.sh}
bulutbilisimciler@playground:~$ dpkg -l
>>> Desired=Unknown/Install/Remove/Purge/Hold  
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend   
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)  
||/ Name                           Version                            Architect>
ii  accountsservice                0.6.55-0ubuntu12~20.04.5           amd64    >  
ii  adduser                        3.118ubuntu2                       all      >  
ii  alsa-topology-conf             1.2.2-1                            all      >  
ii  alsa-ucm-conf                  1.2.2-1ubuntu0.13                  all      >  
ii  apparmor                       2.13.3-7ubuntu5.1                  amd64    >  
ii  apport                         2.20.11-0ubuntu27.21               all      >  
ii  apport-symptoms                0.23                               all      >  
ii  apt                            2.0.6                              amd64    >  
ii  apt-utils                      2.0.6                              amd64    >  
ii  at                             3.1.23-1ubuntu1                    amd64    >  
ii  base-files                     11ubuntu5                          amd64    >  
ii  base-passwd                    3.5.47                             amd64    >  
ii  bash                           5.0-6ubuntu1.1                     amd64    >  
ii  bash-completion                1:2.10-1ubuntu1                    all      >  
ii  bc                             1.07.1-2build1                     amd64    >  
ii  bcache-tools                   1.0.8-3ubuntu0.1                   amd64    >  
ii  bind9-dnsutils                 1:9.16.1-0ubuntu2.10               amd64    >  
ii  bind9-host                     1:9.16.1-0ubuntu2.10               amd64    >  
ii  bind9-libs:amd64               1:9.16.1-0ubuntu2.10               amd64  
``` 

`dpkg --get-selections` komutu sayesinde ise sistemde kurulu veya kaldırılmış programları listeyebilirsiniz:
``` {.sh}
bulutbilisimciler@playground:~$ dpkg --get-selections 
>>> accountsservice  
adduser  
alsa-topology-conf    
alsa-ucm-conf  
apparmor   
apport  
apport-symptoms   
```  

`dpkg -s` komutu <'ProgramAdı'> argümanını alarak kurulan program hakkında bilgi verir:
``` {.sh}
bulutbilisimciler@playground:~$ dpkg -s apt
>>> Package: apt  
Status: install ok installed  
Priority: important  
Section: admin  
Installed-Size: 4209  
``` {.sh}

`dpkg -L` komutu <'ProgramAdı'> argümanını alarak kurulan programın paket içeriğini gösterir:
``` {.sh}
bulutbilisimciler@playground:~$ dpkg -L apt
>>> /.  
/etc  
/etc/apt  
/etc/apt/apt.conf.d  
```  


`apt-get install` komutu <'ProgramAdı'> argümanını alarak programı depodan (repository'den) yükler:
``` {.sh}
bulutbilisimciler@playground:~$ apt-get install npm
``` 

`apt-cache show` komutu <'ProgramAdı'> argümanını alarak yüklenecek program hakkında bilgi verir:
``` {.sh}
bulutbilisimciler@playground:~$ apt-cache show 
>>> Package: npm  
Architecture: all  
Version: 6.14.4+ds-1ubuntu2  
Priority: extra  
Section: universe/web  
```

`apt-get remove` komutu <'ProgramAdı'> argümanını alarak kurulu programı kaldırır:
``` {.sh}
bulutbilisimciler@playground:~$ apt-get remove npm
``` 

`apt-get purge` komutu <'ProgramAdı'> argümanını alarak programı tüm dosyalarıyla beraber kaldırır:
``` {.sh}
bulutbilisimciler@playground:~$ apt-get purge npm
``` 
