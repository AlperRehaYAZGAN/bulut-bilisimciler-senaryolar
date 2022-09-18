### ArgoCD Kurulumu

+ Kubernetes ortamının ArgoCD'ye hazır hale getirilmesi.

Öncelikle node1 makinemize kubernetes master rolü ile ayağa kalkması ve hazırlanması için aşağıdaki komutu yazıyoruz.  

`kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16`  (Bu komut uzun sürmektedir.)
  
Yukarıdaki komut çalışana kadar bekliyoruz. Master makinemize worker rolüne sahip makineleri ekleyebilmemiz için master makinesinde çalıştırdığımız yukarıdaki sorgu sonucunda çıkan `kubeadm join ${MASTER_IP_PORT} --token ${MASTER_TOKEN} --discovery-token-ca-cert-hash sha256:${MASTER_SHA256_TOKEN}` yapısındaki kodu buluyoruz ve node2 ve node3 isimli iki makine daha oluşturarak bu kodu oradaki makinelere yapıştırıyoruz.  

Worker makinelerde:  
`kubeadm join ${MASTER_IP_PORT} --token ${MASTER_TOKEN} --discovery-token-ca-cert-hash sha256:${MASTER_SHA256_TOKEN}`  

Bu kodun çalışması sonucunda ana master makinemize gelip `kubectl get nodes` diyoruz ve eklediğimiz worker makineler ile birlikte ekran çıktımız:  

```
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   45s   v1.20.1
node2   NotReady <none>                 10s   v1.20.1
node3   NotReady <none>                 9s    v1.20.1
```  

Makinelerimiz NotReady durumundan Ready durumuna gelene kadar bekliyoruz. Worker node eklenmesi tamamlandığında `kubectl get nodes` komutumuzun çıktısı aşağıdaki gibi olmalıdır:  

```
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   20m   v1.20.1
node2   Ready    <none>                 19m   v1.20.1
node3   Ready    <none>                 19m   v1.20.1
```  

Kubernetes ortamımız kurulduğuna göre ArgoCD kurulumuna geçebiliriz.

+ Argo CD Kurulumu

Uygulamaları dağıtabilmemizi sağlayan Argo CD aracını clusterımıza yükleyelim. Halihazırda Kubernetes kurulu ortamımızda aşağıdaki adımları izleyerek Argo CD kurabiliriz.

Öncelikle argocd isminde bir namespace oluşturalım. `kubectl create namespace argocd`

`kubectl apply -n argocd -f https://gist.githubusercontent.com/AlperRehaYAZGAN/15b009980e20486f2bd08deb5e8eea64/raw/7184d4bd91b9e117ae61c8e07dd19648710f0e12/argocd_stable_mirror.yaml` komutu ile Argo CD GitHub sayfasında yer alan tanım dosyalarının bizim ortamımız için özelleşmiş hali ile kurulumu gerçekleştirebiliriz.

`kubectl get all -n argocd` komutu ile Argoocd namespace'inde oluşturulan objeleri listeleyelim.

Varsayılan olarak Argo CD API sunucusu harici bir IP ile ile expose edilmez. Bunun için argocd-server servis tipini LoadBalancer olarak değiştirelim.

`kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}' `  

Ayağa kalkan ArgoCD uygulamamızın hangi portta çalıştığını bulabilmemiz için aşağıdaki kodu çalıştırıyoruz.  

`kubectl get svc --all-namespaces -o go-template='{{range .items}}{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}{{end}}'`  

Bu komut sonrası karşımıza çıkan iki port numarasını da sağ yukarıdaki bölgede bulunan makine ve port bilgileri kısmına yazıp makinelere erişmeye çalışıyoruz.  


Artık API Server'a sağ yukarıdaki erişim paneli üzerinden erişilebilir. Gidip ArgoCD arayüzü ile tanışma zamanı!

Admin hesabının ilk parolası otomatik olarak oluşturulur ve Argo CD kurulum ad alanınızda argocd-initial-admin-secret adlı bir gizli alan parolasında açık metin olarak saklanır. Bu şifreyi kubectl kullanarak kolayca alabilirsiniz. Başka bir terminal tab'ı içerisinde aşağıdaki komutu çalıştırın.

`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`

Artık kullanıcı admin olan Argocd hesabının password bilgisine sahipsiniz. Bu bilgiler ile https://localhost:8080 adresinden ArgoCD'ye giriş sağlayabilirsiniz.

Tebrikler ArgoCD kurulumunu tamamladınız.
