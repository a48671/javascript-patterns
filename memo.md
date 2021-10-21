## Мемоизация

Если существует вероятность того, что одна и та же функция, имеющая внутри какую-то сложную логику, может вызываться 
повторно с теми же параметрами, при этом она должна вернуть, точно такой же результат, как и в прошлый раз, можно 
применить кэширование:
```javascript
function memoFunction(a, b, c) {
    const cachekey = JSON.stringify(Array.prototype.slice.call(arguments));
    if (!memoFunction.cache[cachekey]) {
        const result = a + b + c;
        return memoFunction.cache[cachekey] = result;
    }
    return memoFunction.cache[cachekey];
}
memoFunction.cache = {};
```
