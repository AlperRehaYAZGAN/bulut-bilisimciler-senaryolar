## Ansible Module Kullanımı
### Seviye: Başlangıç  

### Ad-Hoc Komutları ile Ansible Modül Kullanımı

Bu bölümde, Ansible Ad-hoc hoc komutlarını kullanarak dosya kopyalama işlemi yapacağız.

Ad-hoc komutları ansible’ı komut satırı olarak çalıştırmamızı sağlarlar. Basit görevleri hızlı bir şekilde gerçekleştirmek için çok kullanışlıdır. Tek seferde tek bir görevi yerine getirir.

Ad-hoc komutlarının yapısı şu şekildedir:

````
ansible [pattern] -m [module] -a "[module arguments]"
````  

![ad-hoc](https://miro.medium.com/max/963/0*oTqEMtp95UgYAFIi)

Pratik yaparak öğrendiklerimizi pekiştirelim.