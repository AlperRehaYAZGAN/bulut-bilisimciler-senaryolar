####  Seviye: Başlangıç

Bu bölümde değişkenleri ele alacağız. Vakit kaybetmeden başlayalım.

Kısaca değişkenler, girdiğimiz değerleri alan veya programın çalışmasıyla bazı değerlerin atandığı veri tutucularıdır. Bir değişkene değer atayarak o değeri tekrar tekrar tanımlamak yerine tek bir değişken üzerinden istediğimiz zaman çağırabiliriz. Değişken tanımlarken öncelikle değişken adını girerek eşittir işaretini koyduktan sonra değişkene atamak istediğimiz değeri tırnak işareti içerisine yazıyoruz. 

Örneğin `sistem="linux"` komutunu çalıştırırsak, "sistem" isimli değişkene "linux" değerini atamış oluruz:

``` {.sh}
root@bulutbilisimakademi:~# sistem="linux"
```

Değişkenin tanımlanıp tanımlanmadığını konsol üzerinden çağırarak kontrol edelim. Tanımladığınız herhangi bir değişkeni çağırırken echo $degisken şeklinde komut girmeniz yeterlidir:

``` {.sh}
root@bulutbilisimakademi:~# echo $sistem
>>linux
```

Tanımladığımız değişken "sistem" ismine sahip olduğu için konsolda `echo $sistem` komutu çalıştırıldığında, gördüğünüz gibi "linux" ifadesi basılmış oldu.

Bir örnek daha yapalım ve bu sefer değişkene, değer olarak sayı atayalım. Bunun için `rakamlar="12345"` ifadesini konsola girelim ve `echo $rakamlar` komutu ile atadığım değişkene ulaşalım:

``` {.sh}
root@bulutbilisimakademi:~# rakamlar="12345"
root@bulutbilisimakademi:~# echo $rakamlar
>>12345
```

Değişken tanımlamanın ne kadar basit olduğunu görmüş olduk. Şimdi değişken tanımlarken dikkat edilmesi gerekenlere değinelim:

+ Değişken isimleri tanımlarken **Türkçe karakter kullanmadan** alfanümerik(A-Z, a-z) karakter kullanmamız gerekiyor. Örneğin konsola içerisinde Türkçe karakter geçen, çalı="bitki" gibi bir değişken tanımlamak istersek, konsol çıktı olarak "komut yok" hatasını basacaktır:

``` {.sh}
root@bulutbilisimakademi:~# çalı="bitki"
>>bash: çalı=bitki: command not found
```

Bu kullanımın doğrusu Türkçe karakter içermeyen cali="bitki" şeklinde olmalıydı:

``` {.sh}
root@bulutbilisimakademi:~# cali="bitki"
root@bulutbilisimakademi:~# echo $cali
>>bitki
```

+ Türkçe karakter dışında, değişken ismi tanımlarken "_(alt tire)" işareti haricinde herhangi bir sembol kullanımı da hataya yol açmaktadır.

Örneğin yeni-yeni="yeni değer" gibi bir değişken tanımlamak istersek, konsol çıktı olarak "komut yok" hatasını basacaktır:

``` {.sh}
root@bulutbilisimakademi:~# yeni-yeni="yeni değer"
>>yeni-yeni=yeni değer: command not found
```

Gördüğünüz gibi değişken tanımlanamadı.Tekrar belirtmiş olalım, hatalı bir kullanıma yol açmamak adına değişken tanımlarken alt tire işareti haricinde hiç bir sembol kullanmayın. Yani "yeni+yeni", "yeni#yeni", "yeni@yeni" vb. tüm kullanımlar hatalıdır.

Şimdi aynı örneği "_(alt tire)" işareti ile deneyelim ve bu durumu teyit edelim. Bunun için konsola `yeni_yeni="yeni değer"` ifadesini yazalım ve tanımladığımız değişkeni `echo $yeni_yeni` komutunu girerek sorgulayalım:

``` {.sh}
root@bulutbilisimakademi:~# yeni_yeni="yeni değer"
root@bulutbilisimakademi:~# echo $yeni_yeni
>>yeni değer
```

+ Dikkat etmemiz gereken bir diğer husus ise tanımlanacak değişken isimlerinin kesinlikle rakam ile başlamamasıdır. Fakat başlangıcı hariç, değişken isimlerinde rakam kullanılabilir.

Örneğin herhangi bir değişken tanımlarken "1kitap" hatalı bir kullanım iken "kitap1" ya da "kit1ap" doğru kullanıma örnektir.

``` {.sh}
root@bulutbilisimakademi:~# 1kitap="yanlış"
>>bash: 1kitap=yanlış: command not found
root@bulutbilisimakademi:~# kitap1="doğru"
root@bulutbilisimakademi:~# echo $kitap1
>>doğru
```


+ Bir başka dikkat edilmesi gereken ayrıntı da; değişken tanımlarken kullanılan tanımların, Linux sistemlerinde olduğu gibi büyük küçük harf duyarlılığına sahip olduğudur.

