# Containerization - площадка GeekBrains (Homework)

<summary>Цели на репозиторий:</summary>
<p>

✔️ Выполнить домашнюю работу 1 семинара
  
✔️ Выполнить домашнюю работу 2 семинара

✔️ Выполнить домашнюю работу 3 семинара

✔️ Выполнить домашнюю работу 4 семинара

✕ Выполнить домашнюю работу 5 семинара

</p>

<br>
<br>
↓ Домашние работы по семинарам с заданиями:

<details><summary><h4>Семинар 1. Механизмы пространства имен.</h4></summary>

✔️ Необходимо продемонстрировать изоляцию одного и того же приложения (как решено на семинаре - командного интерпретатора) в различных пространствах имен.

</details>
<details><summary><h4>Семинар 2. Механизмы контрольных групп.</h4></summary>

✔️ Запустить контейнер с ubuntu, используя механизм LXC

✔️ Ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает

✔️ добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно

''при создании указать файл, куда записывать логи

''после перезагрузки проанализировать логи

</details>
<details><summary><h4>Семинар 3. Введение в Docker</h4></summary>

✔️ Запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: https://hub.docker.com/

✔️ По желанию - заполнить БД данными через консоль

✔️ Запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны

✔️ Создать папку, которую мы будем готовы смонтировать в контейнер

✔️ В этой папке создать файл test.txt и наполнить данными

✔️ В домашней директории создать файл test.txt, который также необходимо будет смонтировать в контейнер и наполнить совершенно другими данными

✔️ Создать контейнер из образа ubuntu:22.10

✔️ Задать ему имя

✔️ Задать hostname

✔️ Смонтировать созданную ранее папку с хоста в контейнер

✔️ Смонтировать созданный ранее текстовый файл внутрь смонтированной папки, чтобы он пересекался с созданным ранее файлом в этой папке. Просмотреть этот файл.

</details>
<details><summary><h4>Семинар 4. Dockerfile и слои.</h4></summary>

✔️ Необходимо создать Dockerfile, основанный на любом образе (вы в праве выбрать самостоятельно).

✔️ В него необходимо поместить приложение, написанное на любом известном вам языке программирования (Python, Java, C, С#, C++).

✔️ При запуске контейнера должно запускаться самостоятельно написанное приложение.

</details>
