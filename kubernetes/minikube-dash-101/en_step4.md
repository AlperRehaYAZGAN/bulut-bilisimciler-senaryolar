
### Deploy Containers

Çalışan bir kubernetes cluster'ına artık container'lar deploy olabilir.

`kubectl run` komutu, container'ların cluster'ına deploy olmasını sağlar -
 `kubectl create deployment first-deployment --image=katacoda/docker-http-server`

`kubectl get pods` komutu ile çalışan pod'lar ile deployment durumu görüntülenir.

`kubectl expose deployment first-deployment --port=80 --type=NodePort`

Container çalıştığında, gereksinimlere bağlı olarak farklı ağ seçenekleri aracılığıyla kullanıma sunulabilir. Olası bir çözüm, bir container'a dinamik bir bağlantı noktası sağlayan NodePort'tur. 

Aşağıdaki komut, tahsis edilen bağlantı noktasını bulur ve bir HTTP isteği yürütür.

`export PORT=$(kubectl get svc first-deployment -o go-template='{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}')
echo "Accessing host01:$PORT"
curl host01:$PORT`

Sonuçta, container isteği işler.
