## Senaryo 4 - Commit analizi

**git status**  ile mevcutta stage alanında commitlenmeyi bekleyen değişiklik var mı diye kontrol ediyorduk. **Commit** durumlarını gözlemlemek içinse **git log** komutunu kullanabiliriz. 
```
git log
```
```
commit 7fb970912331c6815c9ad9c5e84ad8ea0610ca58 (HEAD -> master)
Author: Abdurrahim YILDIRIM <ayildirim@bulutbilisimciler.com>
Date:   Mon Aug 29 13:41:27 2022 +0000

    ilk commit
```
**cat-file** ile önceki commentin detaylarına bakabiliriz. 
``` 
git cat-file -p 7fb970912331c6815c9ad9c5e84ad8ea0610ca58
```
**HASH TREE** yukarıdaki komutun çıktısından daha önce görmediğimiz bir terime gideceğiz.**TREE**
```
tree a8254664752d3433fdeeec39b174ca03990bf3c9
author Abdurrahim YILDIRIM <ayildirim@bulutbilisimciler.com> 1661780487 +0000
committer Abdurrahim YILDIRIM <ayildirim@bulutbilisimciler.com> 1661780487 +0000

ilk commit
```
```
git cat-file -p  a8a8254664752d3433fdeeec39b174ca03990bf3c9
```
Aşağıdaki komutun çıktısından da anlaşışacağı üzere "tree" bir dizini göstermektedir. 
```
100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391    egitim.txt
040000 tree 5cd99b501a2366172abef828e8d61618b316df87    icerik
```