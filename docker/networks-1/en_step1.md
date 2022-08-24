###  Seviye: Başlangıç  

Bu bölümde Docker Network objeleri üzerinde duracağız. Docker kurulumu ile varsayılan olarak bridge, host ve none tipinde 3 adet network objesi gelir.

`docker network ls` komutu ile sistemdeki network objelerini listeleyebiliriz:


``` {.sh}
root@bulutbilisimciler:~# docker network ls
>> NETWORK ID     NAME      DRIVER    SCOPE
3b8ca1ac0fb8   bridge    bridge    local
52bfdde2bd4d   host      host      local
85139ddd0abd   none      null      local
``` 


`docker network inspect bridge` komutuyla bridge objesi ile ilgili detaylı bilgiye erişebiliriz:


``` {.sh}
root@bulutbilisimciler:~# docker network inspect bridge
>> [
    {
        "Name": "bridge",
        "Id": "3b8ca1ac0fb865462a4fff9e83b5cfb717772a46a42fe146f139b44a385b0cda",
        "Created": "2022-06-16T05:31:41.6366557Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "",
                    "Gateway": ""
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "3da5eb96ffa9449c06744323adf80b8cac159b860799dda2beae3496fd29b2e5": {
                "Name": "websunucu",
                "EndpointID": "",
                "MacAddress": "",
                "IPv4Address": "",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```


Biz eğer sıfırdan bir container yaratıp, herhangi bir network objesine bağlanmasını söylemezsek, bu container default olarak bridge network'üne bağlanır.

Öncelikle, `docker container run -d httpd` komutuyla detach modda bir container yaratıp çalıştıralım:

``` {.sh}
root@bulutbilisimciler:~# docker container run -d httpd
>> df710e1a58183bc5b8b254b64226505d1b36b4b777f3468329ac35436fbe5a93
```

Ardından `docker network inspect bridge` komutunu çalıştırırsak, çıktı olarak biraz önce yarattığımız container'ın bu bridge'e default olarak bağlandığını ve MAC adresi, IP adresi gibi bilgilerini görürüz:

``` {.sh}
root@bulutbilisimciler:~# docker network inspect bridge
>> ...
...
 "df710e1a58183bc5b8b254b64226505d1b36b4b777f3468329ac35436fbe5a93": {
                "Name": "silly_benz",
                "EndpointID": "",
                "MacAddress": "",
                "IPv4Address": "123.123.123.123",
                "IPv6Address": ""
            }
...
...

```


Bir container'a `docker exec -it containerID sh` komutu ile bağlanalım içeride `ifconfig` komutunu çalıştıralım.  Burada gördüğümüz IP adresi biraz önce bridge'i inspect'lediğimizde gördüğümüz IP ile aynıdır:

``` {.sh}
root@bulutbilisimciler:~# docker exec -it d4d3c3e347a8 sh
/usr/src/myapp # ifconfig
eth0      Link encap:Ethernet
          inet addr:123.123.123.123  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:726 (726.0 B)  TX bytes:0 (0.0 B)
```


Şimdi "host" objesine geçelim. Daha önce de dediğimiz gibi, host objesine bağlı container'ların hiç bir network izolasyonu yoktur ve çalıştıkları sistemin ağ altyapısını aynen kullanırlar.

`docker container run -it --name deneme1 --net host httpd sh` komutu ile, network'ü bridge değil de host olan bir container yaratıp bağlanalım. Burada da `ifconfig` komutunu çalıştırdığımızda container'ın IP adresinin host makine ile aynı olduğunu görebiliriz. Yani bu şekilde network izolasyonunu ortadan kaldırmış oluruz:

``` {.sh}
root@bulutbilisimciler:~# docker container run -it --name deneme1 --net host httpd sh
>> 
eth0      Link encap:Ethernet  
          inet addr:`HostMakineIP'si`  
          inet6 addr:  Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:43109 errors:0 dropped:0 overruns:0 frame:0
          TX packets:20136 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:63431514 (60.4 MiB)  TX bytes:1190278 (1.1 MiB)
```


Görmüş olduk ki, bridge network'ü sayesinde container, üzerinde çalıştığı host'un adaptörlerini direkt kullanmaz. Ayrı bir sanal ağda çalışır. Host network'ünde ise container, üzerinde çalıştığı sistemin ağ altyapısını direkt kullanır, arada herhangi bir izolasyon yoktur.


Şimdi "none" objesine bakalım. `docker container run -it --name deneme --net host httpd sh` komutu ile none network objesine sahip bir container yaratıp içine bağlanalım. Burada `ifconfig` komutunu çalıştırdığımızda sadece "Loopback" olduğunu görürüz. Yani başka herhangi bir network bağlantısı yoktur: 

``` {.sh}
root@bulutbilisimciler:~# docker container run -it --name deneme --net host httpd sh
>> 
lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:52 errors:0 dropped:0 overruns:0 frame:0
          TX packets:52 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:4392 (4.2 KiB)  TX bytes:4392 (4.2 KiB)
```



Böylelikle bu bölümün de sonuna gelmiş olduk. Bir başka bölümde görüşmek üzere!
