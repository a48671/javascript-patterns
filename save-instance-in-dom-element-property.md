## Сохранение экземпляра класса в свойство DOM-элемента

```html
<style>
    .tooltip {
        display: block;
        position: relative;
    }
    .tooltip.shown .message {
        display: block;
    }
    .message {
        display: none;
        position: absolute;
        left: 0;
        top: 0;
        transform: translate(100%, 0);
    }
</style>
<div id="tooltip">
    <div class="icon">Push me!</div>
    <div class="message">Some description</div>
</div>
```

```javascript
class Tooltip {
    element;
    
    constructor(elementId) {
        this.element = document.getElementById(elementId);
        this.element.classList.add('tooltip');
        const icon = this.element.querySelector('.icon');
        icon.instanceTooltip = this;
        icon.addEventListener('click', this.onClick)
    }
    
    onClick(event) {
        event.preventDefault();
        const instanceTooltip = event.target.instanceTooltip;
        if (instanceTooltip) {
            instanceTooltip.toggle();
        }
    }
    
    toggle() {
        this.element.classList.toggle('shown');
    }
    
    get shown() {
        this.element.classList.contains('shown');
    }
    
    set shown(value) {
        if (value) {
            if (this.shown) return;
            this.toggle();
        } else {
            if (!this.shown) return;
            this.toggle();
        }
    }
}

const tooltip = new Tooltip('tooltip');
```
В данном примере функция `onClick` является методом класса, который передается в качестве обработчика в метод 
`addEventListener` следовательно внутри функции `onClick` не получиться обратиться к `this.element`, так как ссылка 
на экземпляр класса `Tooltip` будет потеряна. Можно, конечно привязать контекст c помощью метода `.bind`, но тогда 
при каждом создании экземпляра класса, будет создаваться новая функция с привязанным контекстом. 
Благодаря тому, что мы сохранили ссылку на экземпляр класса в свойство `icon.instanceTooltip`, при клике на этот 
элемент мы можем обратиться к этому свойству тем самым получив доступ к экземпляру и всем его свойствам и методам.
