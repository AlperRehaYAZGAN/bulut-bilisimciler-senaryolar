### Ansible Shell Module

Bu adımda uzak makinelerimize python kurulumu yapalım. Bu işlem için `shell` modülünü kullanabiliriz.

````
ansible all -m shell -a "apk add python3"
````

Aşağıdakine benzer bir şekilde çıktı almalısınız.

````
node2 | CHANGED | rc=0 >>
OK: 395 MiB in 157 packages
[WARNING]: Platform linux on host node3 is using the discovered Python
interpreter at /usr/bin/python3.10, but future installation of another Python
interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-
core/2.13/reference_appendices/interpreter_discovery.html for more information.
````
Tebrikler ! 
Bu bölümü başarıyla tamamladınız.