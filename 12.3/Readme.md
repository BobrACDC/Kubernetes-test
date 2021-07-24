<h5>12.3 Развертывание кластера на собственных серверах, лекция 1 </h5>
Минимальные требования к кластеру.
база данных должна быть отказоустойчивой (не менее трех копий, master-slave) и потребляет около 4 ГБ ОЗУ в работе;
кэш должен быть аналогично отказоустойчивый, более трех копий, потребление: 4 ГБ ОЗУ, 1 ядро;
фронтенд обрабатывает внешние запросы быстро, отдавая статику: не более 50 МБ ОЗУ на каждый экземпляр;
бекенду требуется больше: порядка 600 МБ ОЗУ и по 1 ядру на копию.

опишите, сколько нод в кластере и сколько ресурсов (ядра, ОЗУ, диск) нужно для запуска приложения. Расчет вести из необходимости запуска 5 копий фронтенда и 10 копий бекенда, база и кеш.





10 нод

3 - мастер-ноды 
- CPU + 2 для k8s.
          +  1 ядро для бэкенда
         
●ОЗУ  2 ГБ для k8s 
1 Гб для бэкенда
50 Мб для фронта

●Диск  50 ГБ для k8s



7 воркеров

CPU  1 ядра k8s
1 ядро для бэкенда
1 ядро для кэша

● ОЗУ 1 ГБ для k8s
4 Гб для БД / кэш
1 Гб для бэкенда
50 Мб для фронта

●Диск от 100 ГБ для k8s


Минимальные требования к кластеру:
3 ноды: CPU - от 3 
             RAM - от 3 Гб
             SSD - от 100 Гб  (т.к. для k8s нужно только 50Гб)
7 воркеров: CPU - от 3
                    RAM - от 6 Гб
                    SSD - от 150 Гб

Нужно еще делать запас, на случай того, что что-то может пойти не так. 

