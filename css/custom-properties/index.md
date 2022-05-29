---
title: "Кастомные свойства"
description: "Удобный способ сохранить повторяющееся значение и потом использовать его в разных местах кода. Как переменные в языках программирования."
cover:
  author: kirakusto
  desktop: 'images/covers/desktop.svg'
  mobile: 'images/covers/mobile.svg'
  alt: 'Кран строит дома: маленький, средний и большой'
authors:
  - ezhkov
contributors:
  - skorobaeus
editors:
  - tachisis
keywords:
  - var
  - root
  - custom properties
tags:
  - doka
---

Давайте предположим, что у нас есть веб-страница, на которой много элементов с текстом одного и того же цвета. Дизайнер создал фирменный стиль, руководство утвердило, мы начали верстать. Наш CSS мог бы выглядеть примерно так:

```css
.header-primary {
  font-size: 2em;
  color: #18191C;
  margin-bottom: .5em;
}

.header-secondary {
  font-size: 1.6em;
  color: #18191C;
}

.text {
  font-family: "Open Sans", sans-serif;
  color: #18191C;
  margin-top: 0;
}

.form-input {
  font-size: 1em;
  color: #18191C;
  padding-top: 4px;
  padding-bottom: 4px;
}
```

Конкретный оттенок чёрного `#18191C` используется по всей странице в совершенно разных элементах: заголовках, тексте, кнопках, полях ввода. Кажется, что это не должно создавать никаких проблем, но на самом деле есть ряд неудобств, которых хотелось бы избежать.

Во-первых, если завтра по какой-то причине нужно будет немного изменить оттенок чёрного, придётся это делать во многих местах.

Во-вторых, приходится копировать и вставлять [HEX-значение](/css/web-colors/) цвета, ну или запоминать первые несколько символов, чтобы текстовый редактор сумел нам подсказать.

Все эти неудобства уходят, если использовать **CSS-переменные**. Чаще их называют **кастомные свойства**.

## Что это и как пишется?

Кастомное свойство — это произвольное свойство с определённым значением. Оно отличается от стандартного CSS-свойства способом записи. Чтобы применить кастомное свойство, нужно передать его в CSS-функцию `var()`.

Стандартное свойство:

```css
.list-item {
  margin-left: 10px;
}

.list-item .link {
  margin-left: 10px;
}
```

Кастомное свойство:

```css
.list {
  --element-gap: 10px;
}

.list-item {
  margin-left: var(--element-gap);
}

.list-item .link {
  margin-left: var(--element-gap);
}
```

Кастомных свойств не существует в спецификации CSS. По способам применения они больше всего похожи на переменные в языках программирования. Если мы определили кастомное свойство, то в дальнейшем можно его переиспользовать сколько угодно раз.

## Наследование кастомных свойств

Как и обычные наследуемые свойства (например, `font-size`), кастомные свойства наследуются вниз по дереву. Определив переменную в родительском элементе, мы сможем переиспользовать её в любом дочернем элементе:

```html
<div class="cards">
  <div class="card">
    <h2 class="card-header">Тариф «Бесплатный»</h2>
    <ul class="benefits">
      <li class="benefits-item">1 пользователь</li>
      <li class="benefits-item">2 ГБ трафика</li>
    </ul>
  </div>
  <div class="card card--primary">
    <h2 class="card-header">Тариф «Популярный»</h2>
    <ul class="benefits">
      <li class="benefits-item">До 5 пользователей</li>
      <li class="benefits-item">20 ГБ трафика</li>
    </ul>
  </div>
</div>
```

```css
.cards {
  --main-color: #E6E6E6;
}

.card-header, .benefits-item {
  color: var(--main-color);
}

.card--primary {
  --main-color: black;
}
```

В примере мы переопределяем значение переменной для карточки с классом `.card--primary`, и все дочерние элементы меняют цвет. В этом и кроется основная мощь CSS-переменных. Изменяем значение в одном месте, а затрагиваем все места, где используется переменная.

<iframe title="Наследование кастомных свойств" src="demos/index/" height="340"></iframe>

Но что, если мы заранее не знаем, какой будет вложенность элементов? Можно задать кастомное свойство корневому элементу страницы `<html>`, и тогда оно гарантированно будет доступно в каждом элементе страницы. Но обычно для этих целей используют псевдокласс [`:root`](/css/root/), который является псевдонимом для `<html>`:

