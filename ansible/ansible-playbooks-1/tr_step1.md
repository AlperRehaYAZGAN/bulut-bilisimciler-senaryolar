## Ansible Playbook Kullanımı
### Seviye: Başlangıç  

### Playbook Oluşturma

Playbook, görevlerin nasıl yürütüleceğini tanımlayan komut dosyası dizisidir. Komut dosyaları veya talimatlar YAML formatında yazılır.

playbook.yml dosyalarının çalıştırılması için ise ansible `ansible-playbook` komutu kullanılmaktadır.


Gelin egzersiz yaparak bu konuyu daha da pekiştirelim.

## LAB 1

Öncelikle hosts dosyamızın içerisine aşağıdaki şekilde node'ları ekleyelim.

````
mkdir /etc/ansible
````
````
vi /etc/ansible/hosts
````
````
[nodes] #Managed Nodes 
node2
node3
````

Önceki senaryomuzdan ansible hosts dosyamız içindeki node'lara erişim için SSH protokolünü kullandığını biliyoruz. Bu yüzden control node üzerinde ssh key oluşturup managed node’a göndermelisiniz. Aşağıdaki komut ssh key oluşturacaktır. Komutu çalıştırdığınızda karşınıza gelen adımlarda enter tuşuna basara ilerletiniz.

````
ssh-keygen -t rsa
````
Oluşturulan ssh key'i uzaktan bağlanacağımız node'lara aşağıdaki komut ile kopyalıyoruz. Burada node2 ve node3 için root şifresi "**root**" olarak girilmelidir.

````
ssh-copy-id -i /root/.ssh/id_rsa.pub root@node2
````
````
ssh-copy-id -i /root/.ssh/id_rsa.pub root@node3
````

İlk olarak kopyalayacağımız dosyayı oluşturalim.

````
touch /tmp/bulutbilisimciler.csv
````

Playbook dosyamızı oluşturacağımız dizini oluşturalım.
````
mkdir /root/playbook
`````
Şimdi bu dizin içerisinde playbook dosyamızı oluşturalim ve bir önceki bölümde yaptığımız kopyalama işlemini yapalım.

````
cd /root/playbook
````
````
touch copyfile.yml
````

Oluşturduğumuz copyfile.yml dosyasını vi editor ile açıp aşağıdaki şekilde düzenleyelim.

````
vi copyfile.yml
````
````
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
ansible-playbook copyfile.yml
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