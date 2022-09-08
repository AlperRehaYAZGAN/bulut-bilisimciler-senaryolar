## Senaryo 1 - İlk Proje

Bu senaryomuzda ***git*** deneyimleyeceğimiz ve basit bir proje oluşturacağız. 

Çalışacağımız projeye ait linux sistemde özel dizin oluşturuyoruz.
```
mkdir -p /data/git/bb
```

Örnek dosyaları ilgili dizin altında oluşturuyoruz. 
```
echo "Python" > /data/git/bb/egitim.txt
```
```
mkdir /data/git/bb/icerik
```
```
echo "Bulut Bilisimciler" >  /data/git/bb/icerik/README.txt
```
```
echo "Python" > /data/git/bb/icerik/python.txt
```

Dizin altına gidip bir git repository oluşturuyoruz. 
```
cd /data/git/bb
```
```
git init
```
```
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /data/git/bb/.git/
```
***Tree** komutunu ilgili dizin altında çalıştırdığınızda aşağıdaki şekilde size dosya yapısını gösterecektir.
```
tree .
```
```
.
├── egitim.txt
└── icerik
    ├── README.txt
    └── python.txt

1 directory, 3 files
```


```
git status
```
**Stage** alanına dosyaları atmak için **add** kullanıyoruz.
```
git add icerik/
```
```
git add egitim.txt
```

**Status** işlem sonrası durum kontrolü yaptığınızda az önce kırmızı olan iki dosyanın yeşile döndüğünü göreceksiniz. Bu stage alanına atıldılar demek.
```
git status
```

*Commit* ile işlemleri nihai olarak onaylıyoruz.
```
git commit -m "ilk commit"
```
**Hata** yukarıdaki komutu çalıştırdığınızda muhtemelen hata alacaksınız. Çünkü bu değişiklikleri kimin yaptığı bilinmiyor. Önce kendinizi tanıtmanız gerekecek. 
```
git config --global user.email "your-email@email.com"
```
```
git config --global user.name "Your Name"
```
```
git commit -m "ilk commit"
```
```
[master (root-commit) 7fb9709] ilk commit
 3 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 egitim.txt
 create mode 100644 icerik/README.txt
 create mode 100644 icerik/python.txt
```
**Stage** alanını kontrol ederseniz bekleyen bir commit olmadığını görebilirsiniz. 
```
git status
```