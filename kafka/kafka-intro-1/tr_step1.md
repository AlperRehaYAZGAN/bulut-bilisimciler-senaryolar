###  Seviye: Başlangıç

#### Kafka Kurulumu Makinesi  

İçerisine java kurulmuş olan Linux Pardus dağıtımıyla aşağıdaki komutlarla birlikte Kafka kurulumunu gerçekleştirebilirsiniz.

#### Talimatlar  
  
Kafkayı kurmak için /ortakatman klasörüne gidip /ortakatman/kafka klasörünü oluşturuyoruz.
- `mkdir -p /ortakatman/kafka && cd /ortakatman/kafka`  
  
Kafka kaynak kodunu indiriyoruz.
- `wget https://archive.apache.org/dist/kafka/3.2.1/kafka_2.13-3.2.1.tgz`  
  
İndirdiğimiz Kafka kaynak kodunu sıkıştırılmış dosyadan çıkartıyoruz ve sıkıştırılmış dosyayı siliyoruz.  
- `tar -zxvf kafka_2.13-3.2.1.tgz && rm kafka_2.13-3.2.1.tgz`  
  
Kaynak kodu alt klasörden güncel dizinimize alıyoruz.  
- `mv kafka_2.13-3.2.1/* . && rm -rf kafka_2.13-3.2.1`  
  
Kaynak kodu terminal ekranından direkt olarak erişebilmemiz için /opt/kafka klasörüne taşıyoruz.
- `mv /ortakatman/kafka /opt/kafka`  
  
Kafka çözümü çalışması için ZooKeeper uygulamasına gereksinim duyar. Bu sebeple kafka uygulamamızı ayağa kaldırmadan önce ZooKeeper uygulamasını çalıştırmamız gerekmektedir.  
- `/opt/kafka/bin/zookeeper-server-start.sh /opt/kafka/config/zookeeper.properties &`  
  
Kafka uygulamamızı çalıştırmadan önce config dosyasını güncellememiz gerekmektedir. Bu sebeple aşağıdaki komutu çalıştırarak Kafka uygulamamıza 9092 portunu dinlemesini sağlıyoruz.  
-`echo "listeners=PLAINTEXT://localhost:9092" >> /opt/kafka/config/server.properties`  
  
Kafka uygulamasını ayağa kaldırıyoruz...  
- `/opt/kafka/bin/kafka-server-start.sh /opt/kafka/config/server.properties &`  
  
Tebrikler Kafka uygulamamız çalıştı 🚀. Şimdi ise Pub&Sub metodolojisini kullanarak bir mesaj gönderip alalım. Onun için öncelikle bir topic oluşturmalı ve ardından bu topic üzerine mesaj gönderecek bir producer oluşturmalıyız. Son olarak da bu topic üzerinden mesajları alacak bir consumer'ı aşağıdaki komutları uygulayarak oluşturmalıyız.  

Topic oluşturuyoruz.  
- `/opt/kafka/bin/kafka-topics.sh --create --topic BBILISIMCILER --bootstrap-server localhost:9092`  
  
Producer oluşturup bu topic'e mesaj yolluyoruz. (Bu komutu çalıştırdıktan sonra CTRL+Z diyerek arka plana atayabilirsiniz.)  
- `/opt/kafka/bin/kafka-console-producer.sh --topic BBILISIMCILER --bootstrap-server localhost:9092`  
  
Consumer oluşturarak bu topic'e bağlanıp mesaj var ise bu mesajı alıyoruz.  
- `/opt/kafka/bin/kafka-console-consumer.sh --topic BBILISIMCILER --from-beginning --bootstrap-server localhost:9092`  
  
Tebrikler Kafka uygulamamızı başarıyla çalıştırdınız 🚀. Daha detaylı komutları öğrenmek için [BU_LINK](https://kafka.apache.org/quickstart) adresini ziyaret edebilirsiniz.

