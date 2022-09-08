## Senaryo 1 - Git Yükleme ve Hash Algoritması

**Git** açık kaynak bir versiyon kontrol ürünü olup, 2005 yılında Linus Torvalds tarafından ilk kullanıma sunulmuştur. Diğer versiyon kontrol ürünleri olan SVN ve CVS ile karşılaştırıldığında Git dağıtık bir yapıda çalışmaktadır. 

**Git** yükleme adımları işletim sisteminden işletim sistemine farklılık gösterebilir. LAB ortamımızda Alphine Linux için kurulum adımı aşağıdaki gibidir. Detaylı versiyon bazlı yükleme adımlarına kendi sitesinden ulaşabilirsiniz."https://git-scm.com/downloads"

```
apk add git
```

**Git** versiyon kontrolü için;
```
git  --version
```

**Git** ilgili değişiklikleri oluşturulan "HASH" ler ile kontrol edip saklamaktadır. HASH tek yönlü bir şifreleme sağlarken verinin HASH TEXT ile tekrar elde edilmesine imkan tanınmamaktadır. 
```
echo "Bulut Bilisimciler" |git hash-object --stdin
```

**Git** hash-object komutunda ilgili giriş değerinde basit bir değişiklikte dahi bir öncekinden farklı bir değer göreceksiniz. 
```
echo "Bulut Bilisimciler" |git hash-object --stdin
```
```
echo "Bulut Bilisimciler " |git hash-object --stdin
```
**HASH** dosya isminden bağımsız içerisindeki değere bağlı olarak değişir.
```
echo "BB" > /tmp/BB1
echo "BB" > /tmp/BB2
```
```
git hash-object /tmp/BB1
git hash-object /tmp/BB1
```