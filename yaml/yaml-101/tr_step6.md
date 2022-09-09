### İç içe Diziler (Nested Sequences)
YAML da JSON da oluduğu gibi iç içe diziler oluşturulabilirsiniz.

İç içe dizi oluşturmayı hem blok tarzda hem de flow tarzda oluşturalım. Burada bir sınırlama yok hangisi kolayınıza geliyorsa onu kullanabilirsiniz unutmayalım ki bir önceki sayfada flow ve block tarzların ikisinde aynı anda kullanabiliyorduk bu biraz yoğurdu nasıl yemek istediğinizle alakalı. 😄😄😄 

Bu örneği mixed.yaml dosyasında ele alarak ikisi arasında herhangi bir fark olmadığını görebilirsiniz.

````
block_lists:
-
  - yaml
  - json
-
  - python
  - java

flow_list:
- [yaml, json]
- [python, java]
````

İç içe diziler kullanarak yazdığınız mixed.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.

````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < mixed.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olmalıdır. Bu çıktıyı almadıysanız mixed.yaml dosyanızı kontrol edin !

````
{
    'block_lists': 
    [
        ['yaml', 'json'], 
        ['python', 'java']
    ], 

    'flow_list': 
    [
        ['yaml', 'json'],
        ['python', 'java']
    ]
}
````
