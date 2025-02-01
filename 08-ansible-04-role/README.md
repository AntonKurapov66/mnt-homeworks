# Домашнее задание к занятию 4 «Работа с roles» - Курапов Антон

## Подготовка к выполнению

1. * Необязательно. Познакомьтесь с [LightHouse](https://youtu.be/ymlrNlaHzIY?t=929).
2. Создайте два пустых публичных репозитория в любом своём проекте: vector-role и lighthouse-role.
3. Добавьте публичную часть своего ключа к своему профилю на GitHub.

## Основная часть

Ваша цель — разбить ваш playbook на отдельные roles. 

Задача — сделать roles для ClickHouse, Vector и LightHouse и написать playbook для использования этих ролей. 

Ожидаемый результат — существуют три ваших репозитория: два с roles и один с playbook.

**Что нужно сделать**

1. Создайте в старой версии playbook файл `requirements.yml` и заполните его содержимым:

   ```yaml
   ---
     - src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
       scm: git
       version: "1.13"
       name: clickhouse 
   ```

2. При помощи `ansible-galaxy` скачайте себе эту роль.
3. Создайте новый каталог с ролью при помощи `ansible-galaxy role init vector-role`.
4. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 
5. Перенести нужные шаблоны конфигов в `templates`.
6. Опишите в `README.md` обе роли и их параметры. Пример качественной документации ansible role [по ссылке](https://github.com/cloudalchemy/ansible-prometheus).
7. Повторите шаги 3–6 для LightHouse. Помните, что одна роль должна настраивать один продукт.
8. Выложите все roles в репозитории. Проставьте теги, используя семантическую нумерацию. Добавьте roles в `requirements.yml` в playbook.
9. Переработайте playbook на использование roles. Не забудьте про зависимости LightHouse и возможности совмещения `roles` с `tasks`.
10. Выложите playbook в репозиторий.
11. В ответе дайте ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.

---

### Решение

добавил роли в репозиторий 

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-04-role/img/01.PNG)

раскидал по ролям все таски 

в плей-файле оставил только вызов ролей и запуск nginx 
```yaml
---
- name: Install clickhouse
  hosts: clickhouse
  roles:
    - role: clickhouse-role

- name: Install vector
  hosts: vector
  roles:
    - role: vector-role

- name: Install lighthouse
  hosts: lighthouse

  handlers:
    - name: Start nginx service
      become: true
      ansible.builtin.service:
        name: nginx
        state: restarted
  pre_tasks:
    - name: Install Nginx on Fedora
      dnf:
        name: nginx
        state: present
      notify: Start nginx service

    - name: Create Nginx config
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        mode: 0644
      notify: Start nginx service

    - name: Check nginx configuration
      command: nginx -t
      register: nginx_test
      failed_when: nginx_test.rc != 0
      changed_when: false

  roles:
    - role: lighthouse-role

  post_tasks:
    - name: Show connect URL lighthouse
      debug:
        msg: "http://{{ ansible_host }}/#http://{{ hostvars['clickhouse-01'].ansible_host }}:8123/?user={{ clickhouse_user }}"
```

Запуск и выполнение тасок : 
![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-04-role/img/01_0.PNG)

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-04-role/img/01_1.PNG)

![alt text](https://github.com/AntonKurapov66/mnt-homeworks/blob/MNT-video/08-ansible-04-role/img/01_2.PNG)

[Vector](https://github.com/AntonKurapov66/mnt-homeworks/tree/MNT-video/08-ansible-04-role/vector-role)

[Lighthouse](https://github.com/AntonKurapov66/mnt-homeworks/tree/MNT-video/08-ansible-04-role/lighthouse-role)

[Clickhouse](https://github.com/AntonKurapov66/mnt-homeworks/tree/MNT-video/08-ansible-04-role/clickhouse-role)

---
