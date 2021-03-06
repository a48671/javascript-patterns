## Работа с массивами в циклах

### Не проверять длину массива на каждой итерации цикла
В примере приведенном ниже происходит запрос длинны массива на каждой итерации цикла
```javascript
for (let i = 0; i < array.length; i++) {}
```
Пример ниже оптимизирует цикл сохраняя длину массива в переменную
```javascript
for (let i = 0, arrayLength = array.length; i < arrayLength; i++) {}
```
Этот цикл можно еще немного оптимизировать заменив выражение i < arrayLength на i--. Таким образом когда i станет 
равно 0 выполнение цикла закончится. Оптимизация происходит за счет того, что получение boolean значения из 
числового значение отнимает меньше ресурсов, чем сравнение числа с числом.
В итоге цикл будет выглядеть следующим образом:
```javascript
for (let i = array.length; i--;) {}
```
или
```javascript
function loop() {
    let i = array.length;
    while (i--) {}
}
```
Оптимизация работы с длиной массива особенно актуальна, когда в цикле перебирается массив DOM элементов.
