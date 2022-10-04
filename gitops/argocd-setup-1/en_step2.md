### Argo CD Kurulumu

Uygulamaları dağıtabilmemizi sağlayan Argo CD aracını clusterımıza yükleyelim. Halihazırda Kubernetes kurulu ortamımızda aşağıdaki adımları izleyerek Argo CD kurabiliriz.

Öncelikle argocd isminde bir namespace oluşturalım. `kubectl create namespace argocd`

`kubectl apply -n argocd -f https://gist.githubusercontent.com/aycakcayy/7418df830d26028ec16f399a2e57a026/raw/281a4fcb4aed799ec2c6cc87ec6a55cc58640453/argocd_mirror.yaml` komutu ile Argo CD GitHub sayfasında yer alan tanım dosyaları ile kurulumu gerçekleştirebiliriz.

`kubectl get all -n argocd` komutu ile ArgoCD namespace'inde oluşturulan objeleri listeleyelim.

ArgoCD namespace'inde oluşturulan pod'ların hepsi **Running** durumunda olmalıdır. Eğer pod'ların hepsi Running durumunda değilse `kubectl get pods -n argocd` komutunu tekrar çalıştırarak durumunu kontrol edebiliriz. Bütün pod'ların Running durumunda oluncaya kadar bekleyelim...

Varsayılan olarak Argo CD API sunucusu harici bir IP ile ile expose edilmez. Bunun için port-forwarding ile API Server'a bağlanacağız.

`kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'`

`kubectl port-forward svc/argocd-server -n argocd 8080:443 & ` : ArgoCD API sunucusuna bağlanmak için port-forwarding yapalım.

(Eğer port-forward işlemi sonucunda 8080 portuna eriştiğinizde ArgoCD ekranını göremiyorsanız aşağıdaki komutu çalıştırarak ArgoCD'nin Kubernetes tarafından otomatik olarak atanan Port numarasını öğrenip oradaki Port değeriyle arayüze erişebilirsiniz.)
`kubectl get svc --all-namespaces -o go-template='{{range .items}}{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}{{end}}'` : ArgoCD API sunucusunun port numarasını öğrenelim.

(Yukarıdaki methodlardan birinin uygulanmasıyla birlikte ArgoCD Server kullanıcı arayüzümüzün çalışacağı port numarasını alacağız. Bu port numarasını kullanarak ArgoCD'ye sağ yukarı bulunan ilgili butonlar ile giriş yapabilirsiniz.)

Admin hesabının ilk parolası otomatik olarak oluşturulur ve Argo CD kurulum ad alanınızda argocd-initial-admin-secret adlı bir gizli alan parolasında açık metin olarak saklanır. Bu şifreyi kubectl kullanarak kolayca alabilirsiniz. Başka bir terminal tab'ı içerisinde aşağıdaki komutu çalıştırın.

`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`

Artık kullanıcı admin olan Argocd hesabının password bilgisine sahipsiniz. Bu bilgiler ile https://localhost:8080 adresinden ArgoCD'ye giriş sağlayabilirsiniz.

Bizleri aşağıdaki gibi bir Argo CD arayüzü karşılıyor olacak!

![argo_homepage](https://github.com/aycakcayy/bb-senaryo/raw/master/screenpage.png)