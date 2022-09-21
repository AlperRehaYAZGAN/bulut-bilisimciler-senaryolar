#### 2)	String Methodları

•	String ifademizin kaç harften oluştuğunu yani uzunluğunu bulabilmek için `len(“python”)` yazarak bulabiliriz. 
```
6
```
çıktısını alırız.

•	String yerine rakam uzunluğu bulmak içinde str komutunu kullanırız. `len(str(3917384))` kodunun çıktısı ise 
```
7
```
olur. 

•	String ifademizin tüm harflerini otomati büyük yapmak istersek `“python”.upper()` kullanırız. 
```
‘PYTHON’
```
çıktısı gelir.

•	Tam tersi büyük harfleri küçük yapmak istersek `“PytHoN”.lower()` kullanırız. 
```
‘python’
```
olarak karşımıza gelir.

•	Yazdığımız kodda kaç tane istediğimiz karakteri bulmak için `count()` metodunu kullanabiliriz.
`(“burası bir playground ortamıdır!!!”).count(“a”)`
yazıp entera basın. Çıktıda gelen sayı sizin “a” harfinizin sayısıdır.
```
3
```


•	Aradığınız karakter kaçıncı indexte bulmak isterseniz  find() komutu ile
`(“burası bir playground ortamıdır!!!”).find(“p”)`
bu komudu çalıştırın ve çıktıya ulaşın.
```
11
```

•	Eğer yazdığınız komutta değişiklik yapmak istiyrsanız `replace()` metodu kullanılır. 
`(“python çok zevkli bir dildir.”).replace(“zevkli”, “eğlenceli”)`
kodunuz çıktısında zevkli kelimesinin, eğlenceli ile değiştiğini fark edersiniz.
```
'python çok eğlenceli bir dil'
```
Burada metodun ne anlama geldiğini ve işlevlerini öğrendik. Bu metodları ilerleyen bölümlerde daha detaylı örneklerle işleyeceğiz. 
