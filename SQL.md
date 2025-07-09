DB - Database
DBMS - Database Management System
SQL - Structured Query Language, реляционная база данных (система отношений)
MS SQL - Microsoft SQL

JSON - JAVASCRIPT OBJECT NOTATION документный тип


DDL (Data Definition Language) - создание, добавление
DML
DCL
TCL

CREATE DATABASE DBName - создание базы данных \[ ] - позволяет писать название с пробелами

-- для комментариев

USE DBName - переключиться на другую базу данных

GO -  пока предыдущая не отработает, к следующему не переходить

SMALLINT (2b)
TINYINT (1b)
INT (4b)
BIGINT (8b)
DECIMAL(n, x)
FLOAT
NVARCHAR(100) - в юникод формате сколько символов
VARCHAR(100) - без поддержки юникода
CHAR(100) - фиксированное занимает 100
NCHAR(100) - фиксированное занимает 100 c юникодом
BIT - 0 или 1
DATE
TIME
DATETIME
DATETIME2

(MAX) - максимальное значение

PRIMARY KEY - уникальный первичный ключ
IDENTITY(1, 1) - автоматическое увеличение ключа (с какого, на сколько увеличиваться)
UNIQUE - проверяет уникальность
DROP TABLE - удаление таблицы

-- CONSTRAINTS
CHECK(Presents > 0) - проверка для добавления
NOT NULL
DEFAULT(N'Mysterious Cloun') - значение по умолчанию
CONSTRAINT позволяет создавать уникальное ограничение

Cоздание таблицы
CREATE TABLE Names
{
	Id INT ~~PRIMARY~~ KEY IDENTITY(1, 1)
	\[Decimal] 
	Name NVARCHAR (64),
	Mail NVARCHAR (100) UNIQUE,
	Gender BIT,
	Birthday DATETIME,
	Presents INT CHECK(Presents > 0)
	CONSTRAINT PK_Clowns_Id PRIMARY KET(Id)
}

INSERT INTO TableName - вставить значение
VALUES("DD" "FFF". 1) - заполняем поля

ALTER TABLE - команда DDL  
DROP CONSTRAINT Name - убрать ограничение

ALTER TABLE - команда DDL  
ADD CONSTRAINT Name - добавить ограничение

____
DML

SELECT - выбрать
SELECT \* - выбрать всё
SELECT TOP n - выбрать топ скольких-то
As - как временное имя
FROM - откуда, например, из какой таблицы
WHERE - где соответствует условию
LIKE - похожи на , например 's%' (начинается на s)
'%s' - заканчивается на
'%s%' - содержит
ORDER BY - по каком столбцу отсортировать. С DESC можно в обратно порядке
IN (n, n, n) - в этих скобках что входит
UPDATE - обновить
DELETE FROM - удалить
SET - установить новое значение (с апдейт)
TRUNCATE - операция мгновенного удаления всех строк в таблице

\> , <, >=, <=
= - equals
<> - not equals

SELECT C.Name As \[Full Name], Mail, C.Id
FROM Clowns AS C
WHERE Presents >= 10 AND Presents <= 11

или WHERE Presents BETWEEN 5 AND 10


CONVERT(datetime, '03/14/1997', 101)
Часть	Значение
CONVERT	Функция преобразования типов в SQL Server.
datetime	Целевой тип данных (мы хотим получить дату и время).
'03/14/1997'	Исходное значение — строка с датой в формате MM/DD/YYYY.
101	Стиль преобразования: 101 означает американский формат даты — mm/dd/yyyy.

\+ для объединения строк
- `OFFSET 1 ROWS` — пропустить первую строку.
- `FETCH NEXT 3 ROWS ONLY` — взять следующие 3 строки.
  
DATEDIFF(year, \[Дата рождения], GETDATE())
- **`DATEDIFF`** — встроенная функция для вычисления разницы между датами.
- Первый параметр — **единица измерения** разницы, в данном случае `year` — значит, мы хотим получить разницу в годах.
- Второй параметр — **начальная дата** — здесь `[Дата рождения]`.
- Третий параметр — **конечная дата** — здесь `GETDATE()` — текущая дата и время сервера.

`UPPER(expression)`
- Преобразует строку в **ЗАГЛАВНЫЕ буквы**.

`LOWER(expression)`
- Преобразует строку в **строчные буквы**.