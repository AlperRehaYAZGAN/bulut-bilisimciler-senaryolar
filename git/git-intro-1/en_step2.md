## Senaryo 2 - Değişiklik Saklama

**Git** proje init   
```
mkdir -p /data/git/first_project
```
```
cd /data/git/first_project
```

**Git** persistent hash - değişiklik kayıt altına alma
```
echo "Bulut Bilisimciler" |git hash-object --stdin -w
```
**Git** init yapıp projeyi oluşturmak gerekecektir. Yoksa yukarıdaki komut çalışmayacaktır.
```
git init
```
```
echo "Bulut Bilisimciler" |git hash-object --stdin -w
```

**.git** dizini folder yapısı için
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
**Branch** Change
```
git branch -m main
```
**Content** ve içerik kontolü
```
git cat-file  c1c17c00601a11f5e1cc4625059e8053f8cea5579b -t 
```
```
git cat-file  c1c17c00601a11f5e1cc4625059e8053f8cea5579b -p