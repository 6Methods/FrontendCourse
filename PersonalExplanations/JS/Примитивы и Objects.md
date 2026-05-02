Примитивы number, string, null, undefined, symbol, boolean, bigint + обьектный тип object и функции также являются обьектными типами
typeof function - object

В чём разница.
Примитивы копируют значения
a = 10
b = a
b = 20
// log b = 20
// log a = 10

А обьекты живут отдельно в памяти. Переменная хранит только ССЫЛКУ НА ОБЬЕКТ

const user = { name: "Иван"}

const copy = user

copy.name = "Alex"

console.log(user.name) - "Alex"

Заметь, что поменяли мы copy, вывели user и получили значение copy

Получилось так тк user и copy смотрят на 1 обьект {name: "Alex"}

ты не меняешь переменную `copy`. Ты меняешь объект, на который смотрят обе переменные.


