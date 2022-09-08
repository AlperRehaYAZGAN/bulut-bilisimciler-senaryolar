# Ansible ile Otomasyona Giriş 
### Seviye: Başlangıç  

### Bu örnek ortamımızda interaktif örnekler ile Ansible'ın temel yapısını inceleyeceğiz.

#### Ansible Temel Kavramlar

Ansible, manuel olarak yaptığınız işleri otomatize etmenizi sağlayan bir otomasyon tool’udur. Birçok modülü sayesinde network cihazlarınızdan bulut ortamlarına kadar kullandığınız sunuculara geniş kapsamlı otomasyon hizmeti sunmanızı sağlar.

Ansible’ın temel yapısını incelemek istersek;

**Control Node:** Ansible’ın kurulu olduğu makinedir. Bu makine üzerinden ansible komutlarını, playbook’larını çalıştırabiliriz.

**Managed Nodes:** Ansible tarafından yönetilen makinelerdir. Örneğin bir playbook’un uygulanmasını istediğimiz hostumuz bu yapıdaki managed node olacaktır.

![Mimari](https://miro.medium.com/max/963/0*9tjXPw5vgixFz6I3)

Ayrıca Ansible ile çalışmaya başladığımızda aşağıdaki terimleri de sıklıkla duyacağız.

**Modules:** Ansible’ın farklı görevler için oluşturulmuş kod kümeleridir. Ansible’ın zengin bir modül kütüphanesi bulunmaktadır.

**Inventory:** Ansible komutlarının uygulandığı hostların tamamını kapsayan envanter diyebiliriz.
Kullanım amacınıza göre farklı farklı bir çok envanter ya da tüm hostlarınız için tek bir envanter oluşturabilirsiniz. 

Inventory oluşturduktan sonra içerisine girip “hosts” kısmına playbook'un çalışırken bağlanacağı değişkeni ekleyebilirsiniz. Bu değişken bir sunucu olabileceği gibi bir network cihazı da olabilir. Bu gibi farklılıklarda inventory dosyanızı ayırmak yönetim açısından sizi rahatlatacaktır.

**Playbooks:** Otomasyon ile yapılacak görevlerin toplandığı dosyadır. YAML formatındadır. Mesela envanterdeki tüm sunuculara remote bağlantı sağlayıp backup scriptini başlat şekilinde bir playbook’umuz olabilir. Ad-hoc komutlarını YAML formatına dönüştürerek kolaylıkla playbook oluşturabiliriz.

![playbook)](https://miro.medium.com/max/963/0*BxInjuE_acj1N6fe)

***NOT:*** Ansible ad-hoc komutları, tek bir görevi (task) yerine getirmek içi komut satırını kullanarak ansible'ı çalıştırma şeklimizdir. Hızlı ve kolay bir şekilde uygulanabilirler fakat tekrar tekrar kullanılmaları pratikte pek mümkün değildir. 

Gelin şimdi biraz pratik yaparak öğrendiklerimizi pekiştirelim.  

























# SENARYO 3 - Playbook Oluşturma

Playbook, görevlerin nasıl yürütüleceğini tanımlayan komut dosyası dizisidir. Komut dosyaları veya talimatlar YAML formatında yazılır.

playbook.yml dosyalarının çalıştırılması için ise ansible `ansible-playbook` komutu kullanılmaktadır.


Gelin egzersiz yaparak bu konuyu daha da pekiştirelim.

## LAB 1

Öncelikle playbook dosyamızı oluşturacağımız dizini oluşturalım.

````
# mkdir /root/playbook
`````
Şimdi bu dizin içerisinde playbook dosyamızı oluşturalim ve bir önceki bölümde yaptığımız kopyalama işlemini yapalım.

````
# cd /root/playbook
# touch copyfile.yml
````
Şimdi de kopyalayacağımız dosyayı oluşturalim.

````
# touch /tmp/bulutbilisimciler.csv
````
Oluşturduğumuz copyfile.yml dosyasını vi editor ile açıp aşağıdaki şekilde düzenleyelim.

````
# vi copyfile.yml

--- 
- name: copy a file 
  hosts: nodes

  tasks: 
  - copy: 
      src: /tmp/bulutbilisimciler.csv
      dest: /tmp/bulutbilisimciler.csv

````
Artık dosya kopyalama işlemi için playbook dosyamızı oluşturduk. Aşağıdaki komut ile bu dosyayı çalıştırabiliriz.

````
# ansible-playbook copyfile.yml
````
Komutun çıktısı aşağıdakine benzer şekilde olmalıdır. 

Burada playbook başarılı çalıştırıldığında CHANGED, hata alındıysa FAILED, değişiklik olmadıysa SKIPPED şekilde dönüş yapacaktır.


````
PLAY [copy a file] *************************************************************

TASK [Gathering Facts] *********************************************************
[WARNING]: Platform linux on host node3 is using the discovered Python
interpreter at /usr/bin/python3.10, but future installation of another Python
interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-
core/2.13/reference_appendices/interpreter_discovery.html for more information.
ok: [node3]
[WARNING]: Platform linux on host node2 is using the discovered Python
interpreter at /usr/bin/python3.10, but future installation of another Python
interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-
core/2.13/reference_appendices/interpreter_discovery.html for more information.
ok: [node2]

TASK [copy] ********************************************************************
changed: [node2]
changed: [node3]

PLAY RECAP *********************************************************************
node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
````
Tebrikler ! 
Bu bölümü başarıyla tamamladınız.