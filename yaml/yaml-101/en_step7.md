### Yorum Satırı
YAML da yorum satırları # işareti ile yazılır.

vim editörü kullanarak sherbet.yaml dosyası oluşturup aşağaki içeriği aktarın.
````
desserts:   # desserts made with sherbet
  - kunefe  
  - baklava # best of
  - tulumba
````
'#' ifadesini kullanarak oluşturduğumuz sherbet.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.

````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < sherbet.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olmalıdır. Bu çıktıyı almadıysanız sherbet.yaml dosyanızı kontrol edin !
````
{'desserts': ['kunefe', 'baklava', 'tulumba']}
````
Görüleceği üzerine dosyada '#' ile başlayan metinler yorum satırı olarak algılanmış çıktıya bir etkisi olmamıştır.

### Etiketler (Tags)
Etiketleri kullanarak sayıları metin ifadesi olarak alabilir. Özel karakterleri metin olarak yazdırabilirsiniz.

spec.yaml dosyası oluşturup aşağaki içeriği aktarın.
````
spec:
  id: 00000010
  cpu: 4
  ssd: 128
  ram: 1024Mi
````
Oluşturduğumuz spec.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.
````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < spec.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olacaktır. Ama bir sorun var !

````
{'id': 8, 'cpu': 4, 'ssd': 128, 'ram': '1024Mi'}
````
### DİKKAT !!!
spec.yaml dosyasına bulunan id kısmına 00000010 ifadesini atamıştık fakat YAML da bulunan akıllı tahmin özelliği nedeniyle girdiğimiz bu değeri octadecimal olarak algılamış bunun neticesinde çıktıda id değeri 8 olmuştur. Bu gibi durumları önlemek için id: !!str 00000010 şeklinde yazmamız gerekmektedir. cpu ve ssd ifadeleri akıllı tahmin özelliği sayesinde sayısal bir değer algılanmış, ram kısmına ise girilen 1024Mi değeri ise sayısalla başlayıp içerisinde harfler bulunduğundan otomatik olarak metin ifadesi şeklinde algılanmıştır.

Buna göre spec.yaml dosyasının doğru içeriği aşağıdaki gibi olmalıdır.

````
spec:
  id: !!str 00000010
  cpu: 4
  ssd: 128
  ram: 1024Mi
````
Python komutunu tekrar yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olacaktır.
````
{'id': '00000010', 'cpu': 4, 'ssd': 128, 'ram': '1024Mi'}
````

### Tarihler (Dates)
YAML da timestamp (2022–03–22T22:19:56.10+02:00) gibi tarih değişkenlerini bir dize olarak saklamak isterseniz !!str ile kullanmanız gerekir.

date.yaml dosyası oluşturup önce !!str kullanmadan çalıştıralım.
````
date:
  timestamp: 2001-12-14T21:59:43.10-05:00
````
Oluşturduğumuz date.yaml dosyasının çıktısını görmek ve doğruluğunu test etmek için aşağıdaki komutu çalıştırın.
````
python3 -c 'import yaml, sys; print(yaml.safe_load(sys.stdin))' < date.yaml
````
Yukarıdaki Python komutunu yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olacaktır.
````
{
    'date': 
    {
        'timestamp': datetime.datetime(2001, 12, 14, 21, 59, 43, 100000, tzinfo=datetime.timezone(datetime.timedelta(days=-1, seconds=68400)))
    }
}
````
Fark ettiyseniz yukarıda girdiğiniz ifade zaman formatında olduğu YAML tarafından algılanmış buna göre otomatik yorumlanmıştır. İfadeyi böyle tutmak istemiyorsanız !!str ile kullanmanız gerekir. 

````
date:
  timestamp: !!str 2001-12-14T21:59:43.10-05:00
````
Python komutunu tekrar yürüttüğünüzde alacağınız çıktı aşağıdaki gibi olacaktır.

````
{'date': {'timestamp': '2001-12-14T21:59:43.10-05:00'}}
````