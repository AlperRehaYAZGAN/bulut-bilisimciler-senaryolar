###  Seviye: Başlangıç

+ Sistem Yönetimi ve Süreç İzleme

Süreç(process) denilen kavram genel olarak; bir program çalıştığında programın belleğe yüklenme işlemine denir. Bu senaryoda süreçler hakkında bilgi almak, işlem yapmak ve gerektiğinde müdahalede bulunmak gibi işlemleri yapabilmek adına ilgili komutlara göz atacağız.

Bu noktada **Systemd**'nin ne olduğundan kısaca bahsedip, sık kullanılan komutlarla devam edeceğiz. **Systemd**, Linux kerneli için sistem ve servis yöneticiliği görevini gerçekleştiren bir servis yöneticisidir. Amacı sistemdeki servislerin çalışmasını organize etmektir. Bu organizasyonu ise `systemctl`, `journalctl`, `notify`, `analyze`,  `loginctl` ve  `nspawn` gibi komutlar sayesinde gerçekleştirir.

`systemctl list-units --type=service` komutu sayesinde sistemde çalışan servisleri görüntülenir:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl list-units --type=service
>>>  accounts-daemon.service              loaded active running Accounts Service    
  apport.service                       loaded active exited  LSB: automatic  
  atd.service                          loaded active running Deferred execution  
  blk-availability.service             loaded active exited  Availability  
  console-getty.service                loaded active running Console Getty  
```

`systemctl stop <'ServisAdı'>` komutu belirtilen bir servisin durdurulmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl stop NetworkManager
``` 

Yukarıdaki komuttan tahmin edebileceğiniz üzere `systemctl start <'ServisAdı'>` komutu ise belirtilen bir servisin başlatılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl start NetworkManager 
```

`systemctl restart <'ServisAdı'>` komutu belirtilen bir servisin tekrar başlatılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl restart NetworkManager
```


Bir servis hakkında detaylı durum bilgisini listelemek istenirse `systemctl status <'ServisAdı'>` komutu kullanılabilir:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl status ssh 
>>>  ssh.service - OpenBSD Secure Shell server  
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset  
     Active: active (running) since Tue 2022-04-12 01:12:11 +03; 5min ago  
       Docs: man:sshd(8)  
             man:sshd_config(5)  
   Main PID: 273 (sshd)  
      Tasks: 1 (limit: 7490)  
     Memory: 3.5M  
     CGroup: /system.slice/ssh.service  
             └─273 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups  

```

`systemctl disable <'ServisAdı'>` komutu belirtilen bir servisin devre dışı bırakılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl disable ssh
```

Yine yukarıdaki komuttan tahmin edebileceğiniz üzere `systemctl enable <'ServisAdı'>` komutu ise belirtilen bir servisin devreye alınmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl enable ssh 
``` 

`systemctl --version` komutu sistemin versiyon bilgilerini görüntülemeyi sağlarken ; `systemctl is-enabled <'ServisAdı'>` komutu belirtilen servisin sistemde aktif olup olmadığının bilgisini verir:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl --version
>>> systemd 245 (245.4-4ubuntu3.15)   
+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP   +BLKID +ELFUTILS +KMOD +IDN2 -IDN +PCRE2 default-hierarchy=hybrid  
  
bulutbilisimciler@playground:~$ systemctl is-enabled ssh 
>>> enabled
``` 

Systemd komutları kapsamında değineceğimiz son komut olan `systemctl list-dependencies <'ServisAdı'>` komutu ise belirtilen servisin bağımlılıklarını görüntülemeyi sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ systemctl list-dependencies ssh
>>> ssh.service  
● ├─-.mount  
● ├─system.slice  
● └─sysinit.target  
●   ├─apparmor.service  
●   ├─blk-availability.service  
●   ├─dev-hugepages.mount  
●   ├─dev-mqueue.mount  
●   ├─finalrd.service  
●   ├─keyboard-setup.service  
●   ├─kmod-static-nodes.service  
●   ├─lvm2-lvmpolld.socket  
●   ├─lvm2-monitor.service  
●   ├─multipathd.service  
●   ├─open-iscsi.service  
●   ├─plymouth-read-write.service  
●   ├─plymouth-start.service  
●   ├─proc-sys-fs-binfmt_misc.automount  
●   ├─setvtrgb.service  
●   ├─sys-fs-fuse-connections.mount  
●   ├─sys-kernel-config.mount  
●   ├─sys-kernel-debug.mount  
●   ├─sys-kernel-tracing.mount  
●   ├─systemd-ask-password-console.path  
``` 

Şimdi süreç yönetimi gerçekleştirilirken sıklıkla kullanılan diğer komutlara göz atalım.

`ps aux` komutu sistemdeki tüm süreçleri gösterir:
``` {.sh}
bulutbilisimciler@playground:~$ ps aux 
>>>
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND  
root           1  0.1  0.2 175052 13612 ?        Ss   01:12   0:01 /lib/systemd/  
root          44  0.0  0.2  51456 15452 ?        S<s  01:12   0:00 /lib/systemd/  
root          64  0.0  0.1  21612  7088 ?        Ss   01:12   0:00 /lib/systemd/  
```

`ps -e` komutu sadece sistem süreçlerini gösterir:
``` {.sh}
bulutbilisimciler@playground:~$ ps -e 
>>> PID TTY          TIME CMD  
      1 ?        00:00:01 systemd  
     44 ?        00:00:00 systemd-journal  
     64 ?        00:00:00 systemd-udevd  
     69 ?        00:00:00 systemd-network  
