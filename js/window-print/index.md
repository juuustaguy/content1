---
title: "`window.print()`"
description: "Открывает диалог печати текущей страницы"
authors:
  - nlopin
tags:
  - doka
---

## Кратко

Вызов метода `print` объекта `window` открывает стандартный диалог печати текущего страницы.

## Как пишется

```js
window.print()
```

## Как понять

При создании приложения мы можем предложить пользователю распечатать текущую страницу. Например, если показываем ему номер оформленного заказа, подтверждение бронирования и так далее.

Для этого достаточно написать несколько строк кода. Например, открывать системный диалог печати при нажатии на кнопку на экране:

```js
const printButton = document.getElementById('print-button')

printButton.addEventListener('click', function() {
  window.print()
})
```

Такой код делает то же самое, что и системное меню _File → Print_.

По умолчанию страница печатается в том виде, какой её видно на экране — цветная, с шапкой, футером, меню. Печатную версию сайта можно настроить с помощью CSS-директивы [`@media print`](/css/media/) и скрыть ненужные блоки.

Если на странице есть [`<iframe>`](/html/iframe/), то вызов `window.print()` внутри него напечатает только этот айфрейм, а не все содержимое вкладки браузера:

<iframe title="Программный вызов печати" src="demos/index.html" height="300"></iframe>