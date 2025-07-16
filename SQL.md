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

___
/// Relations
```sql
CREATE TABLE DepartmentsHeads (  
    HeadID INT IDENTITY(1,1) PRIMARY KEY,  
    FullName NVARCHAR(100) NOT NULL,  
    Email NVARCHAR(100),  
    Phone NVARCHAR(20)  
);  
  
CREATE TABLE Departments (  
    DepartmentID INT IDENTITY(1,1) PRIMARY KEY,  
    Name NVARCHAR(100) NOT NULL UNIQUE,  
    Description NVARCHAR(MAX),  
    HeadID INT,  
    FOREIGN KEY (HeadID) REFERENCES DepartmentsHeads(HeadID)  
);  
  
CREATE TABLE Teachers (  
    TeacherID INT IDENTITY(1,1) PRIMARY KEY,  
    FullName NVARCHAR(100) NOT NULL,  
    Email NVARCHAR(100),  
    Phone NVARCHAR(20)  
);  
  
CREATE TABLE Groups (  
    GroupID INT IDENTITY(1,1) PRIMARY KEY,  
    Name NVARCHAR(50) NOT NULL UNIQUE,  
    Description NVARCHAR(MAX),  
    DepartmentID INT,  
    TeacherID INT,  
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID),  
    FOREIGN KEY (TeacherID) REFERENCES Teachers(TeacherID)  
);  
  
CREATE TABLE Students (  
    StudentID INT IDENTITY(1,1) PRIMARY KEY,  
    FullName NVARCHAR(100) NOT NULL,  
    Email NVARCHAR(100),  
    GroupID INT,  
    FOREIGN KEY (GroupID) REFERENCES Groups(GroupID)  
);  
  
INSERT INTO DepartmentsHeads (FullName, Email, Phone) VALUES  
(N'Иванов Иван Иванович', 'ivanov@university.edu', '1234567890'),  
(N'Петров Петр Петрович', 'petrov@university.edu', '0987654321');  
  
INSERT INTO Departments (Name, Description, HeadID) VALUES  
(N'Математика', N'Кафедра математики и статистики', 1),  
(N'Физика', N'Кафедра общей и теоретической физики', 2);  
  
INSERT INTO Teachers (FullName, Email, Phone) VALUES  
(N'Смирнова Анна Сергеевна', 'smirnova@university.edu', '111222333'),  
(N'Кузнецов Алексей Викторович', 'kuznetsov@university.edu', '444555666');  
  
INSERT INTO Groups (Name, Description, DepartmentID, TeacherID) VALUES  
(N'Группа М101', N'1 курс, математика', 1, 1),  
(N'Группа М102', N'1 курс, математика', 1, 2),  
(N'Группа Ф101', N'1 курс, физика', 2, 2);  
  
INSERT INTO Students (FullName, Email, GroupID) VALUES  
(N'Александров Дмитрий', 'alexandrov@university.edu', 1),  
(N'Борисова Мария', 'borisova@university.edu', 1),  
(N'Волков Николай', 'volkov@university.edu', 2),  
(N'Григорьева Елена', 'grigorieva@university.edu', 3);  
  
SELECT s.*  
FROM Students s  
JOIN Groups g ON s.GroupID = g.GroupID  
WHERE g.Name = N'Группа М101';  
  
SELECT g.*  
FROM Groups g  
JOIN Students s ON g.GroupID = s.GroupID  
WHERE s.FullName = N'Борисова Мария';  
  
SELECT g.*  
FROM Groups g  
JOIN Teachers t ON g.TeacherID = t.TeacherID  
WHERE t.FullName = N'Кузнецов Алексей Викторович';  
  
SELECT g.*  
FROM Groups g  
JOIN Departments d ON g.DepartmentID = d.DepartmentID  
JOIN DepartmentsHeads h ON d.HeadID = h.HeadID  
WHERE h.FullName = N'Петров Петр Петрович';  
  
SELECT s.*  
FROM Students s  
JOIN Groups g ON s.GroupID = g.GroupID  
JOIN Departments d ON g.DepartmentID = d.DepartmentID  
JOIN DepartmentsHeads h ON d.HeadID = h.HeadID  
WHERE h.FullName = N'Иванов Иван Иванович';  
  
SELECT g.GroupID  
FROM Groups g  
JOIN Departments d ON g.DepartmentID = d.DepartmentID  
WHERE d.Name = N'Математика';
```

____
///  Агрегатные функции

Предложение `GROUP BY` в SQL используется для ==группировки строк в таблице по значениям одного или нескольких столбцов==. Оно часто применяется в сочетании с агрегатными функциями, такими как `COUNT`, `SUM`, `AVG`, `MAX` или `MIN`, для выполнения вычислений над сгруппированными данными.

Предложение `HAVING` в SQL используется для фильтрации результатов группировки, полученных с помощью `GROUP BY`. Оно позволяет применять условия к сгруппированным данным, в отличие от `WHERE`, которое применяется к отдельным строкам до группировки. Таким образом, `HAVING` используется для отбора определенных групп на основе агрегатных функций, таких как `SUM`, `COUNT`, `AVG`, `MIN`, `MAX`, в то время как `WHERE` не может напрямую работать с этими функциями.

```sql
-- COUNT, COUNT_BIG

-- SELECT COUNT(*) AS Count, P.SupplierID
-- FROM Products AS P
-- GROUP BY P.SupplierID
-- HAVING COUNT(*) > 3

-- MIN/MAX

-- SELECT MAX(OD.Quantity) AS MaxQuantity, OD.ProductID
-- FROM [Order Details] AS OD
-- GROUP BY OD.ProductID

-- SUM/AVG

-- SELECT SUM(P.UnitPrice), P.CategoryID
-- FROM Products AS P
-- GROUP BY P.CategoryID


SELECT R.Count, S.CompanyName
FROM (SELECT COUNT(*) AS Count, P.SupplierID
      FROM Products AS P
      GROUP BY P.SupplierID
      HAVING COUNT(*) > 3) AS R
JOIN Suppliers AS S ON S.SupplierID = R.SupplierID


SELECT *
FROM (SELECT COUNT(*) AS Count, P.SupplierID
      FROM Products AS P
      GROUP BY P.SupplierID) AS R
WHERE R.Count > 3
```

