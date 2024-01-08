# Объекты
### Инициализация объекта
    ``` javascript
    let user = new Object();    // синтаксис "конструктор объекта"
    let user = {}; 
    ```
### Добавление свойства
    ``` javascript
    object.key = value 
    ```
### Удаление свойства 
    ``` javascript
    delete object.key 
    ```
### Виды свойств объекта
    ``` javascript
    let object = {
        name: 'John',
        "likes birds": true,    // ключ из нескольких слов
        [fruit]: 5              // вычисляемые свойства, где let fruit = '...' или выражение
    } 
    ```
### Доступ к значению свойства
    ``` javascript
    object.key
    object['key'] 
    ```
### Cуществующие переменные, как значения для свойств с тем же именем
    ``` javascript
    {
        name: name,
        age                     // age: age
    } 
    ```
### Проверка существования свойства
    ``` javascript
    'key' in object             // свойство есть/нет ( true/false )
    user.noSuchProperty         // === undefined свойства нет 
    ```
### Перебор свойства
    ``` javascript
    for (key in object) {
        // тело цикла выполняется для каждого свойства объекта
    } 
    ```
Переменная, которой присвоен объект, хранит не сам объект, а его «адрес в памяти» – другими словами, «ссылку» на него в отличии от примитивов. 
### Сравнение объектов
При копировании переменной объекта копируется ссылка, но сам объект не дублируется. 

    ``` javascript
    let user = { name: 'John' };
    let admin = user;
    admin.name = 'Pete';      
    alert(user.name);           // 'Pete'
    ```
> Два объекта равны только в том случае, если это один и тот же объект. Даже пустые объекты не равны друг другу.

### Для дублирования объекта 
    ``` javascript
    let user = {
        name: "John",
        age: 30
    };
    let clone = {}; 

    for (let key in user) {
        clone[key] = user[key];
    }
    ```
или 

    ``` javascript
    Object.assign(dest, [src1, src2, src3...]) // где dest-целевой объект, src-исходные объекты (dest)
    ```
### «Глубокое клонирование» (объект внутри объекта) 
    ``` javascript
    let user = {
        name: "John",
        sizes: {
            height: 182,
            width: 50
        }
    };
    ```
> Решение: Использование цикла клонирования, который проверяет каждое значение user[key] и, если это объект, тогда также копирует его структуру. Это называется «глубоким клонированием», либо _.cloneDeep(obj) из библиотеки lodash, либо structuredClone().

### Методы 
Существует более короткий синтаксис для методов в литерале объекта:

    ``` javascript
    user = {
        sayHi: function() {                    // обычное написание
            alert("Привет");
        }
    };
    user = {
        sayHi() {                              // то же самое, что и "sayHi: function(){...}"
        alert("Привет");
    }
    };
    ```

### Ключевое слово this (ссылка на объект)
Его можно использовать в любой функции, даже если это не метод объекта. 
> Вызов this без объекта в функции: this == undefined или ошибка

Значение this вычисляется во время выполнения кода, в зависимости от контекста.

    ``` javascript
    let user = { name: "John" };
    let admin = { name: "Admin" };

    function sayHi() {
        alert( this.name );
    }

    user.f = sayHi;                             // John  (this == user)
    admin.f = sayHi;                            // Admin  (this == admin)
    ```
> У стрелочных функций нет this.

Если мы ссылаемся на this внутри стрелочной функции, то оно берётся из внешней «нормальной» функции.

    ``` javascript
    let user = {
        firstName: "Ilya",
        sayHi() {
            let arrow = () => alert(this.firstName);    // this == user
            arrow();
        }
    };
    ```