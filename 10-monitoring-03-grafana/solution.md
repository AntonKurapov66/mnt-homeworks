# Домашнее задание к занятию 14 «Средство визуализации Grafana» - Курапов Антон

## Обязательные задания

### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
1. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
1. Подключите поднятый вами prometheus, как источник данных.
1. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/10-monitoring-03-grafana/img/01.PNG)


## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/10-monitoring-03-grafana/img/02.PNG)

```
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100)

node_load1
node_load5
node_load15

node_memory_MemAvailable_bytes / 1024 / 1024 / 1024

node_filesystem_free_bytes{mountpoint="/"} / 1024 / 1024 / 1024
```

## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
1. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

алерты без нагрузки 
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/10-monitoring-03-grafana/img/03_0.PNG)

запустил стресс тест чтобы проверить работу алертов 
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/10-monitoring-03-grafana/img/03.PNG)

## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
1. В качестве решения задания приведите листинг этого файла.

файл с сохраненным дашбордом: 
https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/10-monitoring-03-grafana/img/dashboard.json
