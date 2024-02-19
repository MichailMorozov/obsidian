
___###### tags: #
###### links: [[OBJECT(datatype)]], [[Datatypes(js)]]
___
Тип `object` (объект) – особенный.

Все остальные типы называются «примитивными», потому что их значениями могут быть только простые значения (будь то строка, или число, или что-то ещё). В объектах же хранят коллекции данных или более сложные структуры.

Объекты занимают важное место в языке и требуют особого внимания. Мы разберёмся с ними в главе [Объекты](https://learn.javascript.ru/object) после того, как узнаем больше о примитивах.

Объект  
```js
let object = {
	cat: 'Мурзик',
	dog: 'Шарик',
	number: 23,
	array: [1, 2, 3],
}

console.log(object.array[2])
>>> 3
```