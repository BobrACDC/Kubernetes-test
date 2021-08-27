## Домашнее задание к занятию "14.4 Сервис-аккаунты"

## Задача 1: Работа с сервис-аккаунтами через утилиту kubectl в установленном minikube

Выполните приведённые команды в консоли. Получите вывод команд. Сохраните
задачу 1 как справочный материал.

### Как создать сервис-аккаунт?

```
kubectl create serviceaccount netology
```

![1](https://user-images.githubusercontent.com/54946404/131076942-aaa505ac-a889-483e-af34-2eb635902e76.png)



### Как просмотреть список сервис-акаунтов?

```
kubectl get serviceaccounts
kubectl get serviceaccount
```

![2](https://user-images.githubusercontent.com/54946404/131076954-587786f9-b1b7-4437-b88e-823de217682d.png)



### Как получить информацию в формате YAML и/или JSON?

```
kubectl get serviceaccount netology -o yaml
kubectl get serviceaccount default -o json
```

![3](https://user-images.githubusercontent.com/54946404/131076975-7d879888-29b2-4787-920d-21eca96fa323.png)



### Как выгрузить сервис-акаунты и сохранить его в файл?

```
kubectl get serviceaccounts -o json > serviceaccounts.json
kubectl get serviceaccount netology -o yaml > netology.yml
```

![4](https://user-images.githubusercontent.com/54946404/131076986-a5734bf5-35f9-45af-877e-6f1307f1ef08.png)



### Как удалить сервис-акаунт?

```
kubectl delete serviceaccount netology
```

![5](https://user-images.githubusercontent.com/54946404/131077005-093c0bcd-8bb9-40c8-b0af-9d218697c396.png)



### Как загрузить сервис-акаунт из файла?

```
kubectl apply -f netology.yml
```

![6](https://user-images.githubusercontent.com/54946404/131077012-da6ccaf0-b267-4429-a5ce-cd1f7fc1b66a.png)

