# Домашнее задание к занятию 7 «Жизненный цикл ПО» - Курапов Антон

## Подготовка к выполнению

1. Получить бесплатную версию Jira - https://www.atlassian.com/ru/software/jira/work-management/free (скопируйте ссылку в адресную строку). Вы можете воспользоваться любым(в том числе бесплатным vpn сервисом) если сайт у вас недоступен. Кроме того вы можете скачать [docker образ](https://hub.docker.com/r/atlassian/jira-software/#) и запустить на своем хосте self-managed версию jira.
2. Настроить её для своей команды разработки.
3. Создать доски Kanban и Scrum.
4. [Дополнительные инструкции от разработчика Jira](https://support.atlassian.com/jira-cloud-administration/docs/import-and-export-issue-workflows/).

## Основная часть

Необходимо создать собственные workflow для двух типов задач: bug и остальные типы задач. Задачи типа bug должны проходить жизненный цикл:

1. Open -> On reproduce.
2. On reproduce -> Open, Done reproduce.
3. Done reproduce -> On fix.
4. On fix -> On reproduce, Done fix.
5. Done fix -> On test.
6. On test -> On fix, Done.
7. Done -> Closed, Open.

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/09-ci-01-intro/img/01_1.PNG)

Остальные задачи должны проходить по упрощённому workflow:

1. Open -> On develop.
2. On develop -> Open, Done develop.
3. Done develop -> On test.
4. On test -> On develop, Done.
5. Done -> Closed, Open.

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/09-ci-01-intro/img/01_2.PNG)

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/09-ci-01-intro/img/01_3.PNG)

xml-файлы лежат в директории: 
https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/09-ci-01-intro/img
