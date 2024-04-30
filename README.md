## Работа с Display анимациями
### Создание реестра кадров анимации
```java
//Material.STONE - ID предмета Display
//true - цикличность анимации
Frames frames = new Frames(Material.STONE,true);
```
### Добавление кадра анимации
```java
frames.add(new Frame(
        new Position(0, 0, 0), //обозначение позиции Display в текущем кадре
        new Size(2, 2, 2), //обозначение размера Display в текущем кадре
        new Rotation(90, 0, 0), 0, 20)); //обозначение поворота Display в текущем кадре, а также CustomModelData и длительность кадра
```
Чтобы добавить еще один кадр, продублируйте код выше
### Создание и проигрывание анимации
```java
Animation animation = new Animation(player, location, frames);
//Указание свойств нулевого кадра и проигрывание
animation.play(new Position(0, -1.8F, 0),
        new Size(2, 0.01F,2),
        new Rotation(0, 360, 0),true); //false - закрепление анимации на сущности (пассажир)
```
### Перемещение анимации
```java
//player.getWorld(), 8, -61, 8) - точка телепортации
//50 - скорость телепортации
//0 - задержка телепортации
animation.move(new Location(player.getWorld(), 8, -61, 8), 50, 0);
animation.move(new Location(player.getWorld(), 8, -30, 8), 40, 50);
```
## Работа с MySQL
В рамках API бывают 2 типа запроса - **input** и **output**:
- **Input** отвечает за запросы из базы данных на сервер.
- **Output** отвечает за запросы от сервера в базу данных.
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
