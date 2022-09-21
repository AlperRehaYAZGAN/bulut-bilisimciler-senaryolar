## Collection'lar ve CRUD işlemleri

Bu bölümde, Bulut Bilişimciler interaktif platformumuzda bir veritabanı, collection, kullanıcı oluşturmayı öğrenip temel bir kaç CRUD komutu çalıştıracağız.
Mongodb de create database gibi bir komut yoktur, bir veritabanı oluşturmak için `use veritabaniismi` dersiniz ve daha sonra içerisinde bir collection oluştursanız veritabanınız oluşmuş olur. Aşağıdaki örnekte bulutbilisimciler isminde bir veritabanı içerisinde bulutcollection isimli bir collection oluşturuyoruz.

```
MongoDB > use bulutbilisimciler
switched to db bulutbilisimciler
MongoDB > db.bulutcollection.insertOne( { x: 1 } )
{
        "acknowledged" : true,
        "insertedId" : ObjectId("631ce7c6e0a10591370a6054")
}
MongoDB > show dbs
admin              0.000GB
bulutbilisimciler  0.000GB
config             0.000GB
local              0.000GB
MongoDB Enterprise > 
``` 

Collection oluşturmak içinde gördüğünüz gibi create komutu kullanmadık. Fakat aşağıdaki örnekteki gibi de  collection oluşturabilirdik. Bu örnekte arabalar isminde boş bir collection oluşturup, tablo özelliklerini parametre olarak belirtiyoruz.

```
MongoDB >  db.createCollection("arabalar", { capped : true, detay : 5242880, max : 5000 } );
{ "ok" : 1 }
````
Şimdi biraz daha DML işlemlerini nasıl yapacağımıza bakalım.
Mongodb, insert işlemi için bize 2 farklı seçenek sunar. Tek satır eklemek için `insert()`, birden çok satır eklemek için `insertMany()` kullanabilirsiniz.

```
MongoDB > db.arabalar.insert({"marka" : "Voswogen","model" : "Polo","yil" : 2015})
**Çıktısı**
WriteResult({ "nInserted" : 1 })

MongoDB > db.personeller.insertMany( [
...    { sID: 1982, name: "Gizem", year: 1, title: "Expert" },
...    { sID: 1985, name: "Aslı", year: 2, title: "Junior" },
...    { sID: 2842, name: "Arzu", year: 3, title: "Middle" },
...    { sID: 4214, name: "Büşra", year: 1, title: "Expert" },
...    { sID: 173, name: "Şerife", year: 6, title: "Junior" }
... ] )

**Çıktısı:**
{
        "acknowledged" : true,
        "insertedIds" : [
                ObjectId("631f907b0840908ca64149a3"),
                ObjectId("631f907b0840908ca64149a4"),
                ObjectId("631f907b0840908ca64149a5"),
                ObjectId("631f907b0840908ca64149a6"),
                ObjectId("631f907b0840908ca64149a7")
        ]
}
```
Peki bir `view` oluşturmak istesek bunu nasıl yaparız? Öncelikle view'ı, collection içerisindeki belirli dataları belirli kullanıcılara ulaştırmak için kullanabiliriz. Bir bakıma filtreleme olarak düşünebilirsiniz.  Aşağıda **Expertler** adında bir view oluşturup, yukarıda oluşturmuş olduğumuz **personeller** tablosunun sadece title'ı Expert olan verilerini görüntülemesini sağlıyoruz. **ok:1** çıktısı işlemin başarılı olduğunu söyler. Daha sonra `find()` komutuyla bu view'a select atarak içerisindeki verileri görüntüleyebilirsiniz.
```
MongoDB > db.createView(
...    "Expertler",
...    "personeller",
...    [ { $match: { title: "Expert" } } ]
... )
{ "ok" : 1 }

MongoDB > db.Expertler.find({}, { _id: 0 } )
{ "sID" : 1982, "name" : "Gizem", "year" : 1, "title" : "Expert" }
{ "sID" : 4214, "name" : "Büşra", "year" : 1, "title" : "Expert" }
```

Bir update işlemi yapmak istersek mongodb bize aşağıdaki 3 seçeneği de sunar:
**db.collection.updateOne(<filter>, <update>, <options>)**
**db.collection.updateMany(<filter>, <update>, <options>)**
**db.collection.replaceOne(<filter>, <update>, <options>)**

Urunler adında bir tablo oluşturalım ve aşağıdaki gibi update yapalım. İnsert ederken acknowledge:true olarak gördüğünüz çıktı işlemin başarılı olduğunu söyler.
```
MongoDB > db.urunler.insertMany( [
...    { item: "telefon", qty: 56, detay: { marka: "apple", model: 3.4}, status: "Mevcut" },
...    { item: "tablet", qty: 34, detay: { marka: "hp", model: "pavilion15" }, status: "Stokta yok" },
...    { item: "bilgisayar", qty: 45, detay: {  marka: "Lenova", model: "Thinkpad" }, status: "Mevcut" }
... ] );
**Çıktısı**
{
        "acknowledged" : true,
        "insertedIds" : [
                ObjectId("631f939d0840908ca64149ab"),
                ObjectId("631f939d0840908ca64149ac"),
                ObjectId("631f939d0840908ca64149ad")
        ]
}
```
Tablomuzu oluşturduktan sonra, tablet'in model ve statu bilgilerini update edelim.
```
MongoDB > db.urunler.updateOne(
...    { item: "tablet" },
...    {
...      $set: { "detay.model": "pavilion17", status: "Mevcut" },
...      $currentDate: { lastModified: true }
...    }
... )

MongoDB  > db.urunler.find( { item: "tablet" } )
{ "_id" : ObjectId("631f939d0840908ca64149ac"), "item" : "tablet", "qty" : 34, "detay" : { "marka" : "hp", "model" : "pavilion17" }, "status" : "Mevcut"}
```

Mongodb, bir dökümanı silmek için ise bizlere 2 opsiyon sunar. 
**deleteMany()** ve **deleteOne()**. Aşağıdaki gibi tüm datayı da silebilirsiniz, spesifik bir datayıda.
```
MongoDB > db.urunler.deleteMany({})
**Çıktısı**
{ "acknowledged" : true, "deletedCount" : 3 }

db.urunler.deleteOne( { item: "telefon" } )
```

Son olarak, oluşturduğumuz tabloları drop() fonksiyonunu kullanarak aşağıdaki gibi silebiliriz.
```
db.urunler.drop() 
```

Bir veritabanını silmek için ise, db.dropDatabase() fonksiyonunu kullanmanız gerekir. Bunun için öncesinde ilgili veritabanına use diyip geçmeniz gerekmektedir. Hangi veritabanında bağlı olduğunuzu görmek için ise `db` yazmanız yeterli.
```
MongoDB > use bulutbilisimciler
switched to db bulutbilisimciler
MongoDB > db.dropDatabase()
{ "dropped" : "bulutbilisimciler", "ok" : 1 }
```
Bu senaryomuzun sonuna gelmiş bulunmaktayız :)
