## Кроссплатформенное обращение к глобальному объекту

Глобальный объект в разных средах выполнения JS может называться по-разному, по этому, если есть вероятность, что 
код будет выполняться не только в браузере, но и в других средах выполнения, можно использовать паттерн IIFE и 
передавать в качестве параметра IIFE this, который будет указывать на глобальный объект.
```javascript
(function(globalObject) {
    // use globalObject
})(this);
```
