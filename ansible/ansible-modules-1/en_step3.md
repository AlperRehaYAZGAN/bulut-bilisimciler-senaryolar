### Ansible Shell Module

Bu adımda uzak makinelerimize nano editörünü ansible ile kuracağız. Bu işlem için `shell` modülünü kullanabiliriz.

````
ansible all -m shell -a "apk add nano"
````

Aşağıdakine benzer bir şekilde çıktı almalısınız.

````
node2 | CHANGED | rc=0 >>
fetch https://dl-cdn.alpinelinux.org/alpine/v3.16/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.16/community/x86_64/APKINDEX.tar.gz
(1/1) Installing nano (6.3-r0)
Executing busybox-1.35.0-r17.trigger
OK: 395 MiB in 157 packages
````
Tebrikler ! 
Bu bölümü başarıyla tamamladınız.