Давайте сформулируем 15 задач по теме прототипов и цепочек прототипов в JavaScript, от простых к сложным. Задачи будут включать в себя сравнения и вопросы на понимание работы `__proto__` и `prototype`.

### Задача 1
```javascript
function Animal() {}
let dog = new Animal();
console.log(dog instanceof Animal);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 2
```javascript
let obj = {};
console.log(obj.__proto__ === Object.prototype);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 3
```javascript
function Animal() {}
Animal.prototype.legs = 4;
let cat = new Animal();
console.log(cat.legs);
```
<details>
<summary>Ответ</summary>
4
</details>

### Задача 4
```javascript
function Animal() {}
Animal.prototype.legs = 4;
let rabbit = new Animal();
rabbit.legs = 2;
console.log(rabbit.legs);
```
<details>
<summary>Ответ</summary>
2
</details>

### Задача 5
```javascript
let animal = {
  eats: true
};
let rabbit = Object.create(animal);
console.log(rabbit.eats);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 6
```javascript
let animal = {
  eats: true
};
let rabbit = Object.create(animal);
console.log(rabbit.__proto__ === animal);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 7
```javascript
function Animal(name) {
  this.name = name;
}
let cat = new Animal('Whiskers');
console.log(cat.__proto__ === Animal.prototype);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 8
```javascript
function Animal() {}
let dog = new Animal();
console.log(dog.__proto__.__proto__ === Object.prototype);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 9
```javascript
function Animal() {}
function Dog() {}
Dog.prototype = Object.create(Animal.prototype);
let myDog = new Dog();
console.log(myDog instanceof Animal);
```
<details>
<summary>Ответ</summary>
true
</details>

### Здадача 10
```javascript
function Animal() {}
Animal.prototype.legs = 4;
let dog = new Animal();
Animal.prototype = { legs: 3 };
console.log(dog.legs);
```
<details>
<summary>Ответ</summary>
4
</details>

### Задача 11
```javascript
function Animal() {}
function Bird() {}
Bird.prototype = new Animal();
Bird.prototype.fly = true;
let pigeon = new Bird();
console.log(pigeon.fly && pigeon instanceof Animal);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 12
```javascript
let animal = {
  eats: true
};
let rabbit = Object.create(animal, {
  jumps: {
    value: true
  }
});
console.log(rabbit.jumps && rabbit.eats);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 13
```javascript
function Animal() {}
Animal.prototype.eats = true;
function Rabbit() {}
Rabbit.prototype = Animal.prototype;
Rabbit.prototype.jumps = true;
let animal = new Animal();
console.log(animal.jumps);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 14
```javascript
function Animal() {}
Animal.prototype.eats = true;
let rabbit = new Animal();
rabbit.__proto__.jumps = true;
let squirrel = new Animal();
console.log(squirrel.jumps);
```
<details>
<summary>Ответ</summary>
true
</details>

### Задача 15
```javascript
function Animal() {}
function Rabbit() {}
Rabbit.prototype = Object.create(Animal.prototype);
Animal.prototype.eats = true;
Rabbit.prototype.jumps = true;
let animal = new Animal();
let rabbit = new Rabbit();
console.log(animal.jumps, rabbit.eats);
```
<details>
<summary>Ответ</summary>
undefined,true
</details>
Эти задачи охватывают базовое понимание прототипов и прототипного наследования в JavaScript, включая работу с `__proto__`, `prototype`, использование `Object.create` и оператор `instanceof`.