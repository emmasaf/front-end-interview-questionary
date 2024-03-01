### первое задание

Что будет выводиться в консоль при вызове person.showActions()?

```javascript
const person = {
  name: 'John',
  actions: ['smile', 'wave', 'jump'],
  showActions: function () {
    this.actions.forEach(function (action) {
      console.log(this.name + ' can ' + action)
    })
  },
}

person.showActions()
```

<details>
    <summary>Answer</summary>
    <p>
В данном случае, когда функция обратного вызова передается методу `forEach`, контекст `this` внутри функции обратного вызова не наследуется от внешней функции `showActions`. Вместо этого, без явного указания контекста, `this` внутри функции обратного вызова будет указывать на глобальный объект (`window` в браузерах) или будет `undefined` в строгом режиме (`'use strict'`). Поскольку `name` не определен в глобальном объекте (предполагая, что мы не находимся в строгом режиме и не установили глобальную переменную `name`), вывод будет:

```
undefined can smile
undefined can wave
undefined can jump
```

Чтобы `this` внутри функции обратного вызова указывал на объект `person`, можно использовать дополнительные подходы, например, использование стрелочной функции (которая не создает собственный контекст `this` и наследует его из внешней функции) или метод `bind` для явного указания контекста:

### Используя стрелочную функцию:

```javascript
showActions: function() {
  this.actions.forEach((action) => {
    console.log(this.name + ' can ' + action);
  });
}
```

### Используя `bind`:

```javascript
showActions: function() {
  this.actions.forEach(function(action) {
    console.log(this.name + ' can ' + action);
  }.bind(this));
}
```

Оба этих подхода исправят изначальную проблему и обеспечат вывод, который ты ожидаешь:

```
John can smile
John can wave
John can jump
```



</details>

### второе задание

Хорошо, вот твое второе задание:

```javascript
function Person(name) {
  this.name = name
}

Person.prototype.greet = function () {
  console.log('Hello, my name is ' + this.name)
  setTimeout(function () {
    console.log('I am still ' + this.name)
  }, 1000)
}

const bob = new Person('Bob')
bob.greet()
```

Что будет выводиться в консоль при вызове `bob.greet()`?

<details>
<summary>
Answer
</summary>

```csharp
Hello, my name is Bob
```

Это потому, что метод `greet` вызывается на экземпляре `Person`, и `this` в контексте этого метода ссылается на сам экземпляр, позволяя доступ к свойству `name`.

Однако, внутри `setTimeout`, функция обратного вызова теряет контекст `this`, который ссылался на экземпляр `Person`, и вместо этого `this` начинает ссылаться на глобальный объект (в браузерах это `window`). Если мы находимся в строгом режиме (`'use strict'`), `this` будет `undefined`. Так как в большинстве сред выполнения JavaScript по умолчанию `this` внутри функции, вызванной через `setTimeout`, будет указывать на глобальный объект, и если в этом объекте нет свойства `name`, результатом будет:

```csharp
I am still undefined
```

Но это предполагает, что `name` не определено глобально. Если бы в глобальном объекте было определено свойство `name`, то вместо `undefined` могло бы быть выведено это значение. Например, в браузере может быть установлено глобальное свойство `window.name`, и тогда результат мог бы отличаться. Однако, без дополнительного контекста, предполагая стандартные условия, твой ответ в целом верен, за исключением мелкой опечатки:

```csharp
I am still undefined
```

Чтобы `this` внутри `setTimeout` указывал на правильный объект, можно использовать стрелочную функцию (которая не создает собственный контекст `this`, а использует лексический контекст) или метод `bind`:

### С использованием стрелочной функции:

```javascript
Person.prototype.greet = function () {
  console.log('Hello, my name is ' + this.name)
  setTimeout(() => {
    console.log('I am still ' + this.name)
  }, 1000)
}
```

### С использованием `bind`:

```javascript
Person.prototype.greet = function () {
  console.log('Hello, my name is ' + this.name)
  setTimeout(
    function () {
      console.log('I am still ' + this.name)
    }.bind(this),
    1000,
  )
}
```

Оба этих подхода гарантируют, что `this` внутри асинхронного вызова правильно указывает на экземпляр `Person`, и второй `console.log` выведет:

```
I am still Bob
```

</details>


### давай перейдем к третьему заданию:


```javascript
const team = {
  members: ['Jane', 'Bill'],
  teamName: 'Super Squad',
  teamGreet: function() {
    this.members.forEach((member) => {
      console.log(`${member} is part of ${this.teamName}`);
    });
  }
};

team.teamGreet();
```

Что будет выводиться в консоль при вызове `team.teamGreet()`?

<details>
<summary>Answer</summary>
При вызове `team.teamGreet()`, в консоль будет выведено:

```csharp
Jane is part of Super Squad
Bill is part of Super Squad
```

Это происходит потому, что стрелочная функция, используемая в `forEach`, не создает собственный контекст `this`, а заимствует его из окружающего лексического контекста, то есть из метода `teamGreet`. В этом случае `this` ссылается на объект `team`, благодаря чему доступны свойства `members` и `teamName` этого объекта.
</details>

### Давай рассмотрим более сложный пример с использованием замыканий:

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.delayedGreet = function() {
  setTimeout(function() {
    console.log('Hello, my name is ' + this.name);
  }.bind(this), 1000);
};

const person = new Person('Alice');
person.delayedGreet();

```
<details>
<summary>Answer</summary>
В этом примере определен конструктор Person, который принимает имя и устанавливает его как свойство экземпляра. Метод delayedGreet добавляется в прототип Person и при его вызове запланирует асинхронное выполнение функции, которая выводит приветствие в консоль.

Ключевой момент здесь — использование .bind(this) для функции, переданной в setTimeout. Метод .bind() создает новую функцию, которая, когда вызывается, имеет свой this установленным в предоставленное значение, в данном случае в текущий экземпляр Person. Это необходимо, потому что без .bind(this), this внутри функции, переданной в setTimeout, будет указывать на глобальный объект (или на undefined в строгом режиме), а не на экземпляр Person, как это предполагалось.

Таким образом, благодаря .bind(this), когда delayedGreet вызывается на экземпляре person, через 1000 мс в консоль будет корректно выведено:

```csharp
Hello, my name is Alice
```
Этот пример демонстрирует, как можно использовать замыкания и this вместе для достижения желаемого поведения в асинхронных операциях, таких как задержки с setTimeout, особенно когда требуется сохранить контекст this из внешней функции.
</details>