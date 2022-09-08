## Senaryo 2 - Değişiklik Saklama

**Git** init işlemi ile ilgili klasör altında git projesi başlatabilirsiniz. 
```
mkdir -p /data/git/first_project
```
```
cd /data/git/first_project
```

**Git** persistent hash - değişiklik kayıt altına alma işleminde proje olmaksızın deneme yaptığınız hata alacaksınız. 
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

**.git** dizini folder yapısını ilgili komut ile inceleyebilirsiniz. Detaylı açıklama için video içeriğine göz atabilirsiniz. 
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
**Branch** değişikliği için aşağıdaki şekilde ilerlenebilmektedir. 
```
git branch -m main
```
**Content** - içerik kontolü için git "cat-file" fonksiyonunu çalıştırabilirsiniz. HASH tipini ya da HASH içeriğini -p ile okuyabilirsiniz. 
```
git cat-file  c1c17c00601a11f5e1cc4625059e8053f8cea5579b -t 
```
```
git cat-file  c1c17c00601a11f5e1cc4625059e8053f8cea5579b -p
