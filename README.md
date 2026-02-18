# Домашнее задание к занятию «Система мониторинга Zabbix» - `Викторов Михаил`
### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

#### Требования к результатам 
1. Прикрепите в файл README.md скриншот авторизации в админке.
2. Приложите в файл README.md текст использованных команд в GitHub.

---

### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

#### Требования к результатам
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

## Решение
### Задание 1 
```
 - sudo apt install -y postgresql postgresql-contrib
 - sudo systemctl enable postgresql
 - wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu24.04_all.deb
 - sudo dpkg -i zabbix-release_latest_7.4+ubuntu24.04_all.deb
 - sudo apt update
 - sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
 - sudo -u postgres createuser --pwprompt zabbix
 - sudo -u postgres createdb -O zabbix zabbix
 - zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
 - sudo nano /etc/zabbix/zabbix_server.conf (add DBPassword=zabbix)
 - sudo systemctl restart zabbix-server zabbix-agent apache2
 - sudo systemctl enable zabbix-server zabbix-agent apache2
```

Авторизуемся в кабинете Zabbix:

![Авторизация](https://github.com/starikam/8-03-hw/blob/main/img/2026-02-18_15-21-54.png?raw=true)

### Задание 2 

# Подключаем хосты:
```
 - wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu24.04_all.deb
 - sudo dpkg -i zabbix-release_latest_7.4+ubuntu24.04_all.deb
 - sudo apt update
 - sudo apt install zabbix-agent -y
 - sudo nano /etc/zabbix/zabbix_agentd.conf
 - sudo systemctl start zabbix-agent
 - sudo systemctl enable zabbix-agent
 - sudo systemctl status zabbix-agent
```

![Хосты](https://github.com/starikam/8-03-hw/blob/main/img/2026-02-18_15-49-40.png?raw=true)

# Лог агента:
![Агент](https://github.com/starikam/8-03-hw/blob/main/img/2026-02-18_15-54-15.png?raw=true)

# Разделы Мониторинга:

![Агент 1](https://github.com/starikam/8-03-hw/blob/main/img/2026-02-18_15-50-34.png?raw=true)

![Агент 2](https://github.com/starikam/8-03-hw/blob/main/img/2026-02-18_15-50-46.png?raw=true)
