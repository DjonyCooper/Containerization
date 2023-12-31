# Семинар 1. Механизмы пространства имен

<details><summary><h4>Задание:</h4></summary>
  
✔️ Необходимо продемонстрировать изоляцию одного и того же приложения (как решено на семинаре - командного интерпретатора) в различных пространствах имен.
  
</details>

<details><summary><h4>Формат сдачи ДЗ:</h4></summary>
  
✔️ предоставить доказательства в виде скриншота и текстового документа с введенными командами.

</details>


<h4>Решение:</h4>

• Запустим Bash в новом пространстве имен командой (так как команда требует привилегии суперпользователя, то выполняем через sudo):
```
sudo unshare -pf -n --mount-proc bash
```

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20215958.jpg?raw=true  "Выполнение sudo unshare -pf -n --mount-proc bash")

• Откроем второй терминал, где будем наглядно смотреть, в текущем случае, что проишло. Посмотрим командой:
```
ps -afx
```
• Мы видим несколько родительских процессов, из которых происходят одинаковые процессы Bash. Заметим, что PID у нового процесса 2750:

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20220118.jpg?raw=true  "Выполнение ps -afx")

• Для проверки и наглядности смотрим той же командой ps -afx в root терминале ps -afx. Здесь мы видим, что изолированная оболчка видит всего два процесса. При этом PID процессов начинается с 1.

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20220302.jpg?raw=true  "Выполнение ps -afx")

• Далее, из этого же терминала, пробуем пингануть URL: ya.ru, командой:
```
ping ya.ru
```

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20220413.jpg?raw=true  "Выполнение ping ya.ru")

• Результатом получаем ошибку, так как сеть в этом пронстранстве имен локальная.

• А теперь, ту же команду запустим из второго терминала (котоый не изолирован). Видим, что пакеты летят в обе стороны без проблем.

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20220510.jpg?raw=true  "Выполнение ping ya.ru")

• Теперь, в оба терминала отправляем команду, что бы увидеть наш хост:
```
hostname
```

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20220558.jpg?raw=true  "Выполнение hostname")

Мы видим, что в обоих терминалах хост один и тот же. Теперь в изолированном терминале выполняем команду:
```
sudo unshare -u bash
```

Команда unshare запускает программу (опционально) в новом пространстве имён. Флаг -u указывает на то, что запустить bash нужно в новом UTS пространстве имён. Обратите внимание, что наш новый процесс bash указывает на другой файл UTS, тогда как все остальные остаются прежними. Теперь мы можем изменить системный hostname из нашего нового процесса bash и это не повлияет ни на какой другой процесс в системе. Изменим наш хост в изолированном терминале:
```
hostname geekbrains
```
Как мы видим, эта команда никак не затронула основной хост системы. Можем проверить это, выполнив hostname в первом терминале и увидев, что имя хоста там не изменилось.

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_1/Screenshots/Скриншот%2009-07-2023%20220749.jpg?raw=true  "Выполнение hostname")

Все выше описанное показывает процесс запуска процессов в разных пространствах имён с возможностью изолировать определенные направления.
