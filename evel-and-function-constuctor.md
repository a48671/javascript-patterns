## Функция eval() и конструктор Function

Функция eval() и конструктор Function выполняют примерно одинаковые действия, но есть некоторые отличия:
Код выполненный в eval() получает доступ ко всей цепочке областей видимости, в то время как код выполненный внутри 
Function получает доступ только к глобальной области видимости.
```javascript
const c = 'C';
(function() {
    const a = 'A';
    eval('console.log(c, a)'); // C A
})();
(function() {
    const a = 'A';
    Function('console.log(c)'); // C
    Function('console.log(typeof a)'); // undefined
    Function('console.log(a)'); // error: Uncaught ReferenceError: a is not defined
})();
```
