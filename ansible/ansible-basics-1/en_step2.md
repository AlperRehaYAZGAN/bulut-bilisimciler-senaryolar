#### Ansible Kurulumu  
Bu adımda, Bulut Bilişimciler interaktif platformumuzda öncelikle Ansible kurulumunu yapacağız.


`apk add ansible` komutu ile ansible-core kurulumunu gerçekleştirilir.

`apk add python3` ansible bazı modülleri çalıştırırken python'a ihtiyaç duymaktadır. Bu sebeple gelecek senaryolar için bu kurulumu da gerçekleştirelim. 

`ansible --version` komutu ile yüklenen ansible versiyonuna bakabiliriz. Böylece ilk ansible komutumuzu da çalıştırmış olduk.
  