# Домашнее задание к занятию 1 «Введение в Ansible» - Курапов Антон


## Основная часть

1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте значение, которое имеет факт `some_fact` для указанного хоста при выполнении playbook.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/01_0.PNG)
2. Найдите файл с переменными (group_vars), в котором задаётся найденное в первом пункте значение, и поменяйте его на `all default fact`.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/02_0.PNG)
3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.
4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/03_0.PNG)
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/04_0.PNG)
5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились значения: для `deb` — `deb default fact`, для `el` — `el default fact`.
6.  Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/05_0.PNG)
7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/06_0.PNG)
8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/07_0.PNG)
9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/08_0.PNG)
ansible.builtin.local - должен подойти 
10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.
11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь, что факты `some_fact` для каждого из хостов определены из верных `group_vars`.
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-01-base/png/09_0.PNG)
12. Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.
13. Предоставьте скриншоты результатов запуска команд.
