# REPORT-MSA

## Проект генерации отчетов

1. Должен быть установлен [helm](https://helm.sh/docs/intro/install/)
2. Склонировать репозиторий в текущую директорию

 ```shell
 git clone https://github.com/Vanzhin/report.git
 ```

3. Установить [minikube](https://kubernetes.io/ru/docs/tasks/tools/install-minikube/).
4. Запустить minikube
    ```shell
    minikube start
    ```
5. Подключить аддон ingress.
   ```shell
   minikube addons enable ingress
   ```
6. Выполнить команды
   ```shell
    helm install myapp appChart
    helm install myapp-profile appChartProfile
    helm install myapp-billing appChartBilling
    helm install myapp-order appChartOrder
    helm install myapp-notification appCharNotification
   ```
7. Для работы на локальной машине, необходимо, чтобы в /etc/hosts был прописан "127.0.0.1 arch.homework", также
   выполнить команду
   ```shell
    minikube tunnel
   ```
8. После запуска приложения должны отрабатывать [роуты](postman/HW6.postman_collection.json)
9. Инструкции есть в директории [docs](docs)
10. Удаление приложения
   ```shell
    helm delete myapp myapp-profile myapp-billing myapp-order myapp-notification
   ```
   