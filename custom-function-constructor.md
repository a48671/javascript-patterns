## Собственные функции конструкторы

Если функцию конструктор вызвать без ключевого слова new, то ```this``` внутри функции будет равен либо ```undefined``` (при 
строгом режиме выполнения), либо будет ссылаться на глобальный объект. Таким образом вызов конструктора без 
ключевого слова new может привезти к нежелательным последствиям. Например, результат выполнения вернет ```undefined```, но 
при этом в глобальный объект будут добавлены свойства, которые добавлялись к ```this``` внутри функции конструктор.

Чтобы избежать подобных ситуаций можно сделать проверку внутри функции:
```javascript
function FunConstructor(name) {
    if (!(this instanceof FunConstructor)) {
        return new FunConstructor(name);
    }
    this.name = name;
}
```

В то же время из функции конструктор можно вернуть что-то явно с помощью ключевого слова ```return```.

```javascript
function FunConstructor(name) {
    this.name = name;
    return { name: 'some name' };
}
const person = new FunConstructor('Andrey');
console.log(person); // { name: 'some name' }
```
Обратите внимание, что в данном случае у объекта person не будет связи с ```FunConstructor```, то есть в свойстве ```person.prototype``` будет лежать ссылка не на FunConstructor, а не ```Object```

Так же не стоит забывать, что если функция конструктор что-то возвращает с помощью ключевого слова ```return```, то это 
должен быть объект, так как при вызове функции конструктор с ключевым словом ```new``` все возвращаемое кроме объекта 
будет игнорироваться и результатом выполнения будет ```undefined```.
```javascript
function FunConstructor(name) {
    this.name = name;
    return 'some name';
}
const person = new FunConstructor('Andrey');
console.log(person); // undefined
```
