## Информация о проекте
Необходимо организовать систему учета для питомника, в котором живут
домашние и вьючные животные.

## Задание
1. Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).

![Task 1]([https://user-images.githubusercontent.com/99810114/221401192-b1a5c5aa-d2e2-4531-8341-3b951ee9a5be.jpg](https://github.com/MC-DeniSka/itogwork/blob/main/screenshots/1.png))

2. Создать директорию, переместить файл туда.

![Task 2]([https://user-images.githubusercontent.com/99810114/221401198-5f035f3b-dabb-425a-ae4a-b273822b26bc.jpg](https://github.com/MC-DeniSka/itogwork/blob/main/screenshots/2.png))

3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория.

![Task 3]([https://user-images.githubusercontent.com/99810114/221401204-319e6e99-7b30-4da1-a0ca-db5d821146c8.jpg])

##4. Установить и удалить deb-пакет с помощью dpkg.

![Task 4](https://github.com/MC-DeniSka/itogwork/blob/main/screenshots/4.png)

5. Выложить [историю команд](https://github.com/MC-DeniSka/itogwork/blob/main/HistoryCommand.md) в терминале ubuntu
6. Нарисовать [диаграмму](https://github.com/MC-DeniSka/itogwork/blob/main/diagram.png), в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).

![UML](https://user-images.githubusercontent.com/99810114/221403005-bfe39717-2d41-431d-bc03-f78a1aeb76df.jpg)

7. В подключенном MySQL репозитории создать базу данных “Друзья
человека”
```sql
create database human_friends;

```
8. Создать таблицы с иерархией из диаграммы в БД
```sql
use human_friends;

create table animals
(
    id int auto_increment primary key,
    class_name varchar(30)
);

create table pack_animals
(
    id int auto_increment primary key,
    genus_name varchar(30),
    class_id int,
    foreign key (class_id) references animals (id) on delete cascade on update cascade
);

create table pets
(
    id int auto_increment primary key,
    genus_name varchar(30),
    class_id int,
    foreign key (class_id) references animals (id) on delete cascade on update cascade
);

create table dogs
(
    id int auto_increment primary key,
    name varchar(30),
    birthday date,
    breed varchar(30),
    color varchar(30),
    commands varchar(30),
    genus_id int,
    foreign key (genus_id) references pets (id) on delete cascade on update cascade 
);

create table cats
(
    id int auto_increment primary key,
    name varchar(30),
    birthday date,
    breed varchar(30),
    color varchar(30),
    commands varchar(30),
    genus_id int,
    foreign key (genus_id) references pets (id) on delete cascade on update cascade 
);

create table hamsters
(
    id int auto_increment primary key,
    name varchar(30),
    birthday date,
    breed varchar(30),
    color varchar(30),
    commands varchar(30),
    genus_id int,
    foreign key (genus_id) references pets (id) on delete cascade on update cascade 
);

create table horses
(
    id int auto_increment primary key,
    name varchar(30),
    birthday date,
    breed varchar(30),
    color varchar(30),
    commands varchar(30),
    genus_id int,
    foreign key (genus_id) references pack_animals (id) on delete cascade on update cascade 
);

create table camels
(
    id int auto_increment primary key,
    name varchar(30),
    birthday date,
    breed varchar(30),
    color varchar(30),
    commands varchar(30),
    genus_id int,
    foreign key (genus_id) references pack_animals (id) on delete cascade on update cascade 
);

create table donkeys
(
    id int auto_increment primary key,
    name varchar(30),
    birthday date,
    breed varchar(30),
    color varchar(30),
    commands varchar(30),
    genus_id int,
    foreign key (genus_id) references pack_animals (id) on delete cascade on update cascade 
);
```
9. Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения
```sql
insert into animals (class_name)
values ('Вьючные'),('Домашние');

insert into pack_animals (genus_name,class_id)
values ('Лошади',1),('Верблюды',1),('Ослы',1);

insert into pets (genus_name,class_id)
values ('Собаки',2),('Кошки',2),('Хомяки',2);

insert into dogs (name,birthday,commands,genus_id,breed,color)
values ('Бобик','2020-05-10','сидеть,лежать,голос',1,'Тибетский мастиф','коричневый'),
      ('Тузик','2017-09-01','голос',1,'Самоедская','белый'),
      ('Мухтар','2010-02-11','сидеть,лежать,голос,взять',1,'Немецкая овчарка','Коричнево-черный'),
      ('Граф','2023-02-03','',1,'Немецкий Дог','черный');

insert into cats (name,birthday,commands,genus_id,breed,color)
values ('Гарфилд','2011-08-12','кушать',2,'Мейн-кун','рыжий'),
      ('Борис','2012-01-05','ко мне',2,'Метис','серый'),
      ('Гром','2019-04-09','сидеть,лежать',2,'Анатолийский кот','рыже-белый'),
      ('Гав','2024-10-10','',2,'Метис','коричневый');

insert into hamsters (name,birthday,commands,genus_id,breed,color)
values ('Элвин','2022-08-12','газы',3,'сирийский','рыжий'),
      ('Саймон','2022-01-05','газы',3,'джунгарский','рыжий'),
      ('Теодор','2023-04-09','Противник с тыла',3,'китайский','рыжий');

insert into horses (name,birthday,commands,genus_id,breed,color)
values ('Пенелопа','2017-03-02','но,прррр,шагом',1,'','Черный'),
      ('Молния','2016-07-11','но,прррр,шагом',1,'','Камуфляж (пустынный)');

insert into camels (name,birthday,commands,genus_id,breed,color)
values ('Вася','2014-08-12','',2,'одногорбый','серый'),
      ('Игорь','2019-01-05','',2,'двугорбый','белый');

insert into donkeys (name,birthday,commands,genus_id,breed,color)
values ('Осел','2019-11-02','',3,'','коричнивый'),
      ('Моисей','2022-06-06','',3,'','темно-серый');
```
10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой
питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
```sql
SET SQL_SAFE_UPDATES = 0;
DELETE FROM camels;

select name,birthday,commands from horses
union select name,birthday,commands from donkeys;
```
11. Создать новую таблицу “молодые животные” в которую попадут все
животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью
до месяца подсчитать возраст животных в новой таблице
```sql
create temporary table animals as
select *,'Лошади' as genus from horses
union select *,'Ослы' as genus from donkeys
union select *,'Собаки' as genus from dogs
union select *,'Кошки' as genus from cats
union select *,'Хомяки' as genus from hamsters;

create table young_animals as 
select name,birthday,commands,genus,breed,color,timestampdiff(month,birthday,curdate()) as age_in_months
from animals where birthday between adddate(curdate(),interval -3 year) and adddate(curdate(),interval -1 year);
```
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на
прошлую принадлежность к старым таблицам.
```sql
SELECT h.name, h.birthday, h.commands, pa.genus_name, ya.age_in_months
FROM horses h
LEFT JOIN young_animals ya ON ya.Name = h.Name
LEFT JOIN pack_animals pa ON pa.id = h.Genus_id
UNION 
SELECT d.name, d.birthday, d.commands, pa.genus_name, ya.age_in_months
FROM donkeys d 
LEFT JOIN young_animals ya ON ya.name = d.name
LEFT JOIN pack_animals pa ON pa.id = d.genus_id
UNION
SELECT c.name, c.birthday, c.commands, ha.genus_name, ya.age_in_months
FROM cats c
LEFT JOIN young_animals ya ON ya.name = c.name
LEFT JOIN pets ha ON ha.id = c.Genus_id
UNION
SELECT d.name, d.birthday, d.commands, ha.genus_name, ya.age_in_months 
FROM dogs d
LEFT JOIN young_animals ya ON ya.name = d.name
LEFT JOIN pets ha ON ha.id = d.genus_id
UNION
SELECT hm.name, hm.birthday, hm.commands, ha.genus_name, ya.age_in_months
FROM hamsters hm
LEFT JOIN young_animals ya ON ya.name = hm.name
LEFT JOIN pets ha ON ha.id = hm.genus_id;
```
13. Создать [класс с Инкапсуляцией методов и наследованием по диаграмме](https://github.com/MC-DeniSka/itogwork/tree/main/System/src).
14. Написать [программу, имитирующую работу реестра домашних животных](https://github.com/MC-DeniSka/itogwork/tree/main/System/src).
В программе должен быть реализован следующий функционал:    
	14.1 Завести новое животное    
	14.2 определять животное в правильный класс    
	14.3 увидеть список команд, которое выполняет животное    
	14.4 обучить животное новым командам    
	14.5 Реализовать навигацию по меню    
15. Создайте [класс Счетчик](https://github.com/MC-DeniSka/itogwork/blob/main/System/src/Controller/Counter.java), у которого есть метод add(), увеличивающий̆
значение внутренней̆ int переменной̆ на 1 при нажатии “Завести новое
животное” Сделайте так, чтобы с объектом такого типа можно было работать в
блоке try-with-resources. Нужно бросить исключение, если работа с объектом
типа счетчик была не в ресурсном try и/или ресурс остался открыт. Значение
считать в ресурсе try, если при заведении животного заполнены все поля.
