## Senaryo 1 - Merge

Aşağıdaki komutlar ile senaryo 6 çıktılarını bireberi aynı şekilde oluşturabilirsiniz. Terminalinize tamamını yapıştırıp "Enter" tuşuna basmanız yeterli. 
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
git branch test
echo "Django" >> icerik/python.txt
git add icerik/python.txt
git commit  -m "Python.txt Güncellendi - Django"
git switch test
```
**git branch** komutuyla mevcutta çalıştığımız branch'i görebiliriz. Yanında "*" bulunan branch aktif olan.
``` 
git branch
```
```
echo "Python.txt Güncellendi - Ansible Collection" >> icerik/python.txt
```
```
echo  "Python.txt Güncellendi - Django v2.1" >> icerik/python.txt
```
```
git add icerik/python.txt
```
```
git commit  -m "Python.txt Güncellendi - TEST Branch"
```
```
git switch master
```
**git merge** ile iki farklı brach birleştirilebilir. 
```
git merge test
```
```
git status
```
```
cat icerik/python.txt
```
**vi** ile dosyayı güncelleyip normal sürecimizi işletiyoruz. 
```
vi icerik/python.txt
```
```
git status
```
```
git add icerik/python.txt
```
```
git commit
```
```
git log
```
```
git cat-file -p 63fc6fcb9f5258de19b1e3fa48b902287db10c11
```