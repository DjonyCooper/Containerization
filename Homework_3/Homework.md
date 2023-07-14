# Семинар 3. Введение в Docker

<details><summary><h4>Задание:</h4></summary>
  
Задание:

✔️ Запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: https://hub.docker.com/

✔️ По желанию - заполнить БД данными через консоль

✔️ Запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны

Задание:

✔️ Создать папку, которую мы будем готовы смонтировать в контейнер

✔️ В этой папке создать файл test.txt и наполнить данными

✔️ В домашней директории создать файл test.txt, который также необходимо будет смонтировать в контейнер и наполнить совершенно другими данными

✔️ Создать контейнер из образа ubuntu:22.10

✔️ Задать ему имя

✔️ Задать hostname

✔️ Смонтировать созданную ранее папку с хоста в контейнер

✔️ Смонтировать созданный ранее текстовый файл внутрь смонтированной папки, чтобы он пересекался с созданным ранее файлом в этой папке. Просмотреть этот файл.
  
</details>

<details><summary><h4>Формат сдачи ДЗ:</h4></summary>
  
✔️ Предоставить доказательства в виде скриншота и текстового документа с введенными командами.

</details>


<h4>Решение:</h4>

• Создаем директорию /test/folder, используя редактор nano добавляем произвольный текст в файл test.txt и сохраняем его в директории: ./test/folder, используя редактор nano создаем еще один файл test.txt, но уже в корне, с другим произвольным текстом, проверяем, что директория и файл созданы, далее выделяем терминал для процесса контейнера, задаем hostname: DJC, задаем имя контейнеру: djc_test, монтируем otherway каталог в текущем каталоге в контейнер по /test/folder пути используя -v, тоже делаем с файлом в корне, использующий ubuntu:22.10, посмотрим файл и проверяем список всех контейнеров, чтобы удостовериться, что контейнер создан:
```
mkdir -p ./test/folder
nano ./test/folder/test.txt
nano ./test.txt
ls
sudo docker run -it -h DJC --name djc_test -v /test/folder:/otherway -v /root/test.txt:/otherway/test.txt ubuntu:22.10
sudo docker ps -a
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_3/Screenshot/Скриншот%2014-07-2023%20201646.jpg?raw=true  "Список команд")

```
Полезная информация:
• docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:8.0.31
• docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin

В первой команде docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:8.0.31, происходит следующее:

docker run - запускает новый контейнер на основе указанного образа.
--name some-mysql - задает имя контейнера как "some-mysql".
-e MYSQL_ROOT_PASSWORD=my-secret-pw - устанавливает переменную среды в контейнере, где MYSQL_ROOT_PASSWORD устанавливается в значение "my-secret-pw". Это используется для установки пароля для учетной записи root в MySQL.
-d - запускает контейнер в фоновом режиме (detached mode).
mysql:8.0.31 - указывает на использование образа MySQL версии 8.0.31.
Таким образом, эта команда запускает контейнер MySQL с именем "some-mysql" и устанавливает пароль для учетной записи root в MySQL.

Во второй команде docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin, происходит следующее:

docker run - запускает новый контейнер на основе указанного образа.
--name myphp - задает имя контейнера как "myphp".
-d - запускает контейнер в фоновом режиме (detached mode).
--link some-mysql:db - устанавливает связь (link) между контейнерами "some-mysql" и "myphp", где "some-mysql" будет доступен внутри контейнера "myphp" под именем "db".
-p 8081:80 - пробрасывает порт 8081 на хостовой машине на порт 80 внутри контейнера. Таким образом, при обращении к порту 8081 на хостовой машине, будет установлено соединение с контейнером по порту 80.
phpmyadmin/phpmyadmin - указывает на использование образа phpMyAdmin.
Эта команда запускает контейнер phpMyAdmin с именем "myphp", связывает его с контейнером MySQL "some-mysql" и пробрасывает порт 8081 для доступа к phpMyAdmin через веб-браузер на хостовой машине.
```

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_3/Screenshot/Скриншот%2014-07-2023%20223004.jpg?raw=true  "Создание и запуск новых контейнеров")

• Запускаем some-mysql и запускаем mysql - авторизуемся:
```
sudo docker exec -it some-mysql bash
mysql -u root -pmy-secret-pw
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_3/Screenshot/image.png?raw=true  "Запуск MySQL")

• Далее посмотрим список всех БД, создадим новую дадим ей имя djcdb, проверм, что она создана:
```
show databases;
create database djcdb;
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_3/Screenshot/Скриншот%2014-07-2023%20214023.jpg?raw=true  "Создание БД")

• Далее добавим данные в новую БД, выбираем БД, создаем новую таблицу (задаем столбцы и их типы), добавляем новую строку данных в таблицу, смотрим список таблиц в БД, отправляем пробный запрос на получение информации с БД:
```
use djcdb;
create table users (name varchar(20), age int, gender varchar(1), national varchar(20));
insert into users (name, age, gender, national) value ('Djony', '20', 'm', 'russian');
show tables;
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_3/Screenshot/Скриншот%2014-07-2023%20215724.jpg?raw=true  "Создание таблицы, добавление данных")

• Далее через веб проверяю, что все введенные данные доступны:

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_3/Screenshot/Скриншот%2014-07-2023%20221211.jpg?raw=true  "php")
