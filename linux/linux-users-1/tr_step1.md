###  Seviye: Başlangıç  

+ Kullanıcı Yönetimi

Linux sistemlerindeki en yetkili kullanıcı **root**’tur. Kullanıcı bilgileri **/etc/passwd** ; kullanıcı şifreleri ise **/etc/shadow** dosyasında yer alır. Bu dosyaları okumak, root yetkileri gerektirir.

Root şifresinin bilinmesi halinde, shell’de root yetkileri geçici olarak devralınabilir. Root yetkilerine sahip sudo grubunun üyesi olunabilir. Yetki yükseltme gerektiğinde `sudo` komutu kullanılabilir. Şimdi Linux sistemlerde kullanıcı yönetimini gerçekleştirirken en sık kullanılan komutlara göz atalım.

`chage -l` komutu <'KullanıcıAdı'> argümanı ile birlikte kullanılırsa kullanıcının bilgileri görüntülenir:
``` {.sh}
bulutbilisimciler@playground:~$ chage -l bulutbilisimciler 
>>> Last password change                                    : Feb 16, 2022  
Password expires                                        : never  
Password inactive                                       : never  
Account expires                                         : never  
Minimum number of days between password change          : 0  
Maximum number of days between password change          : 99999  
Number of days of warning before password expires       : 7  
```  


`adduser` komutu <'KullanıcıAdı'> argümanı ile birlikte kullanılırsa sisteme yeni kullanıcı eklenir. Oluşturulan kullanıcıya ait **home** dizini otomatik olarak **home/<'KullanıcıAdı'>** dizininde oluşturulur:
``` {.sh}
bulutbilisimciler@playground:~$ adduser kullanici1 
>>> Adding user kullanici1 ...  
Adding new group kullanici1 (1002) ...  
Adding new user kullanici1 (1001) with group kullanici1 ...  
Creating home directory home/kullanici1 ...  
Copying files from /etc/skel ...  
New password:  ****
```

`useradd` komutu ise kullanıcı oluşturmak için kullanılan bir diğer komuttur. Bu komutun kullanımı `useradd -m <'KullanıcıAdı'>` şeklindedir. Buradaki '-m' parametresi sayesinde oluşturulan kullanıcıya ait **home** dizininin otomatik olarak oluşturulması sağlanır:
``` {.sh}
bulutbilisimciler@playground:~$ useradd -m kullanici2 
```

Şimdi `cd` komutunu kullanarak **/home** dizinine gidelim ve `ls` komutuyla buradaki dosyaları görüntüleyelim. Biraz önce oluşturulan kullanıcıları görüntüleyelim:
``` {.sh}
bulutbilisimciler@playground:~$ cd /home
bulutbilisimciler@playground:/home$  

bulutbilisimciler@playground:/home$ ls 
> kullanici1 kullanici2
```


Yukarıdaki komutlar çalıştırıldığında kullanıcı şifresi otomatik olarak istenmektedir fakat bir kullanıcı şifresini güncellemek isterse `passwd <'KullanıcıAdı'>` komutunu kullanabilir:
``` {.sh}
bulutbilisimciler@playground:~$ passwd kullanici2
>>> New password:  ****  
Retype new password:  ****  
passwd: password updated successfully  
``` 

`deluser --remove-all-files` komutu  <'KullanıcıAdı'> argümanı ile birlikte kullanılırsa oluşturulan kullanıcı hesabı silinir:
``` {.sh}
bulutbilisimciler@playground:~$ deluser --remove-all-files kullanici1 
```

**NOT**: Kullanıcı silmek için bir diğer seçenek ise `userdel --remove-all-files` komutuyla beraber <'KullanıcıAdı'> argümanının kullanılmasıdır: '**--remove-all-files**' parametresi kullanılmazsa **home** dizini silinmez.  


`sudo` komutu <'Komut'> argümanı ile kullanılırsa, argüman olarak verilen komut sudo grubu aracılığıyla root kullanıcısının yetkileri ile çalıştırılır:
``` {.sh}
bulutbilisimciler@playground:~$ sudo apt-get update
``` 
