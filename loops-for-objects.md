## Циклы для объектов
```javascript
for (const key in obj) {}
```
У этого цикла есть проблема, заключающаяся в том, что в нем перебираются свойства не только объекта obj, но и 
enumerable свойства его prototype, а это не всегда очевидно и возможно не нужно.
Например:
```javascript
const obj = {a: 'a', b: 'b'};
Object.prototype.c = 'c';
for (const key in obj) {
    console.log(key, obj[key]);
}
// in console will be
// a 'a'
// b 'b'
// c 'c'
```
Чтобы в цикле обрабатывались только собственные значения объекта можно использовать метод hasOwnProperty
```javascript
const obj = {a: 'a', b: 'b'};
Object.prototype.c = 'c';
for (const key in obj) if (obj.hasOwnProperty(key)) {
    console.log(key, obj[key]);
}
// in console will be
// a 'a'
// b 'b'
```
Для того, чтобы оптимизировать поиск метода hasOwnProperty в списке свойств prototype на каждой итерации цикла можно 
сохранить его в 
переменную и использовать ее, так же можно взять это свойство не у объекта свойства которого мы перечисляем, а 
напрямую у прототипа, чтобы исключить вероятность того, что у перечисляемого объекта по какой-то причине этот метот 
не был переопределен
```javascript
const obj = {a: 'a', b: 'b'};
const checkProperty = Object.prototype.hasOwnProperty.bind(obj);
for (const key in obj) if (checkProperty(key)) {
    console.log(key, obj[key]);
}
```
