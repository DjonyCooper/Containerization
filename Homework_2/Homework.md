# Семинар 2. Механизмы контрольных групп

<details><summary><h4>Задание:</h4></summary>
  
✔️ Запустить контейнер с ubuntu, используя механизм LXC

✔️ Ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает

✔️ добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно

''при создании указать файл, куда записывать логи

''после перезагрузки проанализировать логи
  
</details>

<details><summary><h4>Формат сдачи ДЗ:</h4></summary>
  
✔️ Предоставить доказательства в виде скриншота и текстового документа с введенными командами.

</details>


<h4>Решение:</h4>

• Проинсталлируем LXC и необходимые пакеты:
```
sudo apt install lxc lxc-templates uidmap
```
• Проверяем версию lxc:
```
lxc version
```
• Получаем ошибку и сообщение, о необходимости инициализации - делаем:
```
lxd init
```
• После инициализации, проверка версии отрабатывает корректно:

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20211553.jpg?raw=true  "lxd init")

• Далее создаем новый контейнер с именем djc_test (из под рута):
```
lxc-create -n djc_test -t ubuntu
```

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221126.jpg?raw=true  "Выполнение lxc-create -n djc_test -t ubuntu")
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221217.jpg?raw=true  "Контейнер создан!")

• Видим, что контейнер создан, со стандартными уч. данными. login: ubuntu, secret: ubuntu

• Запускаем созданный контейнер:
```
sudo lxc-start -d -n djc_test
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221400.jpg?raw=true  "Выполнение sudo lxc-start -d -n djc_test")

• После ввода команды - ошибок и доп. сообщений нет, значит команда успешно выполнена. Проверим:
```
sudo lxc-attach -n djc_test
```
• Отлично, вход в контейнер выполнен успешно:

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221457.jpg?raw=true  "Выполнение sudo lxc-attach -n djc_test")

• Посмотрим данные по памяти:
```
free -m
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221545.jpg?raw=true  "Выполнение free -m")

• Считываем данные об ограничении памяти из файла memory.max в директориях sys/fs/cgroup/ и sys/fs/cgroup/.lxc/ :
```
cat sys/fs/cgroup/memory.max
cat sys/fs/cgroup/.lxc/memory.max
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221729.jpg?raw=true  "Ограничения памяти")

• Мы видим, что ограничение памяти в обоих случаях установлено на максимальное значение. Выходим.

• Для того, что бы ограничить потребление памяти контейнером, необходимо добавить данные в файл конфигурации. Для начала убедимся, что ограничений нет:
```
sudo cat /var/lib/lxc/djc_test/config
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20221931.jpg?raw=true  "Выполнение sudo cat /var/lib/lxc/djc_test/config")

• Добавим строку: lxc.cgroup2.memory.max = 256M в файл конфигурации:

![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20222202.jpg?raw=true  "Добавление строки lxc.cgroup2.memory.max")

• Мы ограничили потребление памяти, установив значение: 256 мб. Останавливаем контейнер и повторно запускаем его. Проверяем, что ограничение работает:
```
sudo lxc-stop -k -n djc_test
sudo lxc-start -d -n djc_test
sudo cat /sys/fs/cgroup/lxc.payload.djc_test/mempry.max
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20224230.jpg?raw=true  "sudo cat /sys/fs/cgroup/lxc.payload.djc_test/mempry.max")

• Отлично! Система пересчитала и выдала результат примерно равный 256М

• Как мы видим, после ввода команды: sudo lxc-ls -f, контейнер djc_test запущен и в автозапуске стоит 0 (что означает, что автозапуск контейнера отключен). Нам необходимо включить автозапуск, для этого вносим правки в файл конфигурации:
```
sudo nano /var/lib/lxc/djc_test/config
```
• Добавляем строку: lxc.start.auto = 1, меняющую параметр автозапуска на 1 (включено)

• Перезагружаемся. Далее посмотрим список запущенных контейнеров и проверим значение автозапуска у контейнера djc_test:
```
sudo lxc-ls -f
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20225033.jpg?raw=true  "sudo lxc-ls -f")
• Как видим - автозапуск работает.

• Для логирования, при запуске контейнера в параметрах можно указать, где хранить логи:
```
lxc-start -n djc_test --logfile log.log
```
• Чтобы удалить контейнер (*для удаления он должен быть выключен!) необходмио воспользоваться следующей командой:
```
sudo lxc-destroy -n djc_test
```
![Изображение](https://github.com/DjonyCooper/Containerization/blob/main/Homework_2/Screenshots/Скриншот%2011-07-2023%20225237.jpg?raw=true "sudo lxc-destroy -n djc_test")
