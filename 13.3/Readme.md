<h4>Домашнее задание к занятию "13.3 работа с kubectl"</h4>

Для выполнения задания использовалась тестовая среда из задания 13.1: приложение состоит из фронта, бэка и БД. 
Фронт и бэк разворачиваются в разных деплойментах. 

Развернутые поды приложения:
```
┌──(kali㉿kali)-[~/Documents/kube/13.1/shop]
└─$ kubectl get po -l app=ecommerce            
NAME                          READY   STATUS    RESTARTS   AGE
postgres-0                    1/1     Running   0          3d23h
product-be-56f584c9b7-pdw8d   1/1     Running   0          3d23h
product-fe-56946dbfdc-qrwl5   1/1     Running   0          3d23h

```

, где
- postgres-0   - база данных
- product-be-56f584c9b7-pdw8d - бэкенд
- product-fe-56946dbfdc-qrwl5 - фронтенд



<h5> Задание 1: проверить работоспособность каждого компонента
</h5> 
Для проверки работы можно использовать 2 способа: port-forward и exec. Используя оба способа, проверьте каждый компонент:

сделайте запросы к бекенду;
сделайте запросы к фронту;
подключитесь к базе данных.


Команда для port-forwarding: kubectl port-forward deployment/product-be :8080
Выводы:

Фронтенд

![to front port-forward](https://user-images.githubusercontent.com/54946404/127142034-71686e51-c945-44bc-a92f-cad0a8914b5f.png)


Бэкенд

![to back port-forward](https://user-images.githubusercontent.com/54946404/127142057-02922dbd-8429-43a5-85e3-2c6d2c9772d5.png)


База данных/сервис

![db port-forw](https://user-images.githubusercontent.com/54946404/127142107-6c0867ca-9621-4645-8f79-8fc3ecd9acea.png)



Команда для exec: kubectl exec -ti product-fe-56946dbfdc-qrwl5 /bin/bash
Внутри контейнера был сделан запрос на другой контейнер с помощью утилиты curl: curl http://172.17.0.22:8080

Адрес и порт соответствующего контейнера были взяты из вывода команды: kubectl describe po postgres-0

Запрос с фронта на бэк:

![from front to back](https://user-images.githubusercontent.com/54946404/127142131-aec8b64f-c24f-48da-9089-965730649d45.png)

Запрос с бэка на фронт:

![from back to front ](https://user-images.githubusercontent.com/54946404/127142159-d4b3992a-c35f-4504-bed0-5647d7cdd777.png)


БД:

![db_exec](https://user-images.githubusercontent.com/54946404/127142166-5fbb8637-c20b-4dbf-81cc-224f94419513.png)



<h5> Задание 2: ручное масштабирование
</h5> 
При работе с приложением иногда может потребоваться вручную добавить пару копий. Используя команду kubectl scale, попробуйте увеличить количество бекенда и фронта до 3. После уменьшите количество копий до 1. Проверьте, на каких нодах оказались копии после каждого действия (kubectl describe).


Масштабирование проводилось с помощью команды: kubectl scale --replicas=1 deployment/product-be
Просмотр состояния: kubectl describe deploy product-fe
Выводы соответствующих команд для каждого деплоймента приведены ниже.



Установка 3 реплик:
![scale1](https://user-images.githubusercontent.com/54946404/127142210-dc0001b8-8353-402c-a5c4-cd11c6a8721e.png)
![scale2](https://user-images.githubusercontent.com/54946404/127142213-264380cc-3ab8-452f-be57-0a1de28558e9.png)


Установка 1 реплики:

![scale3](https://user-images.githubusercontent.com/54946404/127142231-9e252796-65ba-48c3-a752-cbe465268a5b.png)
![scale4](https://user-images.githubusercontent.com/54946404/127142239-73d47b59-fcc6-48a0-99aa-e73ba41ad850.png)
