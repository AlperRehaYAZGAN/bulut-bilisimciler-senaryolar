## Ad-Hoc'lar

Bu adımda, Ad-hoc komutları ile dosya kopyalama işlemi yapacağız. Bu işlem için copy modulünü kullanacağız.

**"copy"** modülüne ait ihtiyacımız olan argümanlar ise şöyledir:

**src:** Uzak makineye (managed node) kopyalanacak dosyanın kaynak adresi.

**dest:** Dosyanın kopyalanacağı uzak makinedeki adres.

Hosts dosyamızın içerisine aşağıdaki şekilde node'ları ekleyelim.

````
# vi /etc/ansible/hosts
````

````
[nodes] #Managed Nodes 
node2
node3
````
Şimdi terminal sunucumuz üzerinde bir txt dosyası oluşturalım.

````
# touch /tmp/bulutbilisimciler.txt
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
