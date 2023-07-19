# Семинар 4. Dockerfile и слои

<details><summary><h4>Задание:</h4></summary>
  
Задание:

✔️ необходимо создать Dockerfile, основанный на любом образе (вы в праве выбрать самостоятельно).

✔️ В него необходимо поместить приложение, написанное на любом известном вам языке программирования (Python, Java, C, С#, C++).

✔️ При запуске контейнера должно запускаться самостоятельно написанное приложение.
  
</details>

<details><summary><h4>Формат сдачи ДЗ:</h4></summary>
  
✔️ Предоставить доказательства в виде скриншота и текстового документа с введенными командами.

</details>


<h4>Решение:</h4>

• Создаем директорию Homework_4, в нее используя редактор nano добавляем 2 файла Dockerfile и loader.py, код не сложный иммитирует полосу загрузки в консоли, после отработки цикла - программа завершает работу:
```
mkdir Homework_4
nano Dockerfile
nano loader.py
sudo docker build -t loader_doc
sudo docker run -v /home/djc/Homework_4/:/dir loader_doc python3 dir/loader.py
sudo docker ps -a
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_4/Screenshot/Скриншот%2019-07-2023%20212644.jpg  "Содержимое Dockerfile и loader.py")
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_4/Screenshot/Скриншот%2019-07-2023%20212839.jpg  "Создание образа loader_doc")
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_4/Screenshot/Скриншот%2019-07-2023%20212949.jpg  "Запуск кода из контейнера")


