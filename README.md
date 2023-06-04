
# Итоговая аттестация
## Информация о проекте
Необходимо организовать систему учета для питомника, в котором живут
домашние и вьючные животные.

#### 1 Используя команду cat в терминале операционной системы Linux, создать два файла Домашние животные (заполнив файл собаками, кошками, хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и ослы), а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя (Друзья человека).
```
cat > "Домашние животные" <<EOL
Собаки
Кошки
Хомяки
EOL
```
```
cat > "Вьючные животные" <<EOL
Лошади
Верблюды
Ослы
EOL
```
Объеденил эти два файла
```
cat "Домашние животные" "Вьючные животные" > "Друзья человека"
```
Посмотрел содержимое
```
cat "Друзья человека"
```
Переименовал файл
```
mv "Друзья человека" "Лучшие друзья человека"
```
#### 2 Создать директорию, переместить файл туда.
Создал новую директорию
```
mkdir "Контрольная"
```
Переместил файлы в новую директорию
```
mv "Лучшие друзья человека" "Контрольная/"
```
#### 3 Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.
Добавил репозиторий
```
sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.17-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.17-1_all.deb
```
Обновил и установил пакет `mysql-server`
```
sudo apt-get update
sudo apt-get install mysql-server
```
#### 4 Установить и удалить deb-пакет с помощью dpkg.
Загрузил, установил, запустил пакет sl
```
wget http://ftp.us.debian.org/debian/pool/main/s/sl/sl_5.02-1_amd64.deb
sudo dpkg -i sl_5.02-1_amd64.deb
sl
```
Удалил пакет
```
sudo dpkg -r sl
```
#### 5 Выложить историю команд в терминале ubuntu

```
cat > "Домашние животные" <<EOL
cat > "Вьючные животные" <<EOL
cat "Домашние животные" "Вьючные животные" > "Друзья человека"
cat "Друзья человека"
mv "Друзья человека" "Лучшие друзья человека"
mkdir "Контрольная"
mv "Лучшие друзья человека" "Контрольная/"
sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.17-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.17-1_all.deb
sudo apt-get update
sudo apt-get install mysql-server
wget http://ftp.us.debian.org/debian/pool/main/s/sl/sl_5.02-1_amd64.deb
sudo dpkg -i sl_5.02-1_amd64.deb
sl
sudo dpkg -r sl
```
#### 6 Нарисовать диаграмму, в которой есть класс родительский класс, домашние животные и вьючные животные, в составы которых в случае домашних животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные войдут: Лошади, верблюды и ослы).
```
                      Животные
                         |
              ---------------------
              |                   |
      Домашние животные   Вьючные животные
              |                   |
   -----------------       -----------------
   |       |       |       |       |       |
 Собаки  Кошки  Хомяки  Лошади  Верблюды  Ослы
```
#### 7 В подключённом MySQL репозитории создать базу данных “Друзья человека”
```
mysql -u shum -p
```
```
CREATE DATABASE Друзья_человека;
```
#### 8 Создать таблицы с иерархией из диаграммы в БД
Таблица "Животные":
```sql
CREATE TABLE Животные (
  id INT PRIMARY KEY AUTO_INCREMENT,
  тип VARCHAR(50)
);
```

Таблица "Домашние животные"
```sql
CREATE TABLE Домашние_животные (
  id INT PRIMARY KEY,
  вид VARCHAR(50),
  FOREIGN KEY (id) REFERENCES Животные(id)
);
```

Таблица "Собаки"
```sql
CREATE TABLE Собаки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);
```

Таблица "Кошки"
```sql
CREATE TABLE Кошки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);
```

Таблица "Хомяки"
```sql
CREATE TABLE Хомяки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);
```

Таблица "Вьючные животные"
```sql
CREATE TABLE Вьючные_животные (
  id INT PRIMARY KEY,
  вид VARCHAR(50),
  FOREIGN KEY (id) REFERENCES Животные(id)
);
```

Таблица "Лошади"
```sql
CREATE TABLE Лошади (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);
```

Таблица "Верблюды"
```sql
CREATE TABLE Верблюды (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);
```

Таблица "Ослы"
```sql
CREATE TABLE Ослы (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);
```
#### 9. Заполнить низкоуровневые таблицы именами(животных), командами которые они выполняют и датами рождения
```sql
INSERT INTO Собаки ( имя, команда, дата_рождения)
VALUES ('Рекс', 'Сидеть', '2018-05-10'),
       ('Бэйли', 'Лежать', '2019-02-15'),
       ('Луна', 'Голос', '2020-07-20');
```
```sql
INSERT INTO Собаки ( имя, команда, дата_рождения)
VALUES ('Мурка', 'Кэс-кэс', '2017-09-01'),
       ('Барсик', 'А ну брысь' '2018-11-12'),
       ('Снежок', 'Спать' '2019-04-05');
```
```sql
INSERT INTO Хомяки ( имя, команда, дата_рождения)
VALUES ('Дейл', 'Ешь', '2021-01-20'),
       ('Чип', 'Пей', '2022-03-08');
```
```sql
INSERT INTO Лошади ( имя, команда, дата_рождения)
VALUES ('Рыжий', 'Но', '2020-01-21'),
       ('Чёрный', 'Стой', '2020-03-08');
```

```sql
INSERT INTO Верблюды ( имя, команда, дата_рождения)
VALUES ('Валера', 'Пошёл', '2019-01-21'),
       ('Степан', 'Стой', '2019-03-08');
```
```sql
INSERT INTO Ослы ( имя, команда, дата_рождения)
VALUES ('ЗигЗаг', 'Пошёл', '2018-01-21'),
       ('Пуш', 'Стой', '2018-03-08');
```
10 Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.
```
DELETE FROM Верблюды;
```
```sql
CREATE TABLE Лошади_и_ослы AS
SELECT * FROM Лошади
UNION
SELECT * FROM Ослы;
```
#### 11 Создать новую таблицу “молодые животные” в которую попадут все животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице
```sql
CREATE TABLE молодые_животные AS
SELECT *, TIMESTAMPDIFF(MONTH, дата_рождения, CURDATE()) AS возраст_в_месяцах
FROM (
  SELECT *
  FROM (
    SELECT *
    FROM Домашние_животные
    UNION
    SELECT *
    FROM Вьючные_животные
  ) AS животные
  WHERE дата_рождения >= DATE_SUB(CURDATE(), INTERVAL 3 YEAR)
    AND дата_рождения <= DATE_SUB(CURDATE(), INTERVAL 1 YEAR)
) AS молодые;
```