Örneğin tamamı büyük harflerden oluşan TEST="ilk ifade" şeklindeki bir tanım ile tamamı küçük harflerden oluşan test="ikinci ifade" tanımı, bash diline göre iki farklı değişkeni temsil eder. `echo` komutu yardımıyla bu durumu teyit edelim:

``` {.sh}
root@bulutbilisimakademi:~# TEST="birinci ifade"
root@bulutbilisimakademi:~# test="ikinci ifade"

root@bulutbilisimakademi:~# echo $TEST
>>birinci ifade

root@bulutbilisimakademi:~# echo $test
>>ikinci ifade
```

Gördüğünüz gibi aynı isime sahip olan biri küçük diğeri büyük harflerden oluşan iki değişken, sistem tarafından iki farklı değişken olarak algılanarak konsola ayrı ayrı çıktılar basmış oldu.


+ Bunun haricinde değişken tanımlarken eşittir(=) işaretinin sağında ve solunda boşluk olmamasına dikkat etmemiz gerekiyor. Aksi takdirde sistem bizlerin değişken tanımlamak istediğini anlayamadığından, kaçınılmaz olarak konsola "komut yok" şeklinde hata çıktısı basacaktır:

``` {.sh}
root@bulutbilisimakademi:~# ifade1 = "yanlış"
>>bash: ifade1: command not found

root@bulutbilisimakademi:~# ifade2="doğru"
root@bulutbilisimakademi:~# echo $ifade2
>>doğru
```

+ Ayrıca değişkenlerin değerini belirtirken kullandığımız tırnak işaretleri, değerin birden fazla kelime bütünü içerdiği durumda sistem tarafından değerin tamamının doğru algılanabilmesi adına çok önemlidir. 

Örneğin `kalem="kırmızı"` ya da `kalem=kırmızı` şeklinde değişken tanımlayabiliriz. Fakat değerin `kalem1="kırmızı kalem"` gibi daha fazla öge içerdiği durumlarda mutlaka tırnak içerisinde yazılması gerekir. Bu durumu aşağıdaki çıktılara göz atarak teyit edelim:

``` {.sh}
root@bulutbilisimakademi:~# kalem1="kırmızı kalem"
root@bulutbilisimakademi:~# echo $kalem1
>>kırmızı kalem

root@bulutbilisimakademi:~# kalem2=mavi kalem
>>bash: kalem2: command not found
```

Değişkenler yeniden tanımlanabildiği için sistemin çalışmasında rol oynayan, varsayılan olarak tanımlanmış olan değişkenlerle aynı isimlere sahip yeni değişkenler oluşturmama konusunda da dikkatli olmamız gerekiyor. Eğer farkında olmadan sisteme ait değişkenleri yeniden tanımlarsanız, sistemle ilgili pek çok soruna yol açabilirsiniz. Bu yüzden, tanımlayacağınız değişkenin daha önce kullanılıp kullanılmadığından tam olarak emin değilseniz, değişkeninizi tanımlamadan önce sistem üzerinde var olup olmadığını kontrol etmenizde fayda var.

Konsola `echo` yazıp `$` işareti koyduktan sonra `Tab` tuşuna basarak tanımlı tüm değişkenleri listeleyebiliriz:

``` {.sh}
root@bulutbilisimakademi:~# echo $ 
>>
$sistem
$rakamlar
$cali
$yeni_yeni
$kitap1
$TEST
$test
$ifade2
$kalem1
```

Bu sayede halihazırda sistemde tanımlı olan değişkenlere müdahale etmeden daha bilinçli şekilde yeni değişkenler tanımlayabiliriz. Şimdi sırasıyla farklı türden değişkenleri nasıl tanımlarız bunlara göz atalım.

Değişkenlerin belirli türlerde değer almasını sağlamak için `declare` komutunu kullanıyoruz. Bu komutun parametrelerine göz atalım:

`-p` : Değişkenin niteliklerini bastırma işlevindedir. print(yazdır) ifadesinin kısaltmasıdır.

`-i` : Sayısal değişken tanımlama işlevindedir. integer(tam sayı) ifadesinin kısaltmasıdır.

`-a` : Dizi tanımlama işlevindedir. array(dizi) ifadesinin kısaltmasıdır.

`-r` : Sabit değişken atama işlevindedir. readonly(yalnızca okunabilir) ifadesinin kısaltmasıdır.

`-x` : Değişkeni export(ihraç) ederek, alt kabuklara aktarma işlevindedir.


`declare` komutunu kullanıyorken; eğer değişkenlere özellik eklemek istiyorsak "-" işaretini, şayet var olan özellikleri çıkarmak istiyorsak da "+" işaretini, eklemek ya da çıkarmak istediğimiz özelliğin parametresini de belirterek kullanmamız yeterli olacaktır.


Böylelikle değişken tanımlamanın temellerine değinmiş olduk. Gelecek bölümde bu konunun detaylarına ineceğiz.

