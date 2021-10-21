## Немедленная инициализация объекта

Когда нужно структурировать какую-то операцию инициализации, то в целях сохранения глобальной области видимости 
"чистой" можно использовать немедленно инициализирующийся объект:
```javascript
({
    wrapper: document.getElementById('slider'),
    count: this.wrapper.children.length,
    loop: true,
    init() {
        new Slider({ wrapper, count, loop })
    }
}).init();
```
