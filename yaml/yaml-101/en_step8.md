### YAML DRY
YAML DRY işaretlenen yerlerin başka bir dizi de tekrarlanmasını sağlar. 
* '&' = Tekrarlanması istenen ifadelerin başına & eklenir.
* '*' =  Tekrarın yapılacağı yer * ile belirtilir. 
* '<<' =  Tekrar edilecek ifade de değiştirilecek yerler varsa << ile belirtilir.

vim editör ile humans.yaml dosyası oluşturup aşağıdaki içeriği aktarın. 

````
Person: &person
  Name: Mert
  Age: 25
  Adress:
    Street: Gebze
    City : Kocaeli
Person1:
  <<: *person
  Name: Onur
  Age: 20
````
'&, <<, *' ifalerini kullanarak oluşturduğumuz humans.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.

````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < humans.yaml
````
Alacağınız çıktı:
````
{
    'Person': 
    {
        'Name': 'Mert', 
        'Age': 25, 
        'Adress': 
        {
            'Street': 'Gebze', 
            'City': 'Kocaeli'
        }
    }, 

    'Person1': 
    {
        'Name': 'Onur', 
        'Age': 20, 
        'Adress': 
        {
            'Street': 'Gebze', 
            'City': 'Kocaeli'
        }
    }
}

````
humans.yaml örneğinde iki adet kişi ele alınmıştır. Bu kişilerin name, age, address anahtar çifleri aynı olduğundan bu kısımları tekrar yazmak yerine ilk kişinin anahtar çiftinin yanına tekrar etmesini istediğimiz için &person ifadesi eklenmiştir. Ardından ikinci kişi oluşturulmuş *person ile yukarıdaki ifadenin tekrarı sağlanmış fakat anahtar çiftlerinden name, age değerleri farklılık gösterdiğinden bunlara karşılık gelen değerleri güncellemek için *person ifadesinin soluna << ifadesi eklenmiş ve altına güncellenecek anahtar çifleri ve değerleri yazılmıştır. adress kısmında bir güncelleme olmamış ilk kişiye ait bilgiler ikinci kişiye de aynen aktarılmıştır.

### YAML Belgesi(YAML Document)
YAML belgeleri --- ile başlar … ile biter. Belgenin --- ile başlaması ... ile bitmesi şart değildir fakat kullanılan yerlerde denk gelmeniz durumunda ne olduğunu bilmeniz amacıyla ekledim.
````
--- 

- Apple
- Orange
- Mango

...
````