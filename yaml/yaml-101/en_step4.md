## YAML'ın Yapısı

YAML temel olarak 3 yapı taşı üzerine kurulmuştur. Bunlar;

* Diziler (Sequence): Listeler
* Anahtar Değer Çiftleri (Mapping): Sözlükler
* Skaler (Scalar): Sayılar, Boolean, Timestamp

Ayrıca YAML dosyaları yazılırken tercih edebileceğiniz iki yazım tarzı vardır. İki farklı yazım tarzı demememin nedeni yer yer bu iki tarz birlikte de kullanılabilir.

![Type](https://miro.medium.com/max/1046/1*H8M-Nc_-qO8I4TEyDjr0Jg.png)

### Block Style
Her dize elemanının başına - ifadesinin eklenmesiyle yazılır. Blok tarz girdilere duyarlıdır. Her girdi 2 adet boşluk içermelidir.

Öyleyse ilk .yaml dosyamızı yazmaya başlayalım. Yan taraftaki shell ekranına:
```` 
vim block.yaml
````
komutuyla vim editörünü kullanarak aşağıdaki içeriği aktarabilir veya kendiniz yazmaya çalışabilirsiniz. 

````
block_style:
 - YAML
 - JSON
 - XML
````
Blok tarzını kullanarak yazdığınız block.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.

````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < block.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olmalıdır. Bu çıktıyı almadıysanız block.yaml dosyanızı kontrol edin !
````
{'block_style': ['YAML', 'JSON', 'XML']}
````
block.yaml dosyasının içeriğine baktığımızda boşluk kullanılmadan yazılan ilk satırda bulunan block_style ifadesi JSON veri tipinde bir anahtara denk gelirken, block_style ifadesinin altına - ekleyerek yazdığımız her eleman ise bir dize ifadesi olarak algılanıp [YAML, JSON, XML] anahtarın değerine denktir.

Çıktının bir JSON ifadesi olduğu açıkça görülmektedir. Fakat neden böyle yazmadık da yukarıdaki gibi yazma gereği duyduk bunun en bariz nedeni bir önceki sayfada da bahsettiğim yorumlanabilme kolaylığı. Tanımlar ve ifadeler arttıkça JSON da yazmak ve yazılanı okumak işleri oldukça karmaşıklaştırır. Fakat YAML ile yazılan dosyanın okunabilirliği oldukça kolaydır.