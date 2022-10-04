### Örnek Nginx Uygulamamızı Test Edelim

Bir önceki adımda kurmuş olduğumuz Kubernetes ortmaımız uygulama çalıştırma işlemleri için hazır. Bu adımda ise bir örnek uygulama olan Nginx uygulamasını çalıştırıp test edeceğiz.  

İlk test etme aracı olarak kurmuş olduğumuz Kubernetes ortamına bir Nginx uygulaması kurup çalıştıralım. Bunun için gerekli konfigürasyon dosyalarını aşağıdaki komut ile indirelim:  
`curl -LO https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/deployment.yaml`  

Daha sonra indirdiğimiz konfigürasyon dosyasını aşağıdaki komut ile ekrana yazdıralım ve içeriğini inceleyelim:  
`cat deployment.yaml`  

Konfigürasyon dosyasında görüldüğü üzere bir Nginx uygulaması için gerekli olan Deployment ve Service objeleri tanımlanmış. Deployment objesi ile Nginx uygulamasının çalıştırılacağı Pod'lar oluşturulmuş. Service objesi ile ise Nginx uygulamasının dışarıya açılması sağlanmış. Şimdi ise bu konfigürasyon dosyasını Kubernetes ortamına uygulayalım:  
`kubectl apply -f deployment.yaml`  

Uygulama başarılı bir şekilde oluşturulduğunda aşağıdaki çıktıyı alacağız:  
`deployment.apps/nginx-deployment created`  

Deployment objesini kontrol etmek için aşağıdaki komutu çalıştıralım:  
`kubectl get deployments`  

Deployment objesinin oluşturulduğunu ve çalıştığını göreceğiz:  
```sh
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   3/3     3            3           3m
``` 

Deployment objesinin oluşturduğu Pod'ları kontrol etmek için aşağıdaki komutu çalıştıralım:  
`kubectl get pods`  

Deployment objesinin oluşturduğu Pod'ların hepsinin çalıştığını göreceğiz:  
```sh
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-66b6c48dd5-26lqt   1/1     Running   0          3m
nginx-deployment-66b6c48dd5-k847m   1/1     Running   0          3m
nginx-deployment-66b6c48dd5-n7djv   1/1     Running   0          3m
```

Deployment objesinin oluşturduğu Pod'ların hepsinin çalıştığını gördük. Şimdi ise bu Pod'ların dışarıya açılan servislerini kontrol edelim. Bunun için aşağıdaki komutu çalıştıralım:  
`kubectl get services`  

Deployment objesinin oluşturduğu Pod'ların hepsinin çalıştığını göreceğiz:  
```sh
NAME               TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes         ClusterIP                   <none>        443/TCP        4h
nginx-deployment   ClusterIP                   <none>        80/TCP         3m
```  

Dışarıya açılan servislerden bir tanesinin ClusterIP olarak tanımlanmış olduğunu gördük. Bu servislerin dışarıya açılması için bir Ingress objesi oluşturacağız:  
`kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/service/networking/nginx-ingress.yaml`  

Ingress objesinin oluşturulduğunu görmek için aşağıdaki komutu çalıştıralım:
`kubectl get ingress`  

Ingress objesinin oluşturulduğunu göreceğiz:  
```sh
NAME               HOSTS   ADDRESS   PORTS   AGE
nginx-ingress      *                 80      3m
```  

Tebrikler Kubernetes ortamınızda bir Nginx uygulaması çalıştırmayı başardınız. Şimdi ise bu uygulamayı test edelim. Bunun için öncelikle Ingress objesinin oluşturduğu servisin dışarıya açılan IP adresini öğrenelim:  
`kubectl get ingress`  

Ingress objesinin oluşturduğu servisin dışarıya açılan IP adresini öğrendik. Şimdi ise bu IP adresine bir istek atarak Nginx uygulamasının çalışıp çalışmadığını kontrol edelim. Bunun için aşağıdaki komutu çalıştıralım:  
`curl http://<IP_ADRESI>`  

Nginx uygulamasının çalıştığını göreceğiz:  
```sh
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
```

Bu çıktıları kendi web arayüzünüzde görmek için sağ yukarıdaki ilgili kısımda makine bilgilerinden "node1" ve port numarasına da "30080" yazarak erişebilirsiniz. İlk çalıştırdığınız Nginx uygulamasını başarıyla test ettiniz.  

Tebrikler 👏🏻. Kendi kurduğunuz Kubernetes ortamında bir Nginx uygulaması çalıştırmayı başardınız ve senaryoyu başarıyla tamamladınız. ✅  
