TypeScript предоставляет широкий спектр встроенных типов данных, а также позволяет создавать пользовательские типы. Вот обзор основных встроенных и пользовательских типов в TypeScript с примерами и некоторыми интересными фактами.

### Встроенные типы (Primitive Types)

1. **Boolean**: представляет логическое значение `true` или `false`.

   ```typescript
   let isDone: boolean = false
   ```

2. **Number**: включает в себя целые и числа с плавающей точкой.

   ```typescript
   let decimal: number = 6
   let hex: number = 0xf00d // Шестнадцатеричная
   let binary: number = 0b1010 // Двоичная
   let octal: number = 0o744 // Восьмеричная
   ```

3. **String**: представляет текстовые данные.

   ```typescript
   let color: string = 'blue'
   color = 'red' // Также поддерживаются одинарные кавычки
   ```

4. **Array**: типизированный массив элементов.

   ```typescript
   let list: number[] = [1, 2, 3]
   // Или с использованием обобщенного массива
   let listGeneric: Array<number> = [1, 2, 3]
   ```

5. **Tuple**: позволяет выразить массив с фиксированным числом элементов, которые могут быть разных типов.

   ```typescript
   let x: [string, number]
   x = ['hello', 10] // OK
   ```

6. **Enum**: позволяет определять набор именованных констант.

   ```typescript
   enum Color {
     Red,
     Green,
     Blue,
   }
   let c: Color = Color.Green
   ```

7. **Any**: отключает проверку типа, позволяя значениям быть любого типа.

   ```typescript
   let notSure: any = 4
   notSure = 'maybe a string instead'
   ```

8. **Void**: обратное от `any`, используется в случае отсутствия какого-либо типа.

   ```typescript
   function warnUser(): void {
     console.log('This is my warning message')
   }
   ```

9. **Null и Undefined**: оба представляют собой значения, которые отсутствуют.

   ```typescript
   let u: undefined = undefined
   let n: null = null
   ```

10. **Never**: представляет тип значений, которые никогда не возникают.
    ```typescript
    // Функция, которая выбрасывает исключение или постоянно выполняется, будет возвращать never
    function error(message: string): never {
      throw new Error(message)
    }
    ```
11. **Object**:В TypeScript, object является типом, который представляет непримитивное значение. В отличие от примитивных типов данных, таких как string, number, boolean, symbol, null, или undefined, тип object может быть использован для представления таких структур данных, как объекты, массивы, и функции.

    ```typescript
    let user: object = { name: 'Alice', age: 25 }

    user = { name: 'Bob' } // Допустимо
    user = [1, 2, 3] // Также допустимо, так как массивы в   JavaScript   являются объектами
    user = function () {
      console.log('Hello')
    } // Допустимо, функции тоже объекты
    ```

### Пользовательские типы

1. **Interfaces**: позволяют определять контракты в вашем коде и предоставляют способ определения пользовательских типов.

   ```typescript
   interface LabelledValue {
     label: string
   }

   function printLabel(labelledObj: LabelledValue) {
     console.log(labelledObj.label)
   }

   let myObj = { size: 10, label: 'Size 10 Object' }
   printLabel(myObj)
   ```

2. **Type Aliases**: предоставляют возможность дать типу имя.

   ```typescript
   type Name = string
   type NameResolver = () => string
   type NameOrResolver = Name | NameResolver
   function getName(n: NameOrResolver): Name {
     if (typeof n === 'string') {
       return n
     } else {
       return n()
     }
   }
   ```

3. **Union Types**: позволяют объекту быть одним из нескольких типов.

   ```typescript
   type StringOrNumber = string | number
   let sn: StringOrNumber = 'twenty'
   sn = 20 // также допустимо
   ```

4. **Intersection Types**: позволяют комбинировать несколько типов в один.

   ```typescript
   interface BusinessPartner {
     name: string
     credit: number
   }

   interface Identity {
     id: number
     name: string
   }

   type Employee = BusinessPartner & Identity
   // Employee теперь имеет и name, и credit, и id
   ```

### Интересные факты

- TypeScript способен выводить типы автоматически, что уменьшает необходимость явного указания типов.
- Enum в TypeScript может содержать строковые и числовые значения, что не типично для других языков программирования.
- TypeScript поддерживает расширенные типы, такие как `Mapped types`, `Conditional types`, и `Utility types`, которые предоставляют мощные инструменты для создания сложных типов на основе существующих.
- Даже если TypeScript и добавляет типизацию в JavaScript, весь TypeScript-код компилируется в чистый JavaScript, что обеспечивает его совместимость со всеми браузерами и средами выполнения JavaScript.
