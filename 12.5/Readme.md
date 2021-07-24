<h5> Задание 1: установить в кластер CNI плагин Calico
</h5> 
Для проверки других сетевых решений стоит поставить отличный от Flannel плагин — например, Calico. Требования:
установка производится через ansible/kubespray;
после применения следует настроить политику доступа к hello world извне

```
---
- name: main.yml | Installing Docker
  apt:
    name: docker-engine
    state: latest
  when: ansible_os_family == "Debian"

- name: main.yml | Fetching calico
  get_url:
    url: "https://github.com/projectcalico/calico-cni/releases/download/v{{ calico.version }}/calico"
    dest: /opt/cni/bin/calico
    
- name: main.yml | Fetching calicoctl
  get_url:
    url: "https://github.com/projectcalico/calico-cni/releases/download/v{{ calico.version }}/calicoctl"
    dest: /usr/bin/calicoctl    
```


Получаем:
```
─$ kubectl get pods                                      
NAME                              READY   STATUS    RESTARTS   AGE
hello-minikube-6ddfcc9757-489v8   1/1     Running   1          2d19h
web-79d88c97d6-mgj2x              1/1     Running   1          2d19h
web2-5d47994f45-4nnrk             1/1     Running   1          2d18h
                                                                                                                                           
┌──(kali㉿kali)-[~]
└─$ kubectl get services               
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort    10.97.226.127    <none>        8080:30445/TCP   2d19h
kubernetes       ClusterIP   10.96.0.1        <none>        443/TCP          2d19h
web              NodePort    10.111.140.182   <none>        8080:32148/TCP   2d19h
web2             NodePort    10.106.2.231     <none>        8080:31274/TCP   2d18h

$ kubectl expose deployment web --type=NodePort --port=8080
$ kubectl describe service web                                                                                      1 ⨯
Name:                     web
Namespace:                default
Labels:                   app=web
Annotations:              <none>
Selector:                 app=web
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.111.140.182
IPs:                      10.111.140.182
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  32148/TCP
Endpoints:                172.17.0.11:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>


 echo $(minikube ip)  
192.168.99.100
                                                                                                                          
┌──(kali㉿kali)-[~]
└─$ curl $(minikube ip):32148                                       
Hello, world!
Version: 1.0.0
Hostname: web-79d88c97d6-mgj2x


```



Network Policy:
конфигурационный файл - networkpolicy.yaml
 - разрешен весь трафик на поды, у которых есть метка: 'app: hello-node'.
 
```
 ─(kali㉿kali)-[~/Documents/kube/12.5]
└─$ kubectl apply -f networkpolicy.yaml                                                                                                   1 ⨯
networkpolicy.networking.k8s.io/allow-all-ingress created
```




<h5> Задание 2: изучить, что запущено по умолчанию
</h5> 
Самый простой способ — проверить командой calicoctl get . Для проверки стоит получить список нод, ipPool и profile. Требования:
установить утилиту calicoctl;
получить 3 вышеописанных типа в консоли.


![Screenshot 2021-07-23 19:24:00](https://user-images.githubusercontent.com/54946404/126812498-a63874b8-9c7c-47f7-8b2a-dd7106de1f92.png)

