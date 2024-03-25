### Объекты в JavaScript и их методы

В JavaScript объекты играют ключевую роль, они представляют собой коллекции пар ключ-значение и могут содержать различные методы для работы с ними. Рассмотрим некоторые методы объектов и объясним, почему они хранятся в куче.

#### `Object.create()`

Метод `Object.create()` создает новый объект с указанным прототипом и опциональными свойствами объекта. Этот метод полезен для наследования в JavaScript.

Пример использования:

```javascript
const person = Object.create(
  {
    calculateAge() {
      console.log(`Age: ${new Date().getFullYear() - this.birthYear}`)
    },
  },
  {
    name: {
      value: 'Emma',
      enumerable: true, // visible or not
      writable: true, //default false,can you change or not
      configurable: true, // can you remove key or not
    },
    surname: {
      value: 'Safaryan',
      enumerable: true,
    },
    birthYear: {
      value: 2005,
      enumerable: true, // visible or not
      writable: true, //can you change or not
      configurable: true, // can you remove key or not
    },
    age: {
      get() {
        return new Date().getFullYear() - this.birthYear
      },
      set(value) {
        document.body.style.backgroundColor = 'red'
        console.log(value, 'set age')
      },
    },
  },
)
```

#### `Object.assign()`

Метод `Object.assign()` используется для копирования значений всех перечисляемых свойств из одного или нескольких исходных объектов в целевой объект. Это позволяет объединять объекты или создавать их копии.

Пример использования:

```javascript
const obj1 = { a: 1, b: 2 }
const obj2 = { b: 3, c: 4 }

const mergedObj = Object.assign({}, obj1, obj2)
```

#### `Object.freeze()`

Метод `Object.freeze()` замораживает объект, делая его свойства неизменными. Это означает, что после замораживания объект нельзя изменить, добавить или удалить его свойства.

Пример использования:

```javascript
const obj = { prop: 42 }
Object.freeze(obj)

obj.prop = 33 // Это не будет иметь эффекта
```

#### `Object.defineProperty()`

Метод `Object.defineProperty()` позволяет явно определять новое или изменять существующее свойство непосредственно на объекте и, при необходимости, его параметры.

Пример использования:

```javascript
const obj = {}

Object.defineProperty(obj, 'name', {
  value: 'John',
  writable: false,
  enumerable: true,
})
```

#### `Object.defineProperties()`

Метод Object.defineProperties() определяет новые или изменяет существующие свойства, непосредственно на объекте, возвращая этот объект.

```javascript
const object1 = {}

Object.defineProperties(object1, {
  property1: {
    value: 42,
    writable: true,
  },
  property2: {},
})

console.log(object1.property1)
// Expected output: 42
```

#### `Object.entries()`

Object.entries() метод возвращает массив собственных перечисляемых свойств указанного объекта в формате [key, value], в том же порядке, что и в цикле for...in (разница в том, что for-in перечисляет свойства из цепочки прототипов). Порядок элементов в массиве который возвращается Object.entries() не зависит от того как объект объявлен. Если существует необходимость в определённом порядке, то массив должен быть отсортирован до вызова метода, например Object.entries(obj).sort((a, b) => a[0] - b[0]);.

```javascript
const object1 = {
  a: 'somestring',
  b: 42,
}

//Object.entries(object1) - [["a","somestring"],["b",42]]

for (const [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`)
}

// Expected output:
// "a: somestring"
// "b: 42"
```

#### `Object.preventExtensions()`

Метод Object.preventExtensions() предотвращает добавление новых свойств к объекту (то есть, предотвращает расширение этого объекта в будущем).

```javascript
const object1 = {}

Object.preventExtensions(object1)

try {
  Object.defineProperty(object1, 'property1', {
    value: 42,
  })
} catch (e) {
  console.log(e)
  // Expected output: TypeError: Cannot define property property1, object is not extensible
}
```

#### `Object.keys()`
Метод Object.keys() возвращает массив из собственных перечисляемых свойств переданного объекта, в том же порядке, в котором они бы обходились циклом for...in (разница между циклом и методом в том, что цикл перечисляет свойства и из цепочки прототипов)

```javascript
var arr = ["a", "b", "c"];
console.log(Object.keys(arr)); // консоль: ['0', '1', '2']

