# GitOps ve Argo CD  

### Seviye: Başlangıç

### Neden GitOps?

Günümüzde hızla değişen ve genişleyen yazılım geliştirme dünyasında, dinamik bir yapıda olmak ve yeniliklere adapte olmak oldukça önemli. Zaman içerisinde, ihtiyaçları hızlı karşılayamadığımız Waterfall modelinden Agile’a geçiş yaptık. Daha küçük değişikliklerle, küçük iterasyonlarla hedefi yakalamaya başladık. Bu çevik yapının içinde, sürekli değişimleri karşılamak adına operasyon ve geliştirme takımlarının iç içe geçtiği devops kültürünü oluşturduk. Günümüz modern dünyasında ise daha büyük challengelar ile başbaşayız. Containerization’ın yaygınlaşması, Kubernetes’in hayatımıza girmesiyle beraber, herhangi bir Git reposu üzerinde tutulan uygulamaların bu Kubernetes cluster ları üzerine merkezi bir yerden deploy olması ve yönetilmesi bunlardan biri. GitOps’a bu yüzden ihtiyaç duyuyoruz.

### GitOps Nedir?

Genel bir tanımla; GitOps, versiyon kontrol, işbirliği, uyumluluk ve CI/CD araçları gibi uygulama geliştirme için kullanılan DevOps best practice'lerini alan ve bunları altyapı otomasyonuna uygulayan operasyonel bir çerçevedir.

### Argo CD Nedir?

Argo CD; Kubernetes için bildirime dayalı, GitOps metodolojisini izleyen bir sürekli teslim aracıdır.

“Uygulama tanımları, konfigürasyonları ve ortamları bildirime dayalı ve versiyon kontrollü olmalıdır” mantığı ile çalışır. Uygulama dağıtımı ve yaşam döngüsü yönetiminin otomatikleştirilmiş, denetlenebilir ve anlaşılabilir olmasını sağlar.

### Argo CD Nasıl Çalışır?

Argo CD belirli periyotlarda Kubernetes’e deploy edilmiş uygulamaları izler ve Git reposunda yer alan tanım dosyalarıyla karşılaştırmalar yapar. Herhangi bir farklılık durumunu kullanıcıyı bildirir ya da belirtilirse otomatik olarak senkronizasyon işlemini gerçekleştirir.

### Neden Argo CD ?

+ Kubernetes cluster'ınızı görselleştirir. Yani bir deployment inizi replica set,pod vb.kuberetes objeleri şeklinde görüntülenebilir.
+ Helm, customize, yaml tanım dosyalarını destekliyor.
+ Birden fazla kubernetes cluster ile entegre edilebiliyor.
+ İmperative bir şekilde kubectl kullanmıyorsunuz, yapınızı declarative yapıyorsunuz yani yaptığınız değişikliği Argo CD algılayıp Kubernetes’e yüklenmesini sağlıyor.
+ Kubernetes cluster'ınızda bir deployment silindi veya bir kesinti yaşadınız; Argo CD hem git reposu hem Kubernetes'i sürekli monitor ettiğinden ikisi arasında fark olduğunu anlayıp silinen deployment'ı tekrar yerine getirebilir.

### Öğrenme Hedefleri

GitOps senaryosunu tamamladıktan sonra;

+ GitOps prensibinin ne olduğu,
+ ArgoCD aracının ne işe yaradığıu ve nasıl kurulduğu hakkında bilgi sahibi olacaksınız.

### Ön gereksinimler

+ Linux dağıtımlarından en az birine aşina olmalı ve kullanabiliyor olmalısınız.
+ Docker ve podman gibi container araçlarını kullanabiliyor olmalısınız.
+ Kubernetes container orkestrasyonu hakkında bilgi sahibi olmalısınız.




