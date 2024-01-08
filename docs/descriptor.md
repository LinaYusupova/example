# Флаги конфигурации для свойств
* writable – если true, свойство можно изменить / только для чтения.
* enumerable – если true, свойство перечисляется в циклах / циклы его игнорируют (Object.keys(user) не возвращаеты).
* configurable – если true, свойство можно удалить, атрибуты можно изменять / этого делать нельзя, НО изменить значение можно (из false в true нельзя).
> По умолчанию true
### Метод Object.getOwnPropertyDescriptor(object, property) 
Позволяет получить полную информацию о свойстве, возвращает объект - дескриптор свойства.

    ``` 
    let user = {
        name: "John"
    };

    alert(JSON.stringify(Object.getOwnPropertyDescriptor(user, 'name'), null, 2));
    // дескриптор свойства:
    // {
    //     "value": "John",
    //     "writable": true,
    //     "enumerable": true,
    //     "configurable": true
    // }
    ```
### Метод Object.defineProperty(object, property, descriptor) 
Позволяет изменить флаги.

    ``` 
    let user = {};

    Object.defineProperties(user, "name", { // если свойство одно Object.defineProperty
        value: "John",
        writable: false,
        enumerable: true,
        configurable: true
    });
    ```
Для клонирования объекта вместе с его флагами:

    ``` 
    let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));
    ```
Методы, которые ограничивают ***доступ ко всему объекту***:
* Object.preventExtensions(obj) - запрещает добавлять новые свойства в объект.
* Object.seal(obj) - запрещает добавлять/удалять свойства. Устанавливает configurable: false для всех существующих свойств.
* Object.freeze(obj) - запрещает добавлять/удалять/изменять свойства. Устанавливает configurable: false, writable: false для всех существующих свойств.
> Для проверки Object.isExtensible(obj), Object.isSealed(obj), Object.isFrozen(obj).