// Массивоподобный объект
var obj = { 0: "a", 1: "b", 2: "c" };
console.log(Object.keys(obj)); // консоль: ['0', '1', '2']

// Свойство getFoo является не перечисляемым свойством
var my_obj = Object.create(
  {},
  {
    getFoo: {
      value: function () {
        return this.foo;
      },
    },
  },
);
my_obj.foo = 1;

console.log(Object.keys(my_obj)); // консоль: ['foo']
```

#### `Object.seal()`
Метод Object.seal() запечатывает объект, предотвращая добавление новых свойств к объекту и делая все существующие свойства не настраиваемыми. Значения представленных свойств всё ещё могут изменяться, поскольку они остаются записываемыми.
```javascript
var obj = {
  prop: function () {},
  foo: "bar",
};

// Новые свойства могу быть добавлены, существующие свойства могут быть изменены или удалены.
obj.foo = "baz";
obj.lumpy = "woof";
delete obj.prop;

var o = Object.seal(obj);

assert(o === obj);
assert(Object.isSealed(obj) === true);

// Изменение значений свойств на запечатанном объекте всё ещё работает.
obj.foo = "quux";
```

#### Почему методы объектов хранятся в куче?

Методы объектов хранятся в куче, потому что они являются частью объектов, а объекты хранятся в куче. Куча предназначена для динамически выделяемых данных, таких как объекты и другие сложные структуры данных. Методы объектов, будучи частью этих объектов, сохраняются в той же области памяти (куче), что и сами объекты.

Использование кучи для хранения методов объектов обеспечивает эффективное управление памятью и обеспечивает быстрый доступ к методам при выполнении программы.

Глубокое(deep) и поверхностное(shallow) копирование объектов - это два различных подхода к копированию данных объекта в JavaScript. Давайте рассмотрим их.

### Поверхностное (shallow) копирование

При поверхностном копировании создается новый объект, который содержит те же ключи и значения, что и исходный объект. Однако, если значения исходного объекта являются объектами или массивами, они остаются ссылками на оригинальные объекты в новом объекте.

Пример поверхностного копирования:

```javascript
const originalObject = {
  a: 1,
  b: {
    c: 2,
  },
}

// Поверхностное копирование
const shallowCopy = Object.assign({}, originalObject)

originalObject.b.c = 3

console.log(shallowCopy.b.c) // Выведет 3
```

В этом примере `shallowCopy` содержит те же ключи и значения, что и `originalObject`, но если значения являются объектами, они остаются ссылками на оригинальные объекты.

### Глубокое (deep) копирование

Глубокое копирование создает новый объект и рекурсивно копирует все вложенные объекты и их значения. Это гарантирует, что новый объект полностью независим от исходного.

JavaScript не предоставляет встроенного метода для глубокого копирования объектов. Однако, его можно реализовать с помощью рекурсии или сторонних библиотек.

Для глубокого копирования объектов вы можете использовать оператор расширения ... в JavaScript или метод cloneDeep() из библиотеки Lodash.

### Использование метода `cloneDeep()` из Lodash

Lodash - это библиотека JavaScript, которая предоставляет множество удобных функций для работы с данными, включая глубокое копирование объектов с помощью метода `cloneDeep()`.

```javascript
const _ = require('lodash')

const originalObject = {
  a: 1,
  b: {
    c: 2,
  },
}

const deepCopiedObject = _.cloneDeep(originalObject)

originalObject.b.c = 3

console.log(deepCopiedObject.b.c) // Выведет 2
```

Оба подхода позволяют создавать глубокие копии объектов, но использование метода `cloneDeep()` из Lodash может быть более удобным и читаемым в некоторых случаях, особенно если вам уже доступна библиотека Lodash в вашем проекте.
