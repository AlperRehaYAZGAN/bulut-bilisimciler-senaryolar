## Senaryo 1 - Branche

**Git Branch** yapısını bu senaryomuzda ele alacağız. 
Burada önceki lab senaryosunu oluşturmak için aşağıdaki içeriği kopyalayıp terminale yapıştırabilirsiniz. Benim önerimse bu senaryoyu kendiniz oluşturmayı deneyin. 
```
mkdir -p /data/git/bb
echo "Python" > /data/git/bb/egitim.txt
mkdir /data/git/bb/icerik
echo "Bulut Bilisimciler" >  /data/git/bb/icerik/README.txt
echo "Python" > /data/git/bb/icerik/python.txt
cd /data/git/bb
git init
git add icerik/
git add egitim.txt
git config --global user.email "ayildirim@bulutbilisimciler.com"
git config --global user.name "Abdurrahim YILDIRIM"
git commit -m "ilk commit"
echo "GO" >> egitim.txt
git add egitim.txt
git  commit -m "egitime ekleme yapildi"
```
**git log** ile daha önce yaptığımız commitleri görebilirsiniz. İki adet projede commit yaptık. 
```
git log
```
**git branch** ile hangi branch üzerinde çalıştığımıza bakabiliriz. 
```
git branch
```
```
git branch test 
```
```
git branch
```

**Git** Mevcuttaki çalışılan branch adını nasıl biliyor?
```
cat /data/git/bb/.git/HEAD
```
**Head** and **Branch** Nasıl değişir?
```
echo "Django" >> icerik/python.txt
```
```
git status
```
```
git add icerik/python.txt
```
**git log** ile commit HASH numarasını kontrol edin ve branch dosyasıyla son commit HASH aynı olduğunu gözlemleyin.
```
git commit  -m "Python.txt Güncellendi - Django"
```
```
git log
```
```
cat .git/refs/heads/master
```
```
git branch
```
**git switch** ve **git checkout** branch değişikliği yapma. Switch yeni versiyon git'lerde olan bir komut opsiyonudur. 
```
git switch test
```
**git switch** ile işlem yaptıktan sonra iki önemli aksiyon alınıyor. Birincisi HEAD dosyasının içeriği değiştiriliyor.İkincisi ilgili brach'in adreslediği commit için gerekli değişiklikler yapılıyor. icerik/python.txt dosyasının master ve test branchlerindeki durumunu kontrol edebilirsiniz. 
```
cat icerik/python.txt
```