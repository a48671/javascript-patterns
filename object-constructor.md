## Конструктор Object

Создавая объекты, всегда предпочитайте их создавать с помощью литералов.
Для этого есть несколько причин:
- создание объекта с помощью литералов требует меньшего написания кода;
- если создавать объект с помощью конструктора Object внутри локальной области видимости, то интерпретатор при 
  каждом создании будет обходить всю цепочку областей видимости, чтобы убедиться, что в какой-нибудь из областей 
  видимости не был создан одноименный конструктор.
- конструктор Object может принимать в себя разные типы значений и при этом возвращать различный результат, что 
  может привести к неожиданным последствиям.
```javascript
const obj = new Object();
const stringObj = new Object('string');
const numberObj = new Object(4);
console.log(stringObj.constructor); // String
console.log(numberObj.constructor); // Number
```