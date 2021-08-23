## Домашнее задание к занятию "14.1 Создание и использование секретов"

## Задача 1: Работа с секретами через утилиту kubectl в установленном minikube

Выполните приведённые ниже команды в консоли, получите вывод команд. Сохраните
задачу 1 как справочный материал.

### Как создать секрет?

```
openssl genrsa -out cert.key 4096
openssl req -x509 -new -key cert.key -days 3650 -out cert.crt \
-subj '/C=RU/ST=Moscow/L=Moscow/CN=server.local'
kubectl create secret tls domain-cert --cert=certs/cert.crt --key=certs/cert.key
```

![1](https://user-images.githubusercontent.com/54946404/130408218-6a4607aa-81a1-4b33-ac98-02d67c172a45.png)

![2](https://user-images.githubusercontent.com/54946404/130408242-b33217b4-21b4-4a25-a5f7-99f929cabc41.png)



### Как просмотреть список секретов?

```
kubectl get secrets
kubectl get secret
```

![3](https://user-images.githubusercontent.com/54946404/130408298-aea1be2c-c1bb-45eb-9ea7-0a5dfb23f7c7.png)



### Как просмотреть секрет?

```
kubectl get secret domain-cert
kubectl describe secret domain-cert
```

![4](https://user-images.githubusercontent.com/54946404/130408344-a260b679-5960-4de7-8c77-f4a897ad6bb9.png)



### Как получить информацию в формате YAML и/или JSON?

```
kubectl get secret domain-cert -o yaml
kubectl get secret domain-cert -o json
```

![5](https://user-images.githubusercontent.com/54946404/130408380-00d4c33d-6a6c-41cf-b426-1e26ddc5f0dd.png)

![6](https://user-images.githubusercontent.com/54946404/130408400-52110259-6e93-4f04-a045-e6f412d1049a.png)



### Как выгрузить секрет и сохранить его в файл?

```
kubectl get secrets -o json > secrets.json
kubectl get secret domain-cert -o yaml > domain-cert.yml
```

![7](https://user-images.githubusercontent.com/54946404/130408421-b16369d7-5bc7-4917-899f-863f566129e6.png)



### Как удалить секрет?

```
kubectl delete secret domain-cert
```

### Как загрузить секрет из файла?

```
kubectl apply -f domain-cert.yml
```


![8](https://user-images.githubusercontent.com/54946404/130408495-984f4c7f-55bb-4938-9ecd-bfee803c07c4.png)




## Задача 2 (*): Работа с секретами внутри модуля

Выберите любимый образ контейнера, подключите секреты и проверьте их доступность
как в виде переменных окружения, так и в виде примонтированного тома.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

В качестве решения прикрепите к ДЗ конфиг файлы для деплоя. Прикрепите скриншоты вывода команды kubectl со списком запущенных объектов каждого типа (deployments, pods, secrets) или скриншот из самого Kubernetes, что сервисы подняты и работают, а также вывод из CLI.

---
