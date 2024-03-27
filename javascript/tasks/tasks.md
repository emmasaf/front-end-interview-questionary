Конечно, вот перечень популярных задач для собеседований без решений, включая темы JavaScript и алгоритмы:

### JavaScript:

1. **Последовательность Фибоначчи:**
   Напишите алгоритм на JavaScript, который генерирует первые n чисел последовательности Фибоначчи.

   ```javascript
   let num = 10
   let a = 0
   let b = 1
   let c = 0
   for (let i = 0; i < num; i++) {
     c = a + b
     a = b
     b = c
   }
   console.log(c)
   ```

2. **Реверс строки:**
   Создайте функцию на JavaScript, которая переворачивает строку. Например, "hello" станет "olleh".

```javascript
let str = 'hello'

// without methods
let newStr = ''
for (i = str.length - 1; i >= 0; i--) {
  newStr += str[i]
}
console.log(newStr)

// with methods
console.log(str.split('').reverse().join(''))
```

3. **Проверка на палиндром:**
   Напишите функцию на JavaScript, которая проверяет, является ли данная строка палиндромом.

```javascript
const str = 'repaper'
function checkIsPalidrome(str) {
  let arr = str.split('')
  let bool = false

  arr.forEach(el => {
    arr.reverse().forEach(cl => {
      if (el === cl) {
        bool = true
      } else {
        bool = false
      }
    })
  })

  return bool
}
console.log(checkIsPalidrome(str))
```

4. **Манипуляции с массивом:**
   Напишите функцию на JavaScript, которая перемешивает элементы массива случайным образом.

**Алгоритм Фишера-Йетс**

```javascript
function shuffleArray(array) {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[array[i], array[j]] = [array[j], array[i]]
    // обмен элементами
  }
  return array
}
```

5. **Array method filter**
   Напишите функцию Array.prototype.filter()

```javascript
Array.prototype.myFilter = function (callback) {
  let filteredArr = []

  for (let i = 0; i < this.length; i++) {
    if (callback(this[i], i, this)) {
      let newItem = this[i]
      filteredArr.push(newItem)
    }
  }

  return filteredArr
}

const array = [1, 2, 3, 4, 5]

let filteredArr = array.myFilter((el, index, arr) => {
  return el % 2 === 0
})

console.log(filteredArr)
```

6. **Array method forEach**
   Напишите функцию Array.prototype.forEach()

```javascript
Array.prototype.myForEach = function (callback) {
  for (let i = 0; i < this.length; i++) {
    callback(this[i], i, this)
  }
}

// Example usage:
const array = [1, 2, 3, 4, 5]

array.myForEach((element, index) => {
  console.log(`Element at index ${index}: ${element}`)
})
```

7. **Нахождение максимального числа:**
   Напишите функцию на JavaScript, которая находит максимальное число в массиве.

```javascript
function findMax(arr) {
  let num = arr[0]
  if (arr.length === 0) {
    return 'array is empty' // или выбросить ошибку,
    //   если массив пустой
  }
  for (el of arr) {
    if (el > num) {
      num = el
    }
  }

  return num
}

console.log(findMax([1, 2, 3, 4, 10, 5, 60, 8])) // Выведет 60
console.log(findMax([-1, -2, -3, -4])) // Выведет -1
console.log(findMax([])) // Выведет'array is empty'
```

8. **Нахождение максимальной длинны строки:**
   Задача: Найти максимальную длину подстроки, содержащей только повторяющиеся символы, и вывести эту подстроку.

```javascript
let example = 'ABCDDDEFGHIJKKKLMNOPQRSTUV'
let strArr = []
let fullArr = []
for (let i = 0; i < example.length; i++) {
  if (example[i] !== example[i + 1]) {
    strArr.push(example[i])
  } else {
    if (strArr.length > 0) {
      fullArr.push(strArr)
    }
    strArr = []
  }
}
let longestLength = Math.max(...fullArr.map(el => el.length))

let longestItem = fullArr
  .find(el => {
    return el.length === longestLength
  })
  .toString()

console.log(longestItem) // D,E,F,G,H,I,J
```

9. **Сортировка толыко нечетных цифр:**
   Задача: Отсортировать только нечетные числа в массиве, сохраняя порядок следования остальных элементов.

```javascript
let arr = [2, 5, 4, 7, 3, 9, 8]
let sortedOddNums = arr.filter(e => e % 2 !== 0).sort((a, b) => a - b)

let newArr = [...arr]
let count = 0
newArr.map((e, i) => {
  if (e % 2 !== 0) {
    newArr[i] = sortedOddNums[count]
    ++count
  }
  return newArr
})
console.log(newArr) // [2,3,4,5,7,9,8]
```

### Алгоритмы:

1. **Сортировка пузырьком:**
   Опишите алгоритм сортировки пузырьком и объясните его работу.

```javascript
function sort(arr) {
  let a
  let swapped = false
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > arr[i + 1]) {
      a = arr[i]
      arr[i] = arr[i + 1]
      arr[i + 1] = a
      swapped = true
      sort(arr)
    }
  }
  if (!swapped) {
    return arr
  }

  return arr
}

console.log(sort([5, 1, 2, 9, 6, 7, 11, 0, 13, 14, 63, 2]))
```

2. **Бинарный поиск:**
   Как работает алгоритм бинарного поиска? Напишите функцию бинарного поиска на JavaScript.

```javascript
function binarySearch(arr, num) {
  let low = 0
  let high = arr.length - 1

  while (low <= high) {
    // Использование Math.floor для получения целого индекса
    let mid = Math.floor((low + high) / 2)
    let guess = arr[mid]

    if (guess === num) {
      return mid // Найдено совпадение
    }
    if (guess > num) {
      high = mid - 1 // Смещаем верхнюю границу
    } else {
      low = mid + 1 // Смещаем нижнюю границу
    }
  }

  return -1 // Элемент не найден
}

let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]
let number = 14

console.log(binarySearch(arr, number)) // Должно вывести индекс 13
```

3. **Слияние двух отсортированных массивов:**
   Напишите функцию на JavaScript, которая объединяет два отсортированных массива в один.

4. **Вычисление факториала:**
   Напишите функцию на JavaScript, которая возвращает факториал заданного числа.

```javascript
function fact(num) {
  if (num == 0) return 1
  return num * fact(num - 1)
}
console.log(fact(5))
```

5. **Обход графа:**
   Объясните различные методы обхода графа, такие как обход в ширину (BFS) и в глубину (DFS).

Задачи также могут быть усложнены или адаптированы под конкретные случаи или ситуации, чтобы проверить навыки и способности кандидата в контексте реальных задач.

```

```
