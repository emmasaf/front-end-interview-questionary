# Batching в React

Batching (группировка обновлений) в React — это процесс, при котором несколько последовательных обновлений состояния объединяются в одно обновление, чтобы уменьшить количество ререндеров и, как следствие, повысить производительность приложения. Это одна из ключевых оптимизаций в React, позволяющая избежать излишней работы при множественных изменениях состояния.

## Batching в React 17 и ранее

В версиях React до 18 (включая 17), batching автоматически работал только в контексте обработчиков событий React. Это означает, что если вы вызывали несколько `setState` внутри обработчика событий, React объединял все эти обновления в один пакет и выполнял один ререндер.

Однако, если обновления состояния происходили в асинхронном коде (например, в промисах или `setTimeout`), React не применял автоматическое группирование.

## Изменения в React 18

React 18 внес значительные изменения в механизм batching, расширив его на асинхронные события, такие как обработчики промисов, `setTimeout`, `setInterval` и другие асинхронные API. Теперь, в React 18, все обновления состояния, независимо от того, где они происходят (в синхронном или асинхронном коде), по умолчанию группируются вместе, что приводит к уменьшению количества ререндеров и улучшению производительности.

### Как работает batching в React 18

React 18 внедряет новую функциональность, называемую "автоматическим batching", для всех обновлений, включая те, что происходят в результате асинхронных операций. Это было достигнуто благодаря новой архитектуре, известной как Concurrent Mode, которая позволяет React лучше управлять приоритетами обновлений и планированием их выполнения.

```javascript
button.addEventListener('click', () => {
  // Все эти обновления состояния будут сгруппированы в один ререндер в React 17 и ниже
  setCount(c => c + 1)
  setFlag(f => !f)
})
setTimeout(() => {
  // В React 18, эти обновления будут сгруппированы в один ререндер
  setCount(c => c + 1)
  setFlag(f => !f)
}, 100)
```
###Контроль над batching в React 18

Хотя автоматический batching — мощная оптимизация, иногда разработчикам может потребоваться выполнять обновления вне его контекста, чтобы гарантировать немедленное применение изменений. Для таких случаев React 18 предоставляет API flushSync, который позволяет выполнить обновления синхронно и немедленно.