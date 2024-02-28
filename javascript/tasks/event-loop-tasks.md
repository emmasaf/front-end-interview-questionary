Давай создадим 5 задачек на понимание работы Event Loop в JavaScript. Задачи будут включать в себя разные асинхронные операции, такие как `setTimeout`, `Promise`, и другие.

### Задача 1

```javascript
console.log('A');
setTimeout(() => console.log('B'), 0);
Promise.resolve().then(() => console.log('C'));
console.log('D');
```
<details>
<summary>Ответ на Задачу 1</summary>

1. A
2. D
3. C
4. B

</details>

### Задача 2

```javascript
setTimeout(() => console.log('A'), 100);
Promise.resolve().then(() => console.log('B'));
setTimeout(() => console.log('C'), 0);
console.log('D');
```
<details>
<summary>Ответ на Задачу 2</summary>

1. D
2. B
3. C
4. A

</details>

### Задача 3

```javascript
console.log('A');
new Promise((resolve, reject) => {
    console.log('B');
    resolve();
}).then(() => {
    console.log('C');
    setTimeout(() => console.log('D'), 0);
});
console.log('E');
```

<details>
<summary>Ответ на Задачу 3</summary>

1. A
2. B
3. E
4. C
5. D

</details>

### Задача 4

```javascript
async function asyncFunction() {
    console.log('A');
    await Promise.resolve().then(() => console.log('B'));
    console.log('C');
}
asyncFunction();
console.log('D');
```

<details>
<summary>Ответ на Задачу 4</summary>

1. A - Синхронный вызов функции `console.log`.
2. B - Выполнение `console.log` внутри `Promise.resolve().then()` является микрозадачей, которая запускается сразу после завершения текущего стека вызовов, но перед следующей макрозадачей.
3. D - Синхронный вызов `console.log` после вызова асинхронной функции, но перед тем, как промис внутри этой асинхронной функции разрешится.
4. C - Выполняется после того, как промис внутри асинхронной функции `asyncFunction` разрешается, что происходит после микрозадачи, добавленной с помощью `Promise.resolve().then()`.

</details>



### Задача 5

```javascript
console.log('A');
setTimeout(() => console.log('B'), 0);
new Promise((resolve, reject) => {
    console.log('C');
    resolve();
}).then(() => console.log('D'));
setTimeout(() => {
    console.log('E');
    Promise.resolve().then(() => console.log('F'));
}, 0);
console.log('G');
```

<details>
<summary>Ответ на Задачу 5</summary>

1. A
2. C
3. G
4. D
5. B
6. E
7. F

</details>


Каждая из этих задач разработана так, чтобы проверить понимание порядка выполнения асинхронного и синхронного кода в JavaScript, включая то, как работают микрозадачи (`Promise`) и макрозадачи (`setTimeout`). После того как скажешь, я предоставлю ответы на каждую из этих задач.


##Давай усложним задачи, добавив больше асинхронных операций и взаимодействий между ними.

### Задача 1

```javascript
console.log('Start');

setTimeout(() => {
    console.log('Timeout 1');
    Promise.resolve().then(() => console.log('Promise 1'));
}, 0);

Promise.resolve().then(() => {
    console.log('Promise 2');
    setTimeout(() => console.log('Timeout 2'), 0);
});

setTimeout(() => console.log('Timeout 3'), 0);

console.log('End');
```

<details>
<summary>Ответ на Задачу 1</summary>

```csharp
Start
End
Promise 2
Timeout 1
Promise 1
Timeout 3
Timeout 2
```

</details>

### Задача 2

```javascript
console.log('Start');

Promise.resolve('Promise 1').then((res) => {
    console.log(res);
    setTimeout(() => {
        console.log('Timeout inside Promise');
    }, 0);
});

setTimeout(() => {
    console.log('Timeout 1');
    Promise.resolve('Promise inside Timeout').then(console.log);
}, 0);

console.log('End');
```

<details>
<summary>Ответ на Задачу 2</summary>

```csharp
Start
End
Promise 1
Timeout 1
Promise inside Timeout
Timeout inside Promise

```

</details>

### Задача 3

```javascript
async function async1() {
    console.log('Async 1 start');
    await async2();
    console.log('Async 1 end');
}

async function async2() {
    console.log('Async 2');
}

console.log('Script start');

setTimeout(() => {
    console.log('setTimeout');
}, 0);

async1();

new Promise((resolve) => {
    console.log('Promise 1');
    resolve();
}).then(() => {
    console.log('Promise 2');
});

console.log('Script end');
```
<details>
<summary>Ответ на Задачу 3</summary>

```csharp
Script start
Async 1 start
Async 2
Promise 1
Script end
Async 1 end
Promise 2
setTimeout
```

</details>

### Задача 4

```javascript
console.log('1');

setTimeout(() => {
    console.log('2');
    Promise.resolve().then(() => {
        console.log('3');
    }).then(() => {
        console.log('4');
    });
    setTimeout(() => console.log('5'), 0);
}, 0);

Promise.resolve().then(() => console.log('6')).then(() => {
    console.log('7');
    setTimeout(() => console.log('8'), 0);
});

console.log('9');
```
<details>
<summary>Ответ на Задачу 4</summary>

```csharp
1
9
6
7
2
3
4
8
5
```

</details>

### Задача 5

```javascript
console.log('1');

setTimeout(() => {
    console.log('2');
    process.nextTick(() => {
        console.log('3');
    });
    new Promise((resolve) => {
        console.log('4');
        resolve();
    }).then(() => {
        console.log('5');
    });
});

new Promise((resolve) => {
    console.log('6');
    resolve();
}).then(() => {
    console.log('7');
});

process.nextTick(() => {
    console.log('8');
});

console.log('9');
```


Обратите внимание, что последняя задача включает `process.nextTick()`, который является специфичным для Node.js и имеет высший приоритет, чем промисы и таймеры, но для полноты картины и понимания различий в асинхронных операциях его стоит упомянуть. 


<details>
<summary>Ответ на Задачу 5</summary>

```csharp
1
6
9
8
7
2
4
3
5
```

</details>