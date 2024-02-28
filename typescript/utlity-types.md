Utility types в TypeScript предоставляют удобные инструменты для трансформации типов. Эти типы помогают в управлении и преобразовании существующих типов различными способами, делая код более гибким и уменьшая дублирование. Вот краткий обзор некоторых полезных утилитных типов:

1. **`Partial<Type>`**: Превращает все свойства типа `Type` в необязательные. Это полезно, когда вы хотите создать тип на основе другого, но с возможностью опускать некоторые из свойств.

   ```typescript
   interface Todo {
     title: string;
     description: string;
   }

   const updateTodo: Partial<Todo> = { title: "Clean room" };
   ```

2. **`Required<Type>`**: Превращает все необязательные свойства типа `Type` в обязательные. Это полезно для обеспечения того, чтобы все свойства были предоставлены.

   ```typescript
   interface Props {
     name?: string;
     age?: number;
   }

   const props: Required<Props> = { name: "John", age: 30 }; // Ошибка, если пропущено свойство
   ```

3. **`Readonly<Type>`**: Делает все свойства типа `Type` доступными только для чтения. Это предотвращает изменение свойств после их создания.

   ```typescript
   interface Todo {
     title: string;
   }

   const myTodo: Readonly<Todo> = { title: "Delete inactive users" };
   // myTodo.title = "Hello"; // Ошибка: нельзя изменить свойство, так как оно только для чтения
   ```

4. **`Record<Keys, Type>`**: Создает тип, который для набора свойств `Keys` использует тип `Type`. Это полезно для создания объектов с заранее известным набором ключей, но однотипными значениями.

   ```typescript
   interface PageInfo {
     title: string;
   }

   const pages: Record<string, PageInfo> = {
     home: { title: "Home" },
     about: { title: "About" },
     contact: { title: "Contact" },
   };
   ```

5. **`Pick<Type, Keys>`**: Создает тип, выбирая набор свойств `Keys` (литералы типов) из типа `Type`. Это полезно для создания типов с подмножеством свойств другого типа.

   ```typescript
   interface Todo {
     title: string;
     description: string;
     completed: boolean;
   }

   const displayTodo: Pick<Todo, "title" | "completed"> = {
     title: "Learn TypeScript",
     completed: false,
   };
   ```

6. **`Omit<Type, Keys>`**: Создает тип, исключая набор свойств `Keys` из типа `Type`. Это обратное `Pick` и полезно, когда нужно убрать некоторые свойства из типа.

   ```typescript
   interface Todo {
     title: string;
     description: string;
     completed: boolean;
   }

   const todoWithoutDescription: Omit<Todo, "description"> = {
     title: "Learn TypeScript",
     completed: false,
   };
   ```

7. **`Exclude<Type, ExcludedUnion>`**: Создает тип, исключая из `Type` те типы, которые присутствуют в `ExcludedUnion`. Это полезно для создания типов, исключая определенные значения.

8. **`Extract<Type, Union>`**: Создает тип, выбирая из `Type` те типы, которые присутствуют в `Union`. Это обратное `Exclude`.

9. **`NonNullable<Type>`**: Создает тип, исключая из `Type` `null` и `undefined`. Это полезно для обеспечения того, что переменная не может быть `null` или `undefined`.

Эти и другие utility types делают систему типов TypeScript мощным инструментом для управления типами данных в вашем коде, позволяя легко преобразовывать и адаптировать типы для различных задач.

В TypeScript тип `never` не является утилитой в прямом смысле, как `Partial` или `Readonly`, но он играет важную роль в системе типов. Тип `never` представляет тип значений, которые никогда не должны произойти. Вот несколько ключевых моментов, где тип `never` может быть использован:

1. **Функции, которые не возвращают значение из-за бесконечного цикла или всегда выбрасывают исключение:**

```typescript
function throwError(errorMsg: string): never {
  throw new Error(errorMsg);
}

function infiniteLoop(): never {
  while (true) {}
}
```

2. **Использование в исчерпывающих проверках (Exhaustiveness checking):**

Тип `never` может быть использован для обеспечения того, что все возможные варианты в конструкции `switch` или условных операторах были обработаны. Это особенно полезно при работе с объединениями типов или перечислениями:

```typescript
type Shapes = "circle" | "square" | "triangle";

function getShapeArea(shape: Shapes): number {
  switch (shape) {
    case "circle":
      // реализация для круга
      return Math.PI * Math.pow(10, 2); // Примерная площадь круга
    case "square":
      // реализация для квадрата
      return 10 * 10; // Примерная площадь квадрата
    case "triangle":
      // реализация для треугольника
      return (10 * 5) / 2; // Примерная площадь треугольника
    default:
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```

В примере выше, если `Shapes` будет расширен новым типом, например `"rectangle"`, TypeScript выдаст ошибку на строке с `_exhaustiveCheck`, так как не все возможные варианты были обработаны. Это помогает разработчику не забыть реализовать логику для всех возможных вариантов.

Таким образом, хотя `never` сам по себе не является утилитой в том смысле, в каком мы говорим о `Partial` или `Readonly`, он является важным инструментом в типизации TypeScript для обозначения недостижимых состояний и обеспечения безопасности типов через исчерпывающие проверки.