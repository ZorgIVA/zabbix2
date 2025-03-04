# zabbix1

# Задание 1

Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результаты
Прикрепите в файл README.md скриншот авторизации в админке.
Приложите в файл README.md текст использованных команд в GitHub.

<img src = "img\1_1.jpg" width = 100%>

commands:

 wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb

 dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb

 apt update

 apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
 
 sudo -u postgres createuser --pwprompt zabbix
 
 sudo -u postgres createdb -O zabbix zabbix

Отредактируйте файл /etc/zabbix/zabbix_server.conf - отредактировал

 systemctl restart zabbix-server zabbix-agent apache2

 systemctl enable zabbix-server zabbix-agent apache2

Все как в лекции, правда агента сразу поставил на локалхост (с офсайта Zabbix), правда ставил на Ubunta 24.04 LTS, но разницы нет - Deb.
<<< ...su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD
'\'123456789\'';"'
и
su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"...>>> - очень удобно, спасибо!

<<<...sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf...>>> - не отработал, менял конфиг руками.

# Задание 2
Установите Zabbix Agent на два хоста.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.
Требования к результаты
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
Приложите в файл README.md текст использованных команд в GitHub

<img src = "img\2_1.jpg" width = 100%>

<img src = "img\2_2.jpg" width = 100%>

<img src = "img\2_3.jpg" width = 100%>

commands:

агент был установлен ранее на локалхост, на вторую машину:

wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb

dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb

apt update

apt install zabbix-agent

systemctl restart zabbix-agent

systemctl enable zabbix-agent

потом открыт 10050/tcp

в конфиге агента второй машины прописан ip в параметре ServerActive - все заиграло.

Извините за вольности)