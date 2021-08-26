## Домашнее задание к занятию "14.3 Карты конфигураций"

## Задача 1: Работа с картами конфигураций через утилиту kubectl в установленном minikube

Выполните приведённые команды в консоли. Получите вывод команд. Сохраните
задачу 1 как справочный материал.

### Как создать карту конфигураций?

```
kubectl create configmap nginx-config --from-file=nginx.conf
kubectl create configmap domain --from-literal=name=netology.ru
```

![1](https://user-images.githubusercontent.com/54946404/130913182-6cd93175-3e81-4844-814f-b05e6db9d2bb.png)



### Как просмотреть список карт конфигураций?

```
kubectl get configmaps
kubectl get configmap
```


![2](https://user-images.githubusercontent.com/54946404/130913205-fca0561f-b959-4a29-aa44-8aedd86ec3e9.png)



### Как просмотреть карту конфигурации?

```
kubectl get configmap nginx-config
kubectl describe configmap domain
```

![7](https://user-images.githubusercontent.com/54946404/130913503-0b1f4d85-dfdf-4110-bba2-a515d051f384.png)



### Как получить информацию в формате YAML и/или JSON?

```
kubectl get configmap nginx-config -o yaml
kubectl get configmap domain -o json
```


![3 1](https://user-images.githubusercontent.com/54946404/130913329-2bbe41f0-366a-42d0-8276-48de27de8f44.png)
![3 2](https://user-images.githubusercontent.com/54946404/130913337-73798a99-c0ed-4373-9ac3-f57d66bb0fb1.png)



### Как выгрузить карту конфигурации и сохранить его в файл?

```
kubectl get configmaps -o json > configmaps.json
kubectl get configmap nginx-config -o yaml > nginx-config.yml
```

![4](https://user-images.githubusercontent.com/54946404/130913352-d1cbec8a-0946-4c01-8598-f576859abec7.png)



### Как удалить карту конфигурации?

```
kubectl delete configmap nginx-config
```

![5](https://user-images.githubusercontent.com/54946404/130913366-02f37abc-387c-4198-b06b-065bb6485bc8.png)



### Как загрузить карту конфигурации из файла?

```
kubectl apply -f nginx-config.yml
```

![6](https://user-images.githubusercontent.com/54946404/130913381-0af88206-1ffd-4ea2-a3ab-52f961be0474.png)



























## Задача 2 (*): Работа с картами конфигураций внутри модуля

Выбрать любимый образ контейнера, подключить карты конфигураций и проверить
их доступность как в виде переменных окружения, так и в виде примонтированного
тома

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

В качестве решения прикрепите к ДЗ конфиг файлы для деплоя. Прикрепите скриншоты вывода команды kubectl со списком запущенных объектов каждого типа (pods, deployments, configmaps) или скриншот из самого Kubernetes, что сервисы подняты и работают, а также вывод из CLI.

---
