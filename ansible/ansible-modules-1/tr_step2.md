## Ad-Hoc'lar

Bu adımda, Ad-hoc komutları ile dosya kopyalama işlemi yapacağız. Bu işlem için copy modulünü kullanacağız.

**"copy"** modülüne ait ihtiyacımız olan argümanlar ise şöyledir:

**src:** Uzak makineye (managed node) kopyalanacak dosyanın kaynak adresi.

**dest:** Dosyanın kopyalanacağı uzak makinedeki adres.

Hosts dosyamızın içerisine aşağıdaki şekilde node'ları ekleyelim.

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

Oluşturulan ssh key'i uzaktan bağlanacağımız node'lara aşağıdaki komut ile kopyalıyoruz.Burada node2 ve node3 için root şifresi "**root**" olarak girilmelidir.

````
ssh-copy-id -i /root/.ssh/id_rsa.pub root@node2
````
````
ssh-copy-id -i /root/.ssh/id_rsa.pub root@node3
````

Şimdi control node (node1) üzerinde bir txt dosyası oluşturalım.

````
touch /tmp/bulutbilisimciler.txt
````
Oluşturduğumuz bu dosyayı ansible aracılığıyla hosts dosyamızdaki sunuculara kopyalayacağız.

````
ansible nodes -m copy -a "src=/tmp/bulutbilisimciler.txt dest=/tmp/bulutbilisimciler.txt"
````
Bu işlemi tüm nodelara değil de bir nodeda yapmak için:

````
ansible $NodeIP -m copy -a "src=/tmp/bulutbilisimciler.txt dest=/tmp/bulutbilisimciler.txt"
````
Komut çıktısı aşağıdakine benzer şekilde olacaktır.
````
node2 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": true,
    "checksum": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
    "dest": "/tmp/bulutbilisimciler.txt",
    "gid": 0,
    "group": "root",
    "md5sum": "d41d8cd98f00b204e9800998ecf8427e",
    "mode": "0644",
    "owner": "root",
    "size": 0,
    "src": "/root/.ansible/tmp/ansible-tmp-1662195734.3813276-649-118241447650170/source",
    "state": "file",
    "uid": 0
}
````