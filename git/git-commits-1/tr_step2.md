## Senaryo 2 - Versiyonlama

**Versiyonlama** yapısını anlamak için proje dizinimiz altında egitim.txt dosyamıza içerik ekliyoruz. Sonrasında "git add"  ile stage atıyor ve "git commit" ile değişikliği onaylıyoruz.  
```
echo "GO" >> egitim.txt
```
```
git status
```
```
git add egitim.txt
```
```
git  commit -m "egitime ekleme yapildi"
```
```
git log
```
**ikinci commit** için hash kontrolü yaptığımızda birinci commit ile ilgili bir **parent** kısmını görmemiz gerekiyor. Burada dikkat etmeniz gereken kısım sadece içeriği değişen alanlar için "blob", "tree" hash değişikliği olmaktadır. 
```
commit 016127b4207edfc02b19dedf2d27e032ff67e1b1 (HEAD -> master)
Author: Abdurrahim YILDIRIM <ayildirim@bulutbilisimciler.com>
Date:   Mon Aug 29 14:32:24 2022 +0000

    egitime ekleme yapildi

commit 8799b67dc64ef791852888111171242c4a0155f3
Author: Abdurrahim YILDIRIM <ayildirim@bulutbilisimciler.com>
Date:   Mon Aug 29 14:31:59 2022 +0000

    ilk commit

```
```
git cat-file -p  016127b4207edfc02b19dedf2d27e032ff67e1b1
```
**Count-objects** ile projenin altında "objects" dizininde toplamda kaç adet objenin olduğunu kontrol edebilirsiniz.
```
git count-objects
```