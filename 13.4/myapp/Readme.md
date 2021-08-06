<h4>Домашнее задание к занятию "13.4 инструменты для упрощения написания конфигурационных файлов. Helm и Jsonnet"</h4>

В работе часто приходится применять системы автоматической генерации конфигураций. Для изучения нюансов использования разных инструментов нужно попробовать упаковать приложение каждым из них.


<h5> Задание 1: подготовить helm чарт для приложения
</h5> 
Необходимо упаковать приложение в чарт для деплоя в разные окружения. Требования:

каждый компонент приложения деплоится отдельным deployment’ом/statefulset’ом;
в переменных чарта измените образ приложения для изменения версии.


Чарт приложения myapp


<h5> Задание 2: запустить 2 версии в разных неймспейсах
</h5> 
Подготовив чарт, необходимо его проверить. Попробуйте запустить несколько копий приложения:

одну версию в namespace=app1;
 - команды
   # helm install myapp1 myapp --namespace app11 --create-namespaced
   # helm upgrade --install myapp1 myapp --namespace app11 --create-namespace

 - вывод запущенных деплоев
   # helm list
![ins+err](https://user-images.githubusercontent.com/54946404/128476374-21ef6e9d-961e-4042-b3e6-d132f9107bd2.png)



вторую версию в том же неймспейсе;
- команды
   #  helm install myapp2 myapp/values-2.yaml myapp

 - вывод запущенных деплоев
   # helm list
 
третью версию в namespace=app2.
- команды
   # helm install myapp3 myapp --namespace app22 --create-namespace 

 - вывод запущенных деплоев
   # helm list
   


![helmlist](https://user-images.githubusercontent.com/54946404/128476292-4c72fd4a-ed17-433e-b3f6-43b4f7c38532.png)




# kubectl get deploy
