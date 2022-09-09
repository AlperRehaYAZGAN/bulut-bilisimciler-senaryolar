### YAML Yazarken Sık Yapılan Hatalar

![error](https://miro.medium.com/max/700/1*SYZsODxWOXCnerwHLUDEVQ.png)

### Alıntı (Quotes)
YAML da bir yol uzantısı verirken sıklıkla “ çift tırnak kullanılır” fakat yol uzantılarını ‘ tek tırnak ’ ile vermek oluşabilecek hataların önüne geçer.

````
path: 'C:\Users\Better\…'
````
### Girinti (Indentation)
YAML girintilere duyarlı bir serileştirme dilidir. Dolayısıyla dosyalar yazılırken girdiler YAML IDE ile yazılarak kontrol edilmelidir.

````
spices:
- salt
     - pepper
- cayenne pepper

#result = {'spices': ['salt - pepper', 'cayenne pepper']}
````
### Sayı Tipi (Number Type)
YAML sık yapılan yanlışlardan biri de 0 ile başlayan numaraları örneğin telefon numarası gibi vb. ‘tek tırnak içine almamaktır’ şayet tırnak kullanmadan yazarsanız YAML bunu bir hexadecimal sayı olarak algılar ve yanlış sonuçlar üretir.
````
person:
  name: Mert
  phone: 0505

#result =  {'person': {'name': 'Mert', 'phone': 325}}
````
### Yinelenen Anahtarlar (Duplicate Keys) 
Bir YAML dosyasında aynı anda iki benzer anahtara izin verilmez. Eğer kullanılmışsa eski değer ezilir son değer yazılır.

````
city:
  name: Tokat
  name: Kocaeli

#result = {'city': {'name': 'Kocaeli'}}
````
### Yanlışlıkla Liste Girişi (Accidental List Entry 
Yanlışlıkla liste girişi, bir — ile başlayan bir değeriniz olduğunda yaml bunu liste öğesi olarak algılar.

````
quote:
  mert: - Hello  I am typing YAML

#result = Error: sequence entries are not allowed 
````
### İzin Verilmeyen Anahtar Kullanımı (Lists as Keys in Languages That Don’t Allow This)
YAML da kullanılan mantıksal ifadelerin anahtar olarak kullanılmaması gerekir.

````
values:
  int:
  true:
  false:
  null:
````
### YAML Şemaları (YAML Schemas)
Şemalar YAML kurallarını içerir ve belirli bir YAML dosyasının kurallara uyup uymadığını doğrulamak için kullanılır. Şemalar ayrıca veri türleri oluşturmak için kullanılır ve dile özgü şemalarla özel veri türleri eklenebilir. YAML varsayılan şemaları şunlardır;

* Failsafe Schema: 3 etiketi vardır.

````
!!str: a string value
!!map: a mapping
!!seq: a sequnece
````
* JSON Schema: Failsafe etiketleri de dahil birçok etiketi kapsar
````
!!null: a void
!!bool: a boolean
!!int: a integer
!!float: a comma value
````
* Core Schema: JSON şemasının bir uzantısıdır ve JSON şemasıyla aynı etiketlere sahiptir ancak genişletilmiş etiket çözünürlüğüne sahiptir. dolayısıyla varsayılan olarak kullanılması tavsiye edilir.

### YAML Ayrıştırma (YAML Parsing)

![parse](https://miro.medium.com/max/700/1*0tqQait51aLyI_lQOAU89g.png)

Ayrıştırma ile bir formatın yeni bir formata dönüştürülmesini kastediyoruz. Önce YAML dosyası işlenir, ardından serileştirme gerçekleşir ve serileştirme ağacı oluşturulur. Daha sonra ağaç bir düğüm aracına dönüştürülür ve son olarak yerel veri yapısına çevrilir.