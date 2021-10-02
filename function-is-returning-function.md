## Функция возвращающая функцию

Результатом выполнения функции может быть новая функция.
```javascript
function func() {
    return function foo() {};
}
const fooFunction = func();
```
В момент вызова функции, которая возвращает другую функцию, создается локальная область видимости, закрытая для 
всего, кроме возвращаемой функции. Таким образом можно создавать защищенные переменные и инкапсулировать какую-то 
логику, которой будет пользоваться возвращаемая функция.

Самый просто пример - это создание счетчика вызовов.
```javascript
function counter() {
    let count = 0;
    return function addCount() {
        return ++count;
    }
}
const fun = counter();
const foo = counter();
fun(); // 1
fun(); // 2
fun(); // 3
foo(); // 1
foo(); // 2
```