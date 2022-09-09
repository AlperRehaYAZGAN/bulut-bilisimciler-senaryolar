### ArgoCD Kurulumu

+ Argo CD Kurulumu

Uygulamaları dağıtabilmemizi sağlayan Argo CD aracını clusterımıza yükleyelim. Halihazırda Kubernetes kurulu ortamımızda aşağıdaki adımları izleyerek Argo CD kurabiliriz.

Öncelikle argocd isminde bir namespace oluşturalım. `kubectl create namespace argocd`

`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml` komutu ile Argo CD GitHub sayfasında yer alan tanım dosyaları ile kurulumu gerçekleştirebiliriz.

`kubectl get all -n argocd` komutu ile Argoocd namespace'inde oluşturulan objeleri listeleyelim.

Varsayılan olarak Argo CD API sunucusu harici bir IP ile ile expose edilmez. Bunun için argocd-server servis tipini LoadBalancer olarak değiştirelim.

`kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}' `  

Ayrıca port-forwarding de API server'a bağlanmak için kullanılabilir. Aşağıdaki komut ile port-forwarding sağlanır.

`kubectl port-forward svc/argocd-server -n argocd 8080:443`

Artık API Server'a https://localhost:8080 üzerinden erişilebilir. Gidip ArgoCD arayüzü ile tanışma zamanı!

Admin hesabının ilk parolası otomatik olarak oluşturulur ve Argo CD kurulum ad alanınızda argocd-initial-admin-secret adlı bir gizli alan parolasında açık metin olarak saklanır. Bu şifreyi kubectl kullanarak kolayca alabilirsiniz. Başka bir terminal tab'ı içerisinde aşağıdaki komutu çalıştırın.

`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`

Artık kullanıcı admin olan Argocd hesabının password bilgisine sahipsiniz. Bu bilgiler ile https://localhost:8080 adresinden ArgoCD'ye giriş sağlayabilirsiniz.  

Tebrikler ArgoCD kurulumunu tamamladınız.

