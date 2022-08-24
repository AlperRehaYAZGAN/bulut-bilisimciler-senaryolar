###  Seviye: Başlangıç

Bu bölümde çeşitli türlerde değişken tanımlamaya bakacağız. 

+ İlk olarak sayısal değişken tanımlama işlemi ile başlayalım. Sayısal değişken tanımlamak için konsola `declare -i değişken="değeri"` şeklinde komutumuzu girmemiz gerekiyor.

Örneğin, 9 değerine sahip rakam isimli bir sayısal değişken tanımlamak istediğimiz için konsola declare -i rakam="9" komutunu girmemiz gerekiyor:

``` {.sh}
root@bulutbilisimakademi:~# declare -i rakam="9"
root@bulutbilisimakademi:~# echo $rakam
>>9
```

Böylelikle "rakam" isimli sayısal değişkene 9 rakamını atamış olduk ve bu değişken, biz aksini istemedikçe yalnızca sayısal ifadeler alan bir değişken olarak sınıflandırılmış oldu. Bu durumu teyit etmek için öncelikle değişkenin sınıfını sorgulamak üzere `declare` komutunun `p` parametersini kullanarak `declare -p rakam` komutunu çalıştıralım: 

``` {.sh}
root@bulutbilisimakademi:~# declare -p rakam
>>declare -i rakam="9"
```

+ Şimdi ise dizi tanımlama işlemine bakalım. Birden fazla değeri tek bir değişken içerisine toparlamak istediğimizde dizileri kullanabiliyoruz.

Dizi tanımlamak için `declare` komutunun `-a` parametresini `declare -a dizi=(değer1 değer2 değer3)` şeklinde kullanabiliyoruz.

Ayrıca `declare `komutunu kullanmadan, dizide yer alacak ifadeleri parantez içine `dizi=(değer1 değer2 değer3)` şeklinde alarak da dizi belirtebiliyoruz. Buradaki parantezler o değişkenin bir dizi olduğunu otomatik olarak belirtiyor:

``` {.sh}
root@bulutbilisimakademi:~# declare -a dizi=(a b c d e)
root@bulutbilisimakademi:~# declare -p dizi
>>declare -a dizi=([0]="a" [1]="b" [2]="c" [3]="d" [4]="e")
```

Dizilerin kullanımına en basit örnek alışveriş listesi olarak verilebilir. Örneğin "liste" isimli bir değişken tanımlayıp bu değişkenin içerisine istediğimiz sayıda değer atayabilir ve atadığımız değerleri tek tek çağırabiliriz. Örnek olarak; konsola `liste=(su süt çay elma ekmek)` şeklinde komutu girerek, "liste" isimli değişkene birden fazla değer atamış oluruz:

``` {.sh}
root@bulutbilisimakademi:~# liste=(su süt çay elma ekmek)
root@bulutbilisimakademi:~# declare -p liste
>>declare -a liste=([0]="su" [1]="süt" [2]="çay" [3]="elma" [4]="ekmek")
```

Böylelikle her bir değere 0'dan başlayarak sırasıyla birer index numarası atanmış oldu. Yani örneğin "su" ifadesi ilk değer olduğu için 0 index numarasını almışken, 3. sıradaki "çay" değerinin index numarası 2 olmuş oldu. Bizler de sıralı şekilde atanan bu index değerleri sayesinde istediğimiz değerleri diziden çağırabiliyoruz.

Örneğin dizide yer alan ilk değeri çağırmak istersem konsola `echo ${liste[0]}` komutunu girmemiz yeterli oluyor:

``` {.sh}
root@bulutbilisimakademi:~# echo ${liste[0]}
>>su
```

Eğer tüm değişkenleri tek seferde bastırmak istersek `*` ya da `@` işaretini kullanabiliriz:

``` {.sh}
root@bulutbilisimakademi:~# echo ${liste[*]}
>>su süt çay elma ekmek

root@bulutbilisimakademi:~# echo ${liste[@]}
>>su süt çay elma ekmek
``` 

Tanımlanmış olan dizi elemanının kaç karakterden oluştuğunu öğrenmek için "#" simgesini kullanarak , komutumuzu `echo ${#dizi[değişken indexi]}` şeklinde giriyoruz.

