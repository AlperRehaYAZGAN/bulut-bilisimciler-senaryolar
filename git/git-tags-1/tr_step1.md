## Senaryo 1 - TAGs
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
git switch master
```
```
git tag release_1 -a -m "İlk versiyon"
```
```
cat .git/refs/tags/release_1
```
```
git cat-file -p  a62718f27bd816c1e6bb6c8988dd74b8126631ab
```
**Annotated** ve standart tag karşılaştırması için her iki tag türününde içeriğine bakabilirsiniz. 
```
git tag nonannotated
```

**Tag** ve **Branch** arasındaki fark için bir adet commit yapalım. 
```
cat .git/refs/heads/master
```
```
cat .git/refs/tags/nonannotated
```
```
touch icerik/test.txt
```
```
git add icerik/test.txt
```
```
git commit -m "Test.txt added"
```

**HASH** kontrolünde de göreceğiniz üzere TAG halen daha eski commit'i gösterirken Branch yeni kommiti göstermektedir.
```
cat .git/refs/heads/master
```
```
cat .git/refs/tags/nonannotated
```