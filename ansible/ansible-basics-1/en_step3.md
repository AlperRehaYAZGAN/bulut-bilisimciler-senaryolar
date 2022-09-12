### Ansible Inventory'leri  

Bu adımda, managed node'lar ile bağlantı kurarak basit bir şekilde inventory dosyasını nasıl düzenleyeceğimizi göreceğiz.

Ansible SSH protokolünu kullanarak haberleşir. Managed Node’a bağlanmak istiyorsanız control node üzerinde ssh key oluşturup managed node’a göndermelisiniz. Aşağıdaki komut ssh key oluşturacaktır. Komutu çalıştırdığınızda karşınıza gelen adımlarda `enter` tuşuna basara ilerletiniz.

```
ssh-keygen -t rsa
````
Oluşturulan ssh key'i uzaktan bağlanacağımız node'a aşağıdaki komut ile kopyalıyoruz.Burada root şifresi "**root**" olarak girilmelidir.

````
ssh-copy-id -i /root/.ssh/id_rsa.pub root@node2
`````
Inventory dosyası için varsayılan konum  "**/etc/ansible/hosts**" dosyasıdır.

Hosts dosyası içerisinde eklediğimiz bilgiler bizim managed node'larımızı temsil eder. Control node üzerinden bu bu management nodelara erişip uzaktan yönetimini sağlayabiliriz.

Öncelikle "**/etc**" dizinine gidilir 
`ls` komutu ile ansible dizini oluşmuş mu kontrol edilir.
Dizin yok ise aşağıdaki komutu ile ansible dizini oluşturulur.

````
mkdir /etc/ansible
````
`vi /etc/ansible/hosts` komutu ile inventory dosyası oluşturularak editor aracılığıyla düzenlenir.

Basit bir şekilde inventory dosyası oluşturmak için hosts dosyasının içerisine aşağıdaki gibi uzaktan bağlantı sağlanacak node hostname'ini yazıp kaydedelim. 

```
node2
```

***Hatırlatma:**  vi editorde düzenleme yapabilme için klavyede `i` 'ye basılmalıdır. Düzenleme sonrası vi editoru kaydetmek için `esc+ wq!` yazılmalıdır.*

Şimdi terminalimizde aşağıdaki ansible komutunu çalıştıralım. Bu komut ile hosts dosyamız içerisindeki nodelara ping atılacaktır. Ping başarılı olması durumunda çıktı SUCCESS olarak dönecektir.

````
ansible all -m ping
````

Komutun çıktışı aşağıdakine benzer bir şekilde olmalıdır.

````
node2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": false,
    "ping": "pong"
}
````

Tebrikler, bu bölümdeki adımları başarıyla tamamladınız. 2.bölüm ile devam edebilirsiniz.  