# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Моторин Алексей`

---

### Задание 1
Установите Zabbix Server с веб-интерфейсом.

1. Cкриншот авторизации в админке и стартовый дашбоард Zabbix.

Скриншот-1.1 к заданию 1 (Cкриншот авторизации в админке):
![Скриншот-1.1](img/2025-11-27_00-00-41.png)

Скриншот-1.2 к заданию 1 (Стартовый дашбоард Zabbix):
![Скриншот-1.2](img/2025-11-27_16-39-03.png)

2. Текст использованных команд и конфигурация Zabix Server.

[Конфигурация: Zabbix 7.4 (Server, Frontend, Agent), Debian 13 Trixie, PostgreSQL 17.6, Apache 2](https://www.zabbix.com/ru/download?zabbix=7.4&os_distribution=debian&os_version=13&components=server_frontend_agent&db=pgsql&ws=apache)

`Установка Zabbix 7.4 (Server, Frontend, Agent) под root Debian 13`

```bash
# 1. Установка PostgreSQL
apt install postgresql

# 2. Настроить аутентификацию в PostgreSQL
nano /etc/postgresql/*/main/pg_hba.conf
# Меняем опцию на md5
# TYPE  DATABASE        USER            ADDRESS                 METHOD
# local   all             all                                     md5

# 3. Перезапуск PostgreSQL
systemctl reload postgresql

# 4. Установка репозитория Zabbix
wget https://repo.zabbix.com/zabbix/7.4/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.4+debian13_all.deb
dpkg -i zabbix-release_latest_7.4+debian13_all.deb
apt update

# 5. Установка Zabbix сервера, веб-интерфейса и агента
apt install zabbix-server-pgsql zabbix-frontend-php php8.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
 
# 6. Задаём пользователя и БД через интерактивную сессию postgres
su - postgres
createuser --pwprompt zabbix
createdb -O zabbix zabbix
exit

# 7. Импорт начальной схемы и данных
zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | psql -U zabbix -W zabbix

# 8. Настройка конфига Zabbix
nano /etc/zabbix/zabbix_server.conf
# DBPassword=zabbix

# 9. Запускаем процессы Zabbix сервера и агента, настраиваем их запуск при загрузке ОС.
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2

# 10. Открываем Zabbix UI web интерфейс и следуем подсказкам мастера установки, завершаем установку.
```
`Команды Git (PowerShell)`

```powershell
# Перейти в нужный каталог
cd E:\

# Создать папку 005, если её нет
New-Item -ItemType Directory -Path "E:\005" -Force

# Клонируем репозиторий
git clone https://github.com/presdes/8-04-hw.git

# Переходим в каталог с репозиторием
cd E:\005\8-04-hw

# Проверяем статус репозитория
git status

# Производим изменения в файлах
# ...

# Добавляем изменения в индекс
git add .

# Создаём коммит
git commit -m "h/w zabbix ч.1, версия 5 (задание 1)"

# Отправляем изменения на удалённый репозиторий
git push origin main
```

---

### Задание 2
Установите Zabbix Agent на два хоста.

1. Cкриншот  раздела Configuration > Hosts, где видно, что агенты подключены к серверу.

Скриншот-2.1 к заданию 2:
![Скриншот-2.1](img/2025-11-27_14-59-08.png)

2. Cкриншот лога zabbix agent (windows).

Скриншот-2.2 к заданию 2:
![Скриншот-2.2](img/2025-11-27_15-52-56.png)

3. Cкриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.

Скриншот-2.3 к заданию 2 (Загрузка ЦПУ наших агентов):
![Скриншот-2.3](img/2025-11-27_16-12-23.png)

Скриншот-2.4 к заданию 2: (Поступающие данные от агентов)
![Скриншот-2.4](2025-11-27_15-07-59.png)

4. Текст использованных команд в GitHub.
```powershell
# Переходим в каталог с репозиторием
cd E:\005\8-04-hw

# Проверяем статус репозитория
git status

# Производим необходимые изменения в файлах
# ...

# Добавляем изменения в индекс
git add .

# Создаём коммит
git commit -m "h/w zabbix ч.1, версия 6 (задание 2)"

# Отправляем изменения на удалённый репозиторий
git push origin main
```

---

### Задание 3
Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

1. Cкриншот раздела Latest Data, где видно свободное место на диске C:

Скриншот-3.1 к заданию 23:
![Скриншот-3.1](img/2025-11-27_15-49-39.png)
