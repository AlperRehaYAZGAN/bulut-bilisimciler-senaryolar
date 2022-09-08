## Senaryo 3 - Rebase 

Senaryo 2'de oluşturulan test ortamını yeniden oluşturmak için aşağıdaki komutları kullanabilirsiniz. Test branch için değişiklikler yaparak merge yapabilir ve sizlerde bir senaryo oluşturabilirsiniz. 
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
```
echo "Golang" > icerik/golang.txt
```
```
git status
```
```
git add icerik/golang.txt
```
```
git commit -m "Golang Added"
```
```
git rebase master
```
```
git switch master
```
**Git Log** ile test branch için master branch commitleri de görülebilir. 
```
git log
```