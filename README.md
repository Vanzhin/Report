# Проект, который генерирует отчеты

Репозиторий содержит helm-чарты для запуска приложения.
Симфони - феймворк сервисов

## 1. Термины

- Symfony — фреймворк основного контейнера (php-fpm). Можно почитать [здесь](https://symfony.com/doc/current/index.html)

## 2. Используемые технологии

Основные технологии: PHP, Redis, PostgreSQL, RabbitMQ
Код пишем на PHP

### 2.1 Общие технологии

| Технология | Версия          | Описание                           | Ссылка                     |
|------------|-----------------|------------------------------------|----------------------------|
| PHP        | 8.3             | PHP                                | https://www.php.net        |
| PostgreSQL | 16.0-alpine3.17 | Реляционная БД                     | https://www.postgresql.org |
| Nginx      | 1.25.4          | Прокси-сервер                      | https://www.nginx.com      |
| Redis      | 7.2.1           | быстрая БД для временного хранения | https://redis.io           |          
| RabbitMQ   | 7.2.1           | Брокер сообщений                   | https://www.rabbitmq.com   |          

## 3. Подготовка окружения для запуска

1. Должен быть установлен [helm](https://helm.sh/docs/intro/install/)

2. Должен быть установлен [Docker-compose](https://docs.docker.com/compose/install/linux/#install-the-plugin-manually)

3. Должен быть установлен [Minikube](https://kubernetes.io/ru/docs/tasks/tools/install-minikube).

## 4. Установка

1. Склонировать репозиторий в текущую директорию

    ```shell
    git clone https://github.com/Vanzhin/report.git
    ```
2. Запустить minikube

    ```shell
    minikube start
    ```
3. Подключить аддон ingress

   ```shell
   minikube addons enable ingress
   ```
4. Выполнить команду

   ```shell
     helm install stack prometheus-community/kube-prometheus-stack -f ./appChart/prometheus.yaml
   ```
5. Выполнить команду, после которой можно перейти в интерфейс Прометея по роуту http://localhost:9090 (в моем
   случае http://arch.homework:9090)

   ```shell
      kubectl port-forward service/prometheus-operated  9090
   ```
6. Выполнить команду, после которой можно перейти в интерфейс Графаны по роуту http://localhost:9009 (в моем
   случае http://arch.homework:9009), 9009 выбран, т.к. он свободен у меня на машине

   ```shell
      kubectl port-forward service/stack-grafana  9009:80
   ```

## 5. Запуск

1. Выполнить команды
   ```shell
    helm install myapp appChart
    helm install myapp-profile appChartProfile
    helm install myapp-report appChartReport
    helm install myapp-notification appChartNotification

   ```
2. Для работы на локальной машине, необходимо, чтобы в /etc/hosts был прописан "127.0.0.1 arch.homework", также
   выполнить команду
   ```shell
    minikube tunnel
   ```
3. После запуска приложения должны отрабатывать [роуты](postman)
4. Инструкции есть в директории [docs](docs)
5. Удаление приложения
   ```shell
    helm delete myapp myapp-profile myapp-report myapp-notification
   ```
   