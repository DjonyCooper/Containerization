 # Семинар 5. Docker Compose и Docker Swarm

<details><summary><h4>Задание:</h4></summary>
  
Задание:

✔️ Создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД (compose)

✕  Необходимо создать 3 сервиса в каждом окружении (dev, prod, lab) (**не обязательно**)

✕  По итогу на каждой ноде должно быть по 2 работающих контейнера (**не обязательно**)

✔️ Выводы зафиксировать
  
</details>

<details><summary><h4>Формат сдачи ДЗ:</h4></summary>
  
✔️ Предоставить доказательства в виде скриншота и текстового документа с введенными командами.

</details>


<h4>Решение:</h4>

• Создаем директорию compose, в нее используя редактор nano добавляем файл compose.yaml:
```
mkdir compose
cd compose/
nano compose.yaml
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_5/Screenshot/Скриншот%2022-07-2023%20124715.jpg?raw=true  "mkdir compose")

!Справка, содержимое файла compose.yaml (добавляем для запуска 2 сервиса, DB и phpmyadmin, оба latest версии, задаем параметры для DB и phpmyadmin, устанавливаем для phpmyadmin зависимость (depends_on):
```
version: '3.9'

services:
  db:
    image: mysql:latest
    environment:
      MYSQL_USERNAME: root
      MYSQL_ROOT_PASSWORD: 12345
      MYSQL_DATABASE: djc_db
  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    restart: always
    ports:
      - 8080:80
    depends_on:
      - db
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_5/Screenshot/Скриншот%2022-07-2023%20135401.jpg?raw=true  "compose.yaml")

• Запускаем .yaml файл - проверяем работу: 
```
sudo docker-compose up
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_5/Screenshot/Скриншот%2022-07-2023%20125209.jpg?raw=true  "sudo docker-compose up")
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_5/Screenshot/Скриншот%2022-07-2023%20130902.jpg?raw=true  "phpmyadmin")
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_5/Screenshot/Скриншот%2022-07-2023%20135324.jpg?raw=true  "phpmyadmin")
