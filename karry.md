## Каррирование

Предположим, что перед нами стоит задача преобразовать строку в массив, а затем произвести несколько разных 
фильтраций с разными вхождениями строк в элементах массива.
В данном случае можно применить коррирование:
```javascript
function handleString(string, value) {
    const array = string.split(' ');
    if (!value) {
        return function(value) {
            return array.filter(item => item.includes(value));
        }
    }
    return array.filter(item => item.includes(value));
}
const string = "I would like to have something to drink with you";
const filter = handleString(string);
console.log(filter('a'));
console.log(filter('d'));
console.log(filter('o'));
console.log(handleString(string)('v'));
console.log(handleString(string, 't'));
```
Ниже приведен вариант функции, которая принимает в качестве единственного параметра функцию и возвращает ее 
коррированный вариант.
```javascript
function carry(func) {
    const length = func.length;
    let gotArgs = [];
    
    function carryFunction(gotArgs) {
        return function (...args) {
            newGotArgs = [...gotArgs, ...args];
            if (newGotArgs.length < length) {
                return carryFunction(newGotArgs);
            }
            return func(...newGotArgs);
        }
    }
    
    return carryFunction(gotArgs);
}
function sum(a, b, c, d, e) {
    return a + b + c + d + e;
}
const carrySum = carry(sum);
console.log(carrySum(1, 2)(3)(4)(5));
```
Функция `carryFunction` написана таким образом, что при ее вызове создается локальная область видимости, где 
определяется новая локальная переменная `gotArgs` переданная как параметр функции. Это сделано для того, чтобы каждый 
экземпляр возвращенной функции, не был связан со значением `gotArgs` предыдущей функции.
