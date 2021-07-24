<h5> Задание 1:</h5> 
подготовить тестовый конфиг для запуска приложения
Для начала следует подготовить запуск приложения в stage окружении с простыми настройками. Требования:

под содержит в себе 3 контейнера — фронтенд, бекенд, базу;
регулируется с помощью deployment фронтенд и бекенд;
база данных — через statefulset.


1.  Конфигурация тестовой среды для фронтенда и бэкенда - 13.1/staging.yaml
Конфигурация для БД - 13.1/stagebd.yaml

```
(kali㉿kali)-[~/Documents/kube/13.1]
└─$ kubectl create -f staging.yaml                                        
deployment.apps/front-back created
                                                                                                                          
┌──(kali㉿kali)-[~/Documents/kube/13.1]
└─$ kubectl get depl              
error: the server doesn't have a resource type "depl"
                                                                                                                          
┌──(kali㉿kali)-[~/Documents/kube/13.1]
└─$ kubectl get deploy                                                                                                1 ⨯
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
front-back       0/1     1            0           15s
hello-minikube   1/1     1            1           2d22h
hello-node       1/1     1            1           131m
web              1/1     1            1           2d22h
web2             1/1     1            1           2d21h
                                                                                                                          
┌──(kali㉿kali)-[~/Documents/kube/13.1]
└─$ kubectl describe deployment front-back
Name:                   front-back
Namespace:              default
CreationTimestamp:      Fri, 23 Jul 2021 12:39:23 +0300
Labels:                 app=frontback
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=frontback
Replicas:               1 desired | 1 updated | 1 total | 0 available | 1 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=frontback
  Containers:
   front:
    Image:        nginx:1.14.2
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
   back:
    Image:        debian
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      False   MinimumReplicasUnavailable
  Progressing    True    ReplicaSetUpdated
OldReplicaSets:  <none>
NewReplicaSet:   front-back-56f887dcd4 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  38s   deployment-controller  Scaled up replica set front-back-56f887dcd4 to 1




(kali㉿kali)-[~/Documents/kube/13.1]
└─$ kubectl apply -f stagesrv.yaml                                                  
service/frontback-svc created
statefulset.apps/cassandra created
                                                                                                                          
┌──(kali㉿kali)-[~/Documents/kube/13.1]



─(kali㉿kali)-[~]
└─$ kubectl get services                                                                                              1 ⨯
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
frontback-svc    NodePort    10.109.181.174   <none>        80:30080/TCP     28s
hello-minikube   NodePort    10.97.226.127    <none>        8080:30445/TCP   2d23h
kubernetes       ClusterIP   10.96.0.1        <none>        443/TCP          2d23h
web              NodePort    10.111.140.182   <none>        8080:32148/TCP   2d22h
web2             NodePort    10.106.2.231     <none>        8080:31274/TCP   2d22h
                                                                                                                          
$ kubectl get statefulset
NAME                                READY   AGE
cassandra                           0/1     6m39s
nfs-server-nfs-server-provisioner   1/1     30h
postgres                            1/1     30h
```

![cassandra_descr](https://user-images.githubusercontent.com/54946404/126877274-5af75702-893d-48e2-a0e0-f5ff944f3d28.png)






<h5>Задание 2: </h5>
подготовить конфиг для production окружения
Следующим шагом будет запуск приложения в production окружении. Требования сложнее:

каждый компонент (база, бекенд, фронтенд) запускаются в своем поде, регулируются отдельными deployment’ами;
для связи используются service (у каждого компонента свой);
в окружении фронта прописан адрес сервиса бекенда;
в окружении бекенда прописан адрес сервиса базы данных.



Конфигурация собрана в папке shop.
Для бэкенда - 13.1/shop/backend.yaml
Для фронтенда - 13.1/shop/frontend.yaml
Для БД - 13.1/shop/postgres.yaml


![13 1 2  deploy](https://user-images.githubusercontent.com/54946404/126810288-5e469e77-f6f3-46fb-9590-1e24314e3eb9.png)
![image info] [13 1 2  deploy]![13 1 2  pods](https://user-images.githubusercontent.com/54946404/126810217-5a9110fe-5409-47a6-b5cc-6905e3f1b49e.png)

Вывод команды kubectl describe po -l app=ecommerce приведено в файле describe_pod.txt
