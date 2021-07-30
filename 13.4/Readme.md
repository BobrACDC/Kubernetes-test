<h4>Домашнее задание к занятию "13.4 инструменты для упрощения написания конфигурационных файлов. Helm и Jsonnet"</h4>

В работе часто приходится применять системы автоматической генерации конфигураций. Для изучения нюансов использования разных инструментов нужно попробовать упаковать приложение каждым из них.


<h5> Задание 1: подготовить helm чарт для приложения
</h5> 
Необходимо упаковать приложение в чарт для деплоя в разные окружения. Требования:

каждый компонент приложения деплоится отдельным deployment’ом/statefulset’ом;
в переменных чарта измените образ приложения для изменения версии.


Чарты приложения представлены в соответствующих папках:
h_backend: для бэкенда
h_frontend: для фронтенда
h_postgres: для БД


<h5> Задание 2: запустить 2 версии в разных неймспейсах
</h5> 
Подготовив чарт, необходимо его проверить. Попробуйте запустить несколько копий приложения:

одну версию в namespace=app1;
 - команды
   ```
   # helm install app11test h_backend
   # helm upgrade --install app11test h_backend
     ```
     
 ![2 1](https://user-images.githubusercontent.com/54946404/127622743-335caa9d-16ef-459b-a3ea-11f3aac684b3.png)

 
 - вывод запущенных деплоев
   
   ```
    helm list
   ```
   
   ![2 2](https://user-images.githubusercontent.com/54946404/127622799-df28f346-0c05-4be9-a67a-2ae7269d8bf7.png)


вторую версию в том же неймспейсе;
- команды

 ```
 helm install app12test --set name=prod-be-2test h_backend
```

![3 11](https://user-images.githubusercontent.com/54946404/127622911-7b3c5b0d-62b2-4b42-a169-99bde0c3811d.png)


 - вывод запущенных деплоев
```   
    helm list
```
![3 12](https://user-images.githubusercontent.com/54946404/127622962-1ef59c69-de16-422f-85da-a8e0e8261d7d.png)


третью версию в namespace=app2.
- команды
```
helm install app13test h_backend --namespace app2 --create-namespace
```

![3 11](https://user-images.githubusercontent.com/54946404/127623019-acf14d37-34e7-4a06-a9c8-95a5b7569353.png)

 - вывод запущенных деплоев
   ```
   helm list
   ```
   ![3 12](https://user-images.githubusercontent.com/54946404/127623067-55551372-2782-4231-a923-76d96339905b.png)



kubectl get deploy
![3 13](https://user-images.githubusercontent.com/54946404/127623104-531b1dae-b3b3-411d-80c3-a9db91f0ec2d.png)
