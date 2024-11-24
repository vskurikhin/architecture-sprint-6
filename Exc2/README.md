# Задание 2. Динамическое масштабирование контейнеров

## Чек-лист:
- [x] поднять локальный кластер Kubernetes в Minikube
- [x] активировать metrics-server
- [x] написать манифест развёртывания (Deployment) Kubernetes для запуска тестового приложения
- [x] написать и применить манифест сервиса (Service) для доступа к приложению
- [x] настроить динамическую маршрутизацию на основании показателей утилизации оперативной памяти с помощью HPA
- [x] создать манифест для HPA
- [x] убедиться, что всё работает как задумано


## Поднять локальный кластер Kubernetes в Minikube.
```bash
$ minikube start --vm-driver=kvm2 --cpus 8 --memory 10g
😄  minikube v1.32.0 на Ubuntu 22.04
✨  Используется драйвер kvm2 на основе конфига пользователя
👍  Запускается control plane узел minikube в кластере minikube
🔥  Creating kvm2 VM (CPUs=8, Memory=10240MB, Disk=20000MB) ...
🎉  minikube 1.34.0 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.34.0
💡  To disable this notice, run: 'minikube config set WantUpdateNotification false'

🐳  Подготавливается Kubernetes v1.28.3 на Docker 24.0.7 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
    ▪ Используется образ gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Компоненты Kubernetes проверяются ...
🌟  Включенные дополнения: storage-provisioner, default-storageclass
🏄  Готово! kubectl настроен для использования кластера "minikube" и "default" пространства имён по умолчанию
```

## Активировать metrics-server. 
```bash
$ minikube addons enable metrics-server 
💡  metrics-server is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Используется образ registry.k8s.io/metrics-server/metrics-server:v0.6.4
🌟  The 'metrics-server' addon is enabled
```

## Написать манифест развёртывания (Deployment) Kubernetes для запуска тестового приложения.
Для начального количества реплик установите значение, равное единице. Лимит памяти установите равный “30Mi”. Примените написанную конфигурацию в вашем кластере.
Deployment-shestera-scaletestapp.yaml
```bash
$ kubectl apply -f Exc2/Deployment-shestera-scaletestapp.yaml 
deployment.apps/shestera-scaletestapp-deployment created
```

## Написать и применить манифест сервиса (Service) для доступа к приложению.
```bash
$ kubectl apply -f Exc2/Service-shestera-scaletestapp.yaml                                                                                                                
service/shestera-scaletestapp-service created
$ kubectl expose deployment.apps/shestera-scaletestapp-deployment --type="NodePort" --port 8080
service/shestera-scaletestapp-deployment exposed
$ curl $(minikube service shestera-scaletestapp-deployment --url)
Идентификатор пода: shestera-scaletestapp-deployment-7767594589-4k28r
```

## Настроить динамическую маршрутизацию на основании показателей утилизации оперативной памяти с помощью HPA.
```bash
$ kubectl apply -f Exc2/HPA-shestera-scaletestapp.yaml 
horizontalpodautoscaler.autoscaling/shestera-scaletestapp-hpa created
```

## Убедиться, что всё работает как задумано.
Скриншоты добавлены.