``` {.sh}
root@bulutbilisimakademi:~# echo ${liste[2]}
>>çay
root@bulutbilisimakademi:~# echo ${#liste[2]}
>>3
```


Üstelik bu kullanım sadece diziler için değil değişkenler ve sabitler için de geçerlidir.

``` {.sh}
root@bulutbilisimakademi:~# deneme="deneme metni"
root@bulutbilisimakademi:~# echo ${#deneme}
>>12
```


Ayrıca dizi içerisinde kaç tane değişken olduğunu öğrenmek için de "#" simgesini ile birlikte index numarası kısmında "*" simgesini kullanmamız yeterli:

``` {.sh}
root@bulutbilisimakademi:~# echo ${liste[*]}
>>su süt çay elma ekmek
root@bulutbilisimakademi:~# echo ${#liste[*]}
>>5
```


Bu bölümde son olarak tanımladığımız değişkenin değerinin, değiştirilemez şekilde sabit kalmasını nasıl sağlarız buna bakalım. Bu işlem için "salt okunur" anlamına gelen `readonly`  komutunu ya da `declare` komutunun `-r` parametresini kullanabiliyoruz.

Örneğin, sabit isimli bir değişkenin değerini sabitlemek üzere konsola `readonly sabit="sabit değer"` şeklinde komutu girelim. Daha sonra, atadığımız sabit değeri değiştirmeye çalışarak, değerin gerçekten sabit olup olmadığını teyit etmeye çalışalım:

``` {.sh}
root@bulutbilisimakademi:~# readonly sabit="sabit değer"
root@bulutbilisimakademi:~# declare -p sabit
>>declare -r sabit="sabit değer"

root@bulutbilisimakademi:~# sabit="yeni değer"
>>-bash: sabit: readonly variable
```

Ve gördüğünüz gibi sabit isimli değişkenimin değeri sabit olduğu için içerisine yeni bir değer atanamadı.

Ayrıca daha önce de değindiğimiz gibi, sabit değer atama işlemini `readonly` komutu yerine, `declare` komutu ile de gerçekleştirebilirdik. Hemen bu şekilde de bir örnek yapmak adına konsola `declare -r sabit1="sabit değer 1"` şeklinde de komutumuzu girip değişkenin özelliğini `-p` parametresi ile teyit edelim:

``` {.sh}
root@bulutbilisimakademi:~# declare -r sabit1="sabit değer 1"
root@bulutbilisimakademi:~# declare -p sabit1
>> declare -r sabit1="sabit değer 1"
```

Son olarak bu değeri de değiştirmeye çalışarak değişkenin sabit olup olmadığını teyit edelim:

``` {.sh}
root@bulutbilisimakademi:~# sabit1="yeni değer 1"
>>-bash: sabit1: readonly variable
```

Ve yine gördüğünüz gibi atadığımız değişken sabit olduğundan yeni bir değer atanamadı.

Sabit değişken tanımlarken dikkat edilmesi gereken bir diğer nokta ise, sabit değişkenlerin bir kez tanımlandıktan sonra kesinlikle silinip, değiştirilemeyeceğidir. Sabit değişken bir kez tanımlandıktan sonra sabit şekilde kalır. Bu durumu teyit etmek için değişkenimizin sabitlik özelliğini declare +r komutu ile kaldırmayı deneyelim:

``` {.sh}
root@bulutbilisimakademi:~# declare +r sabit1
>>-bash: sabit1: readonly variable
```

Komutumuzu girdik ancak gördüğünüz gibi değişken sabit değere sahip olduğundan konsol bu işlemin mümkün olmadığını belirtiyor. Peki ama sabit değişkenler gerçekten sonsuza kadar tanımlandığı şekilde mi kalıyor ?

Aslında bu durum; yalnızca değişkenin tanımlandığı konsol ekranı için geçerli olduğundan, konsol kapatıldığında tanımlanan tüm değişkenlerle birlikte sabit değişkenlerin de sıfırlanmasıyla sonuçlanır.


Böylelikle bu bölümün de sonuna geldik. Bir sonraki bölümde görüşmek üzere