```

`ps -u` komutu <'KullanıcıAdı'> argümanı ile beraber kullanılırsa kullanıcıya ait süreçler gösterilir:
``` {.sh}
bulutbilisimciler@playground:~$ ps -u bulutbilisimciler 
>>> PID TTY          TIME CMD  
   1481 ?        00:00:00 systemd  
   1482 ?        00:00:00 (sd-pam)  
   1487 pts/0    00:00:00 bash  
   1566 pts/0    00:00:00 ps  
``` 


İlk senaryoda **grep** komutuna göz atmıştık. `ps aux | grep <'SüreçAdı'>` komutu sayesinde belirtilen işleme ait süreçler gösterilir:
``` {.sh}
bulutbilisimciler@playground:~$ ps aux | grep systemd 
>>> root           1  0.1  0.2 175052 13612 ?        Ss   01:12   0:01 /lib/systemd   
systemd --system-unit=basic.target  
root          44  0.0  0.2  51456 15452 ?        S<s  01:12   0:00 /lib/systemd  
``` 

`top` komutu süreçleri üç saniyede bir listeler:
``` {.sh}
bulutbilisimciler@playground:~$ top 
>>> PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND  
      1 root      20   0  175052  13612   8808 S   0.0   0.2   0:01.24 systemd   
     44 root      19  -1   51456  15452  14440 S   0.0   0.2   0:00.11 systemd-journal  
     64 root      20   0   21612   7088   3784 S   0.0   0.1   0:00.10 systemd-udevd  
     69 systemd+  20   0   18380   7516   6632 S   0.0   0.1   0:00.04 systemd-network  
    212 systemd+  20   0   23928  12160   8052 S   0.0   0.2   0:00.05 systemd-resolve  
```


`top -d <'Sayı'>` komutu süreçleri belirtilen sayı kadar saniyede bir listeler:
``` {.sh}
bulutbilisimciler@playground:~$ top -d 5
>>> PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND  
      1 root      20   0  175052  13612   8808 S   0.0   0.2   0:01.24 systemd   
     44 root      19  -1   51456  15452  14440 S   0.0   0.2   0:00.11 systemd-journal  
     64 root      20   0   21612   7088   3784 S   0.0   0.1   0:00.10 systemd-udevd  
     69 systemd+  20   0   18380   7516   6632 S   0.0   0.1   0:00.04 systemd-network  
    212 systemd+  20   0   23928  12160   8052 S   0.0   0.2   0:00.05 systemd-resolve 
``` 

`pstree -p` komutu süreçleri bağımlılıkları (dependencies) ve PID (Process ID)'leri ile gösterir:
``` {.sh}
bulutbilisimciler@playground:~$ pstree -p
>>> systemd(1)─┬─accounts-daemon(215)─┬─{accounts-daemon}(222)    
           │                      └─{accounts-daemon}(245)    
           ├─agetty(261)  
           ├─agetty(268)  
           ├─atd(243)  
           ├─cron(239)  
           ├─dbus-daemon(216)  
           ├─networkd-dispat(219)  
           ├─polkitd(269)─┬─{polkitd}(270)  
           │              └─{polkitd}(272)  
           ├─rsyslogd(220)─┬─{rsyslogd}(228)  
           │               ├─{rsyslogd}(229)  
           │               └─{rsyslogd}(230)  
           ├─snapd(681)─┬─{snapd}(682)  
           │            ├─{snapd}(683)  
           │            ├─{snapd}(684)  
           │            ├─{snapd}(685)  
           │            ├─{snapd}(686)  
           │            ├─{snapd}(687)  
           │            ├─{snapd}(688)  
           │            ├─{snapd}(690)  
           │            ├─{snapd}(691)  
           │            ├─{snapd}(692)  
           │            ├─{snapd}(693)  
           │            ├─{snapd}(697)  
           │            ├─{snapd}(698)  
           │            ├─{snapd}(717)  
           │            ├─{snapd}(718)  
           │            ├─{snapd}(719)  
           │            ├─{snapd}(720)  
           │            ├─{snapd}(982)  
           │            ├─{snapd}(1034)  
           │            └─{snapd}(1035)  
           ├─snapfuse(573)  
           ├─snapfuse(847)  
           ├─snapfuse(981)  
           ├─sshd(273)  
           ├─systemd(1481)───(sd-pam)(1482)  
           ├─systemd-journal(44)  
           ├─systemd-logind(224)  
           ├─systemd-network(69)  
           ├─systemd-resolve(212)  
           ├─systemd-udevd(64)  
           └─unattended-upgr(255)───{unattended-upgr}(277)  

```


`pgrep <'SüreçAdı'>` komutu belirtilen sürece ait PID (Process ID)'leri görüntüler:
``` {.sh}
>bulutbilisimciler@playground:~$ pgrep systemd
>>> 1  
44  
64  
69   
212  
224  
1481  
```


`kill <'ProcessID'>`komutu belirtilen PID (Process ID)'ye ait sürecin sonlandırılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ kill 1590 
``` 

`kill -9 <'ProcessID'>`komutu belirtilen PID (Process ID)'ye ait sürecin **zorla** sonlandırılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ kill -9 1590
```


`killall <'SüreçAdı'>`komutu belirtilen sürece bağlı tüm süreçlerin sonlandırılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ killall ssh 
``` 

`killall -9 <'SüreçAdı'>`komutu belirtilen sürece bağlı tüm süreçlerin **zorla** sonlandırılmasını sağlar:
``` {.sh}
bulutbilisimciler@playground:~$ killall -9 ssh*
``` 

`xkill` komutu Kullanıcı Grafik Arayüzü'ne (GUI) yanıt vermeyen uygulamayı sonlandırmaya zorlar:
``` {.sh}
bulutbilisimciler@playground:~$ xkill 
>>> Select the window whose client you wish to kill with button 1...
```

