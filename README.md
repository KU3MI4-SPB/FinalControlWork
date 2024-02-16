# Итоговая контрольная работа

## Задание 

### Операционные системы и виртуализация (Linux)

**1. Использование команды cat в Linux**
   - Создать два текстовых файла: "Pets"(Домашние животные) и "Pack animals"(вьючные животные), используя команду `cat` в терминале Linux. В первом файле перечислить собак, кошек и хомяков. Во втором — лошадей, верблюдов и ослов.
   - Объединить содержимое этих двух файлов в один и просмотреть его содержимое.
   - Переименовать получившийся файл в "Human Friends"(.
Пример конечного вывода после команды “ls” :
Desktop Documents Downloads  HumanFriends.txt  Music  PackAnimals.txt  Pets.txt  Pictures  Videos

```shell
sudo su
apt update
mkdir GB
cd GB/
mkdir FinalControlWork
cd FinalControlWork/
cat > Pets.txt
Dogs
Cats
Hamsters
cat > PackAnimals.txt
Horses
Camels
Donkeys
cat Pets.txt PackAnimals.txt > HumanFriends.txt
cat HumanFriends.txt
ls
```

**2. Работа с директориями в Linux**
   - Создать новую директорию и переместить туда файл "Human Friends".

```shell
mkdir HumanFriends
mv HumanFriends.txt HumanFriends/
cd HumanFriends/
ls
```

**3. Работа с MySQL в Linux. “Установить MySQL на вашу вычислительную машину”**
   - Подключить дополнительный репозиторий MySQL и установить один из пакетов из этого репозитория.

```shell
cd ~
wget https://dev.mysql.com/get/mysql-apt-config_0.8.29-1_all.deb
dpkg -i mysql-apt-config_0.8.29-1_all.deb 
apt update
```

**4. Управление deb-пакетами**
   - Установить и затем удалить deb-пакет, используя команду `dpkg`.

```shell
apt update
apt install mysql-server
wget https://github.com/atom/atom/releases/download/v1.60.0/atom-amd64.deb
dpkg -i atom-amd64.deb
dpkg -r atom
```

**5. История команд в терминале Ubuntu**
   - Сохранить и выложить историю ваших терминальных команд в Ubuntu.
В формате: Файла с ФИО, датой сдачи, номером группы(или потока)

Объектно-ориентированное программирование 

**6. Диаграмма классов**
   - Создать диаграмму классов с родительским классом "Животные", и двумя подклассами: "Pets" и "Pack animals".
В составы классов которых в случае Pets войдут классы: собаки, кошки, хомяки, а в класс Pack animals войдут: Лошади, верблюды и ослы).
Каждый тип животных будет характеризоваться (например, имена, даты рождения, выполняемые команды и т.д)
Диаграмму можно нарисовать в любом редакторе, такими как Lucidchart, Draw.io, Microsoft Visio и других.

