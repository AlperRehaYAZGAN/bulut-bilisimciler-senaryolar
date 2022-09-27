## Senaryo 2

+ Argo CD Üzerinde Uygulama Oluşturma

Merhabalar, Kubernetes ortamı üzerinde Argo CD kurulumumuzu tamamladığımıza göre artık ilk Argo CD uygulamamızı deploy edebiliriz.

Argo CD arayüzü üzerinde bir uygulama oluşturmak için "+New App" butonuna tıklanır. Açılan pencere üzerinden uygulama bilgileri doldurulur. Bu örnekte Codefresh'in örnek reposundaki bir uygulamayı deploy edeceğiz. 

Aşağıda açılan pencere üzerinde uygulama bilgilerini girelim:

![argo_create_app](https://github.com/aycakcayy/bb-senaryo/raw/master/img1.png)

![argo_create_app2](https://github.com/aycakcayy/bb-senaryo/raw/master/img2.png)

Son durumda Appliation bilgileri aşağıdaki gibidir:

+ application name : `demo`
+ project: `default`
+ repository URL: `https://github.com/codefresh-contrib/gitops-certification-examples`
+ path: `./simple-app`
+ Cluster: `https://kubernetes.default.svc` 
+ namespace: `default`

Diğer parametreleri boş bırakarak Create butonuna tıkladığımızda demo uygulamamız aşağıdaki şekilde oluşur.

![argo_create_app3](https://github.com/aycakcayy/bb-senaryo/raw/master/img3.png)

Argo CD bizlere uygulamamızı otomatik veya manuel şekilde sync etme seçeneği sunar. Şanki uygulamamızda sync durumu manuel olacak şekilde bir seçim yaparak ilerledik. Yani biz manuel olarak tetiklemediğimiz sürece uygulama sync durumuna geçmeyecektir.

Uygulama şuanda OutOfSync durumundadır. Bunun anlamı;

+ Cluster boş
+ Git reposunda bir uygulama var
+ Bu nedenle Git durumu ve cluster durumu farklıdır. Git reposu ve cluster sync durumda değildir. (OutOfSync)

Ayrıca CLI’da aşağıdaki komutu çalıştırarak herhangi bir deployment oluşmadığını da görebiliriz.

`kubectl get deployments` 

![argo_create_app4](https://github.com/aycakcayy/bb-senaryo/raw/master/img4.png)

Application’ı oluştururken sync policy parametresini manuel olarak seçtiğimiz için, sync butonuna basarak uygulamayı manuel olarak tetiklemeliyiz. Sync olduktan sonra uygulamamız içine girdiğimizde aşağıdaki şekilde gözükecektir.

![argo_create_app5](https://github.com/aycakcayy/bb-senaryo/raw/master/img6.png)

Tüm kalper yeşil! Uygulamamız başarıyla deploy oldu!

Tekrar `kubectl get deployments` dediğimizde oluşan uygulamamızı artık görüntüleyebiliriz.

Burada aynı zamanda Argo CD arayüzü sayesinde görselleştirilmiş bir cluster görebiliyoruz. Demo uygulamamızda yer alan,
replicaset, endpoint, pod objelerini görüntüleyebiliyoruz. Uçtan uca görselleştirilmiş bir deployment!

![argo_create_app6](https://github.com/aycakcayy/bb-senaryo/raw/master/img5.png)

Arayüz üzerinden “delete” butonuna basarak uygulamayı silip, demo çalışmasını bitirebiliriz. 
