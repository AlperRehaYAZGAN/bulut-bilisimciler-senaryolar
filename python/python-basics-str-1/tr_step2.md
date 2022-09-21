### Temel Komutlar
Öncelikle terminalimizde `python3` yazılarak Python çalıştırılır. 
```
Python 3.10.5 (main, Jul 25 2022, 15:52:08) [GCC 11.2.1 20220219] on linux
Type "help", "copyright", "credits" or "license" for more information.
```
Yukarıdaki ibare geldiyse eğer tebrikler. Python ortamına giriş yaptınız. Fark ettiyseniz komut istemi `>>>` olarak değişti. Bu demek oluyor ki burada sadece python dilini kullanabiliriz. Başka dil kullanmayı denersek `SyntaxError: invalid syntax` hatası verir. Hata vermemesi için `exit()` ya da `ctrl+Z` / `ctrl+D` yaparak çıkış yapabiliriz. 

Şimdi Python’ı öğrenmeye başlayalım:

#### 1)	String İfadeler
-	Python’da string(metin) ifade kullanacağımız zaman ya çift tırnak parantez  " " ya da tek tırnak parantez '' arasında kodumuzu yazarız. Ancak bu şekilde çıktımızı sağlam alabiliriz.

-	`"Merhaba Dünya"` ya da `'Merhaba Dünya'` yazdığımızda aynı sonuç olan 
```
'Merhaba Dünya'
``` 
çıktısını alırız. String ifadelerin çıktıları ‘ ’ arasında gelir.

-	`"Bulut" + "Bilişimciler"` yazdığımızda ise birleşik
```
‘BulutBilişimciler’
```
çıktısı alırız.`"Bulut"+ " " + "Bilişimciler"`ın çıktısı ise araya boşluk koyduğumuzdan ötürü 
```
‘Bulut Bilişimciler’
```
olur.

-`"Python"*3` kodumuzun çıktısı ‘PythonPythonPython’ olarak görülür. String ifademizi çoğaltmak istediğimizde kullanabiliriz.

-	'' tek tırnak parantezi kullanacağımız zaman string cümle içerisinde kesme kullanacaksak eğer \’ yaparak kullanmalıyız. Çünkü backslash \ kullanmadığımız zaman string parantezi zannedip syntax error verir.  `'Python\'ı geliştiren kişi Guido Van Rossum\'dur'` yazdığımızda temiz bir çıktı alırız. Aynı şekilde bu kodu `"Python'ı geliştiren kişi Guido Van Rossum'dur"` böyle yazdığımızda da çıktısı gelir.

