# test-case
# Создать две виртуальные машины. Средство виртуализации на своё усмотрение.

Для создания виртуальных машин я использовал VirtualBox. ОС Debian
![alt text](https://github.com/kod1197/test-case/blob/main/img/Pasted%20image%2020240422132050.png)
# ·         На двух виртуальных машинах запустить два узла Rancher (Kubernetes). Способ развертывания и версию Rancher также можно выбрать на своё усмотрение.


Установка docker согласно документации
https://docs.docker.com/engine/install/debian/

Для развертывая Rancher я выбрал способ названный в документации "# Installing Rancher on a Single Node Using Docker" (https://ranchermanager.docs.rancher.com/getting-started/installation-and-upgrade/other-installation-methods/rancher-on-a-single-node-with-docker)


Установка rancher
![[Pasted image 20240418150244.png]]

![[Pasted image 20240418160843.png]]

# ·         Получить доступ к управлению кластером Kubernetes через Web UI Rancher и через командную строку (kubectl). +

После установки заходим в Web UI Rancher и выполняем предложенную команду для получения пароля 
![[Pasted image 20240420225405.png]]
Для получения доступа к управлению кластером для начала создаем кластер
![[Pasted image 20240420225018.png]]

И регистрируем ноды
![[Pasted image 20240420230057.png]]

Установка kubectl
![[Pasted image 20240418163122.png]]
https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/

Скачиваем KubeConfig
![[Pasted image 20240421131346.png]]

Создаем папку .kube и перемещаем туда скачанный конфиг, называем его config, проверяем доступ к кластеру
![[Pasted image 20240421131752.png]]

# ·         В Rancher создать новый проект и дополнительную учётную запись. Учётной записи предоставить право управлять этим проектом.+


Создание пользователя 
![[Pasted image 20240418163751.png]]

Создание проекта
![[Pasted image 20240418163855.png]]

Права пользователю на новый проект
![[Pasted image 20240418163908.png]]
# С помощью Helm Charts развернуть два Helm releases с web серверами nginx. Каждый web сервер nginx должен возвращать статичную страницу, однозначно указывающую, с  какого web сервера она возвращается. HTML код для nginx монтируется в контейнеры из соответствующих ConfigMap.
Установка helm
https://helm.sh/docs/intro/install/

Создаем helm charts
Упаковываем и устанавливаем релиз
![[Pasted image 20240418165400.png]]
# ·         Включить Ingress для Kubernetes. Web-серверы должны быть доступны по внешним IP адресам виртуальных машин, не только по hostnames или IP внутри Kubernetes.
# ·         Настроить маршруты HTTP на основе путей URI. Например, myhostname.localdomain/server1 указывает на первый web сервер, работающий внутри Kubernetes. Аналогично myhostname.localdomain/server2 указывает на второй.

Устанавливаем Nginx Ingress согласно документации
https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters

![[Pasted image 20240421161130.png]]
После установки переходим к созданию Ingress, указываем путь, сервис и нужный порт

![[Pasted image 20240421161046.png]]
Добавляем аннотацию
![[Pasted image 20240421162655.png]]

Проверяем доступность серверов
Доступность по порту 30973
![[Pasted image 20240421161642.png]]
Доступность по порту 80
![[Pasted image 20240421162106.png]]
На одной из машин добавил запись 10.0.2.6 test.host в hosts и получил доступ из браузера
![[Pasted image 20240421162258.png]]
![[Pasted image 20240421162314.png]]