![diagram] (https://github.com/KU3MI4-SPB/FinalControlWork/blob/master/diagram.jpg)

**7. Работа с MySQL**

7.1. После создания диаграммы классов в 6 пункте, в 7 пункте база данных "Human Friends" должна быть структурирована в соответствии с этой диаграммой. Например, можно создать таблицы, которые будут соответствовать классам "Pets" и "Pack animals", и в этих таблицах будут поля, которые характеризуют каждый тип животных (например, имена, даты рождения, выполняемые команды и т.д.). 

7.2   - В ранее подключенном MySQL создать базу данных с названием "Human Friends".
```sql
CREATE DATABASE human_friends;
```

   - Создать таблицы, соответствующие иерархии из вашей диаграммы классов.
```sql
USE human_friends;


CREATE TABLE animal_class (ID int AUTO_INCREMENT PRIMARY KEY,
                                                         class_name varchar(20));


INSERT INTO animal_class (class_name)
VALUES ('вьючные'),
       ('домашние');


CREATE TABLE animal_pack
  (ID INT AUTO_INCREMENT PRIMARY KEY,
                                 genus varchar(20),
                                       id_class INT,
   FOREIGN KEY (id_class) REFERENCES animal_class (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO animal_pack (genus, id_class)
VALUES ('лошади', 1),
       ('ослы', 1),
       ('Верблюды', 1);


CREATE TABLE home_animals
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 genus varchar(20),
                                       id_class INT,
   FOREIGN KEY (id_class) REFERENCES animal_class (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO home_animals (genus, id_class)
VALUES ('кошки', 2),
       ('собаки', 2),
       ('хомяки', 2);
```
   - Заполнить таблицы данными о животных, их командах и датами рождения.
```sql
CREATE TABLE cats
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 name varchar(20),
                                      birthday date, commands varchar(30),
                                                              genus int,
   FOREIGN KEY (genus) REFERENCES home_animals (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO cats (name, birthday, commands, genus)
VALUES ('Вася', '2021-01-01', 'лапу', 1),
       ('Барсик', '2019-01-01', "ко мне", 1),
       ('Томас', '2014-01-01', "", 1);


CREATE TABLE dogs
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 name varchar(20),
                                      birthday date, commands varchar(30),
                                                              genus int,
   FOREIGN KEY (genus) REFERENCES home_animals (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO dogs (name, birthday, commands, genus)
VALUES ('Барбос', '2023-01-01', 'ко мне, сидеть, голос', 2),
       ('Граф', '2022-06-05', "лапу, голос", 2),
       ('Шарик', '2021-02-01', "фу, место, сидеть, след", 2),
       ('Белка', '2020-03-10', "след, фас, фу, место", 2);


CREATE TABLE hamsters
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 name varchar(20),
                                      birthday date, commands varchar(30),
                                                              genus int,
   FOREIGN KEY (genus) REFERENCES home_animals (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO hamsters (name, birthday, commands, genus)
VALUES ('Сардж', '2023-04-01', '', 3),
       ('Кореш', '2022-05-01', '', 3),
       ('Черныщ', '2021-06-01', NULL, 3);


CREATE TABLE horses
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 name varchar(20),
                                      birthday date, commands varchar(30),
                                                              genus int,
   FOREIGN KEY (genus) REFERENCES home_animals (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO horses (name, birthday, commands, genus)
VALUES ('Гром', '2022-07-01', 'бегом, шагом', 1),
       ('Закат', '2021-07-01', "бегом, шагом, хоп", 1),
       ('Байкал', '2020-08-02', "бегом, шагом, хоп, брр", 1),
       ('Спирит', '2019-09-01', "бегом, шагом, хоп", 1);


CREATE TABLE donkeys
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 name varchar(20),
                                      birthday date, commands varchar(30),
                                                              genus int,
   FOREIGN KEY (genus) REFERENCES home_animals (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO donkeys (name, birthday, commands, genus)
VALUES ('Первый', '2023-10-01', "ко мне", 2),
       ('Второй', '2022-11-01', "", 2),
       ('Третий', '2021-12-01', "", 2),
       ('Четвертый', '2020-01-10', NULL, 2);


CREATE TABLE camels
  (ID int AUTO_INCREMENT PRIMARY KEY,
                                 name varchar(20),
                                      birthday date, commands varchar(30),
                                                              genus int,
   FOREIGN KEY (genus) REFERENCES home_animals (ID) ON DELETE CASCADE ON UPDATE CASCADE);


INSERT INTO camels (name, birthday, commands, genus)
VALUES ('Горбатая', '2023-10-01', 'вернись', 3),
       ('Гора', '2019-03-12', "остановись", 3),
       ('Борода', '2022-12-10', "улыбнись", 3);


SELECT *
FROM home_animals;
```
   - Удалить записи о верблюдах и объединить таблицы лошадей и ослов.
```sql
TRUNCATE TABLE camels;


SELECT name,
       birthday,
       commands
FROM horses
UNION
SELECT name,
       birthday,
       commands
FROM donkeys;
```
   - Создать новую таблицу для животных в возрасте от 1 до 3 лет и вычислить их возраст с точностью до месяца.
```sql
CREATE
TEMPORARY TABLE animals AS
SELECT *,
       'Лошади' AS genus_animal
FROM horses
UNION
SELECT *,
       'Ослы' AS genus_animal
FROM donkeys
UNION
SELECT *,
       'Собаки' AS genus_animal
FROM dogs
UNION
SELECT *,
       'Кошки' AS genus_animal
FROM cats
UNION
SELECT *,
       'Хомяки' AS genus_animal
FROM hamsters;


CREATE TABLE yang_animal AS
SELECT name,
       birthday,
       commands,
       genus,
       timestampdiff(MONTH, birthday, CURDATE()) AS age_in_month
FROM animals
WHERE birthday BETWEEN ADDDATE(curdate(), interval -3 YEAR) AND ADDDATE(CURDATE(), interval -1 YEAR);


SELECT *
FROM yang_animal;
```
   - Объединить все созданные таблицы в одну, сохраняя информацию о принадлежности к исходным таблицам.

```sql
SELECT h.name,
       h.birthday,
       h.commands,
       pa.genus,
       ya.age_in_month
FROM horses h
LEFT JOIN yang_animal ya ON ya.name = h.name
LEFT JOIN animal_pack pa ON pa.ID = h.genus
UNION
SELECT d.name,
       d.birthday,
       d.commands,
       pa.genus,
       ya.age_in_month
FROM donkeys d
LEFT JOIN yang_animal ya ON ya.name = d.name
LEFT JOIN animal_pack pa ON pa.ID = d.genus
UNION
SELECT c.name,
       c.birthday,
       c.commands,
       ha.genus,
       ya.age_in_month
FROM cats c
LEFT JOIN yang_animal ya ON ya.name = c.name
LEFT JOIN home_animals ha ON ha.ID = c.genus
UNION
SELECT d.name,
       d.birthday,
       d.commands,
       ha.genus,
       ya.age_in_month
FROM dogs d
LEFT JOIN yang_animal ya ON ya.name = d.name
LEFT JOIN home_animals ha ON ha.ID = d.genus
UNION
SELECT hm.Name,
       hm.birthday,
       hm.commands,
       ha.genus,
       ya.age_in_month
FROM hamsters hm
LEFT JOIN yang_animal ya ON ya.name = hm.name
LEFT JOIN home_animals ha ON ha.ID = hm.genus;
```


**8. ООП и Java**
   - Создать иерархию классов в Java, который будет повторять диаграмму классов созданную в задаче 6(Диаграмма классов).

## [РЕШЕНИЕ] (https://github.com/KU3MI4-SPB/FinalControlWork/tree/master/App/Model)

**9. Программа-реестр домашних животных**
    - Написать программу на Java, которая будет имитировать реестр домашних животных. 


![program_work](https://github.com/KU3MI4-SPB/FinalControlWork/assets/129791531/37cf5de0-bb56-42e9-aee7-b74f5934ae8a)

## [ПРОГРАММА] (https://github.com/KU3MI4-SPB/FinalControlWork/tree/master/App)