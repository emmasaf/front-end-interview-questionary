`async` и `await` - это ключевые слова в JavaScript, которые позволяют работать с асинхронными операциями и промисами более удобно и читаемо. Вот краткое описание каждого из них:

1. **async**:

   - Ключевое слово `async` используется для определения асинхронной функции.
   - Асинхронная функция возвращает промис, который может быть либо выполнен, либо отклонен.
   - Внутри асинхронной функции можно использовать ключевое слово `await`, чтобы ждать завершения асинхронных операций, таких как вызовы функций, возвращающих промисы.

2. **await**:
   - Ключевое слово `await` используется внутри асинхронной функции для приостановки выполнения функции до тех пор, пока промис, переданный после `await`, не будет разрешен (выполнен или отклонен).
   - `await` может использоваться только внутри асинхронной функции.
   - Если промис, переданный после `await`, разрешен успешно, значение, возвращаемое промисом, будет доступно для использования. Если промис отклонен, будет выброшено исключение, которое можно обработать с помощью блока `try-catch`.

Пример использования `async` и `await`:

```javascript
async function fetchData() {
  try {
    // Ждем завершения асинхронной операции
    let response = await fetch('https://api.example.com/data')

    // Дождались успешного ответа, преобразуем данные в JSON
    let data = await response.json()

    // Возвращаем полученные данные
    return data
  } catch (error) {
    // Обрабатываем ошибку, если она произошла
    console.error('Error fetching data:', error)
    throw error
  }
}

// Вызываем асинхронную функцию и обрабатываем результат
fetchData()
  .then(data => {
    console.log('Data fetched successfully:', data)
  })
  .catch(error => {
    console.error('Failed to fetch data:', error)
  })
```

```javascript
async function hello() {
  let bool = false
  try {
    if (bool) {
      return await Promise.resolve('Hello')
    } else {
      throw 'bool is false' // Генерируем ошибку вместо return
    }
  } catch (e) {
    console.log(e)
    throw 'Bye'
  }
}

hello()
  .then(d => {
    console.log(d)
  })
  .catch(e => {
    console.log(e)
  })
```

В этом примере `fetchData()` - асинхронная функция, использующая `await` для ожидания ответа от сетевого запроса. Затем данные обрабатываются и возвращаются. В блоке `.then()` мы обрабатываем успешный результат, а в блоке `.catch()` - ошибку, если таковая возникла.


`async` и `await` - это новые конструкции в JavaScript, предназначенные для упрощения асинхронного программирования и работы с промисами.

<hr>

**Async/await** работает поверх событийного цикла (event loop) в JavaScript и предоставляет синтаксический сахар для работы с асинхронным кодом. Они делают код асинхронных функций более читабельным и поддерживаемым, скрывая сложности работы с промисами.

1. **Async**: Ключевое слово `async` используется для определения асинхронной функции. Функция, объявленная с ключевым словом `async`, возвращает промис. Если внутри асинхронной функции есть оператор `return`, JavaScript автоматически оборачивает его в промис и возвращает его.

2. **Await**: Ключевое слово `await` используется внутри асинхронной функции для приостановки выполнения функции до тех пор, пока промис, переданный после `await`, не завершится. Это позволяет писать асинхронный код так, как будто он синхронный, что улучшает его читаемость.

Вот пример, иллюстрирующий работу `async/await` вместе с событийным циклом:

```javascript
async function fetchData() {
    console.log('Fetching data...');

    // Ждем завершения запроса и получаем результат
    let result = await fakeAPIRequest();

    console.log('Data received:', result);
}

function fakeAPIRequest() {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve('Fake data');
        }, 2000);
    });
}

console.log('Before fetchData');

// Вызываем асинхронную функцию
fetchData();

console.log('After fetchData');

// Вывод:
// Before fetchData
// Fetching data...
// After fetchData
// Data received: Fake data
```

В примере выше, когда вызывается `fetchData()`, выполнение асинхронной функции приостанавливается на строке с `await fakeAPIRequest()`, пока `fakeAPIRequest()` не завершится (через 2 секунды в данном случае). В это время событийный цикл продолжает выполнение других задач. Когда промис завершается, выполнение функции `fetchData()` продолжается.

## Недостатки async/await

Асинхронные функции с async/await бывают очень удобными, но есть несколько замечаний, о которых полезно знать.

async/await позволяет вам писать код в синхронном стиле. Ключевое слово await блокирует приостанавливает выполнение promise-based функции до того момента, пока promise примет статус fulfilled. Это не блокирует код за пределами вашей асинхронной функции, тем не менее важно помнить, что внутри асинхронной функции поток выполнения блокируется.

Ваш код может стать медленнее за счёт большого количества awaited promises, которые идут один за другим. Каждый await должен дождаться выполнения предыдущего, тогда как на самом деле мы хотим, чтобы наши Promises выполнялись одновременно, как если бы мы не использовали async/await.

Есть подход, который позволяет обойти эту проблему — сохранить все выполняющиеся Promises в переменные, а уже после этого дожидаться (awaiting) их результата. Давайте посмотрим на несколько примеров.

```javascript
function timeoutPromise(interval) {
  return new Promise((resolve, reject) => {
    setTimeout(function () {
      resolve("done");
    }, interval);
  });
}

async function timeTest() {
  await timeoutPromise(3000);
  await timeoutPromise(3000);
  await timeoutPromise(3000);
}

```

Здесь мы просто ждём все три timeoutPromise() напрямую, блокируя выполнение на данного блока на 3 секунды при каждом вызове. Все последующие вызовы вынуждены ждать пока разрешится предыдущий. Если вы запустите первый пример (slow-async-await.html), то увидите alert сообщающий время выполнения около 9 секунд.

##### Во втором  примере, функция timeTest() выглядит так:

```javascript
async function timeTest() {
  const timeoutPromise1 = timeoutPromise(3000);
  const timeoutPromise2 = timeoutPromise(3000);
  const timeoutPromise3 = timeoutPromise(3000);

  await timeoutPromise1;
  await timeoutPromise2;
  await timeoutPromise3;
}
```

В данном случае мы храним три объекта Promise в переменных, каждый из которых может разрешиться независимо от других.

Ниже мы ожидаем разрешения промисов из объекта в результат. Так как они были запущенны одновременно, блокируя поток, то и разрешатся одновременно. Если вы запустите второй пример вы увидите alert, сообщающий время выполнения около 3 секунд.

```javascript
function timeoutPromise(interval,num) {
  return new Promise((resolve, reject) => {
    setTimeout(function () {
      resolve("done" + " " + num);
    }, interval);
  });
}

async function timeTest() {
  const timeoutPromise1 = timeoutPromise(3000,1);
  const timeoutPromise2 = timeoutPromise(3000,2);
  const timeoutPromise3 = timeoutPromise(3000,3);

  return Promise.all([timeoutPromise1, timeoutPromise2, timeoutPromise3])
    .then((values) => {
      return values;
    });
}

timeTest().then((d)=>{
    console.log(d)
})

```