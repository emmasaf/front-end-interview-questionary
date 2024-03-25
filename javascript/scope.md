В JavaScript существует несколько типов областей видимости (scope), где могут храниться данные. Вот основные виды областей видимости в JavaScript:

1. **Global scope (глобальная область видимости)**:
   - Глобальная область видимости охватывает всю программу.
   - Переменные, объявленные вне всех функций, доступны из любой части кода.

2. **Function scope (область видимости функции)**:
   - Переменные, объявленные внутри функции, доступны только внутри этой функции.
   - Переменные, объявленные с использованием ключевого слова `var`, имеют область видимости функции.
   - С другой стороны, переменные, объявленные с использованием `let` и `const`, имеют блочную область видимости (см. ниже), а не только область видимости функции.

3. **Block scope (блочная область видимости)**:
   - Переменные, объявленные внутри блока кода (например, внутри `{}`), доступны только внутри этого блока.
   - Появилась с появлением `let` и `const` в ECMAScript 6 (ES6).

4. **Module scope (область видимости модуля)**:
   - В ES6 появилась новая область видимости - область видимости модуля.
   - Переменные, объявленные внутри модуля (файла), доступны только внутри этого модуля, если не экспортированы.

Примеры:

```javascript
// Global scope
var globalVariable = 10;

function myFunction() {
  // Function scope
  var functionScopedVariable = 20;

  if (true) {
    // Block scope (ES6+)
    let blockScopedVariable = 30;
    const constantInBlockScope = 40;
    console.log(blockScopedVariable); // 30
  }

  // console.log(blockScopedVariable); // Error: blockScopedVariable is not defined
}

// console.log(functionScopedVariable); // Error: functionScopedVariable is not defined
// console.log(blockScopedVariable); // Error: blockScopedVariable is not defined
```

В этом примере `globalVariable` доступна из любой части кода, `functionScopedVariable` доступна только внутри функции `myFunction`, а `blockScopedVariable` и `constantInBlockScope` доступны только внутри блока `if`.