```css
:root {
  --gap-small: 10px;
  --gap-medium: 20px;
}
```

В первом примере цвет `#18191C` используется в самых разных элементах страницы. Мы можем назначить этот цвет кастомному свойству с осмысленным названием и дальше везде использовать именно это свойство. Очень удобно, ведь запомнить название свойства проще, чем HEX-код цвета:

```css
:root {
  --text-color: #18191C;
}

.header-primary {
  font-size: 2em;
  color: var(--text-color);
  margin-bottom: .5em;
}

.header-secondary {
  font-size: 1.6em;
  color: var(--text-color);
}

.text {
  font-family: "Open Sans", sans-serif;
  color: var(--text-color);
  margin-top: 0;
}

.form-input {
  font-size: 1em;
  color: var(--text-color);
  padding-top: 4px;
  padding-bottom: 4px;
}
```

Обратите внимание: кастомные свойства, объявленные в `:root`, тоже при необходимости могут быть переопределены:

```css
:root {
  --main-color: #18191C;
}

.article-promo {
  --main-color: #272822;
}
```

## Запасные значения

Если по какой-то причине значение переменной не определено, мы можем передавать в функцию `var()` второй параметр, который станет «запасным» значением. По аналогии со свойством [`font-family`](/css/font-family/). Если не найдено первое значение, браузер будет подставлять следующее:

```css
.section-title {
  color: var(--primary-color, #222);
}
```

В качестве запасного значения может быть передана функция `var()`, которая в свою очередь также может иметь запасное значение:

```css
.section-title {
  color: var(--primary-color, var(--black, #222));
}
```

## Корректность использования

У стандартных CSS-свойств типы значений предопределены, поэтому браузер понимает, правильно ли мы употребляем значение.

Используем HEX-запись цвета для свойства `color`. Это правильно.

```css
.valid-value {
  color: #272822;
}
```

Используем размерную величину для свойства `color`. Это неправильно.

```css
.invalid-value {
  color: 10px;
}
```

У кастомных свойств всё иначе. Значения вычисляются в браузере непосредственно перед отрисовкой страницы. Браузер заранее не знает, в каком месте будет применено кастомное свойство, поэтому по умолчанию считает любую переменную корректной. И только после подстановки значения свойству браузер узнаёт, правильно ли мы его применили. Для такого поведения есть причины, рассмотрим пример:

```css
:root {
  --big-header: 20px;
}

.promo-header {
  color: var(--big-header);
}
```

В этом примере браузер подставляет значение переменной `--big-header` (`20px`) в качестве значения свойства `color`, но это не имеет смысла. В такой ситуации браузер делает две вещи:

- Проверяет, является ли свойство наследуемым. Если да, то значение для него ищется выше по дереву.
- Если свойство не наследуемое или значение не найдено выше по дереву, то берётся начальное значение по умолчанию (`initial`). Для свойства `color` у заголовка это будет `black`.

## Использование в JavaScript

В JavaScript значения кастомных свойств используются точно так же, как и значения стандартных CSS-свойств.

Чтобы получить значение:

```js
element.style.getPropertyValue("--main-color")
```

Чтобы задать значение:

```js
element.style.setProperty("--translate", `${currentScroll}px`)
```

## Подсказки

Кастомные свойства можно использовать в любых других функциях. Например, в функции [`calc()`](/css/calc/).

```css
.logo {
  display: inline-block;
  width: calc(var(--size, 1) * 15px);
  height: calc(var(--size, 1) * 15px);
}

.logo--small {
  --size: 2;
}

.logo--medium {
  --size: 3;
}

.logo--big {
  --size: 4;
}
```

В этом примере мы задали значение по умолчанию, равное `1`. Если будет использоваться только класс `.logo`, браузер установит `--size: 1`. Если будет применён один из классов-модификаторов, значение `--size` будет переопределено, и ширина и высота элемента будут пересчитаны благодаря использованию [`calc()`](/css/calc/).

А вот так можно применить CSS-переменную в функции [`linear-gradient`](/css/linear-gradient/).

```css
.element {
  --angle: 45deg;
  background-image: linear-gradient(var(--angle), #235ad1, #23d1a8);
}

.element--inverted {
  --angle: -45deg;
}
```