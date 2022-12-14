## Senaryo 2 - Değişiklik Saklama

**Git** proje init  ile ilk projemizi ilgili dizin altında oluşturuyoruz. Önce ilgili dizini tanımlamamız gerekecek.  
```
mkdir -p /data/git/first_project
```
```
cd /data/git/first_project
```

**Git** Git SHA1 algoritması kullanarak verileri adreslemek için HASH'ler object database içerisinde kayıt altına alır. 
```
echo "Bulut Bilisimciler" |git hash-object --stdin -w
```
**Git** Daha öncesinde hash-object ile oluşturduğumuz bir HASH'i kaydetmek istediğimizde git uygun projeyi ve dosya yapısını bulamadığından HASH adresleyemeyecektir.  Bunun için git init ile ilk projeyi oluşturmak gerekecektir. 
```
git init
```
```
echo "Bulut Bilisimciler" |git hash-object --stdin -w
```

**.git** dizini folder yapısı detaylıca kontrol edilerek Objeclerin hangi mantıkta adreslendiği kontrol edilebilir. 
```
ls -alrt /data/git/first_project/.git
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
```
**Branch**  değişikliği aşağıdaki komut ile yapılabilir. Bu konu diğer session'larda değerlendirilecektir. 
```
git branch -m main
```
**Content** içerik kontrolü ve adreslenen hash aşağıdaki komutlarla kontrol edilebilir. 
```
git cat-file  c1c17c00601a11f5e1cc4625059e8053f8cea5579b -t 
```
```
git cat-file  c1c17c00601a11f5e1cc4625059e8053f8cea5579b -p