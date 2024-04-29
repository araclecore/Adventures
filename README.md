# Adventures
### Создание таблицы в базе данных
```java
//Декларирование output запроса
Output output = new Output(AAPI.connection, "Test");
//Обозначение будующих колонн таблицы
output.column("id","INT(9)");
output.column("username","VARCHAR(15)");
output.column("status","VARCHAR(10)");
//Создание таблицы
output.table();
```
### Внесение информации в базу данных
```java
//Декларирование output запроса
Output output = new Output(AAPI.connection, "Test");
//Обозначение вносимых значений
output.value("1");
output.value("aracle");
output.value("online");
//Внесение значений в таблицу
output.insert();
```
### Обновление информации в базе данных
```java
//Декларирование output запроса
Output output = new Output(AAPI.connection, "Test");
//Обозначение условия для обновления данных
output.condition("username","aracle");
//Обозначение обновляемых столбцов и данных в них
output.modify("status", "offline");
//Обновление значений в таблице
output.update();
```
### Получение информации из базы данных
```java
//Декларирование input запроса
Input input = new Input(AAPI.connection, "Test");
//Обозначение колонн из которых нужно плучить данные
input.column("username");
input.column("status");
//Обозначение условия для выбора данных
input.condition("id","1");
//Получение данных из таблицы
input.select();
//Обработка данных
String username = input.value("username").toString();
String status = input.value("status").toString();
```
