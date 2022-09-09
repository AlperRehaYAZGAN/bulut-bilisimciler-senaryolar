### Flow Style 
JSON formatta yazmanıza izin veren tarzdır. Flow tarz girdilere duyarlı değildir.

Yine yan taraftaki shell ekranına:
````
vim flow.yaml
````
komutuyla vim editörünü kullanarak aşağıdaki içeriği aktarabilir veya kendiniz yazmaya çalışabilirsiniz. 

````
flow: [YAML, JSON, XML]
````
Flow tarzını kullanarak yazdığınız flow.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.

````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < flow.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olmalıdır. Bu çıktıyı almadıysanız flow.yaml dosyanızı kontrol edin !

````
{'flow': ['YAML', 'JSON', 'XML']}
````
flow.yaml dosyasının içeriğine baktığımızda girdilere ihtiyaç duymadan standart bir JSON veri tipine ait bir dosya oluşturduk.

YAML da dosya yazarken aynı anda hem blok hem de flow tarzı kullanabilirsiniz.

block_flow.yaml dosyası oluşturup aşağıdaki içeriği aktarın.

````
shopping_list:
  fruits:
    - apple
    - banana
    - cherry
  vegetables: [tomato, cucumber, lettuce]
````

İki tarzını kullanarak yazdığınız block_flow.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.

````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < block_flow.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olmalıdır. Bu çıktıyı almadıysanız block_flow.yaml dosyanızı kontrol edin !

````
{
    'shopping list': 
    {
        'fruits': ['apple', 'banana', 'cherry'],
        'vegetables': ['tomato', 'cucumber', 'lettuce']
    }
}
````