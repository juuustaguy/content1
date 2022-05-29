---
title: "Поток документа"
description: "Объяснение одной из основных концепций вёрстки и её составляющих: контекста форматирования, схлопывания отступов и выхода из потока."
cover:
  author: kirakusto
  desktop: 'images/covers/desktop.svg'
  mobile: 'images/covers/mobile.svg'
  alt: 'Четыре аквариума с рыбами, один большой внизу с надписью block, три сверху рядом друг с другом (в строку) и надписью inline. Перед аквариумом растение'
authors:
  - ezhkov
editors:
  - tachisis
contributors:
  - skorobaeus
keywords:
  - раскладка
  - схлопывание
  - отступы
  - margin
  - контекст форматирования
  - флоат
  - float
  - абсолютное позиционирование
  - absolute
  - fixed
tags:
  - article
---

Поток — одно из важнейших базовых понятий в вёрстке. Это принцип организации элементов на странице при отсутствии стилей: если мы напишем HTML и не напишем CSS, то отображение в браузере будет предсказуемо благодаря тому, что мы абсолютно точно знаем, как браузер располагает элементы в потоке.

Даже если к странице не подключено никаких стилей, к каждому элементу всё равно будут применяться CSS-правила, «зашитые» в движке браузера. Благодаря этим правилам заголовок `<h1>` крупнее заголовка `<h2>`, а ссылки — синие и подчёркнутые. На основании этих правил **условно** все элементы на странице можно разделить на две категории: блочные (block) и строчные (inline). Например, `<div>` будет блочным, а `<span>` или `<a>` — строчным. Поменять стандартное поведение можно при помощи CSS-свойства [`display`](/css/display/).

Если вообще не применять никаких стилей, браузер формирует из элементов **нормальный поток**. Поведение блочных элементов в нормальном потоке отличается от поведения строчных.

## Контекст форматирования

Правила расположения строчных и блочных элементов в нормальном потоке называются **контекстом форматирования**. Блочные элементы участвуют в формировании **блочного** контекста форматирования. Строчные элементы формируют **строчный** контекст форматирования. Расположение элементов в контексте форматирования зависит от направления письма для конкретного языка. Например, тексты на европейских языках мы читаем и пишем слева направо сверху вниз. Это означает, что по умолчанию контекст форматирования располагает блочные элементы сверху вниз, а строчные — слева направо. Но, например, в случае с японским языком мы видим совершенно другую картину: блочные элементы будут располагаться слева направо, а строчные — сверху вниз.

Во всех примерах далее будет рассматриваться направление письма, характерное для европейских языков: слова — слева направо, блоки — сверху вниз. Но все те же объяснения можно применять и для другого направления письма.

## Блочные элементы в нормальном потоке

Блочные элементы в нормальном потоке располагаются друг под другом, всегда занимая всю доступную ширину родителя. Высота блочного элемента по умолчанию равна высоте его содержимого. Три абзаца, идущие друг за другом в HTML, будут располагаться точно в таком же порядке и на странице.

<iframe title="Блочные элементы в нормальном потоке" src="demos/normal/" height="550"></iframe>

Даже если ширина блочного элемента явно задана и позволяет разместить справа ещё один такой элемент, поток всё равно продолжит выстраивать их друг под другом.

<iframe title="Блочные элементы, ограниченные по ширине, в нормальном потоке" src="demos/normal-width/" height="570"></iframe>

Можно воспринимать блочный элемент как поплавок, который стремится всплыть на странице как можно выше. И всплывает до тех пор, пока не встретит на пути другой элемент или границу родителя.

<iframe title="Анимация блочных элементов в нормальном потоке" src="demos/normal-animated/" height="630"></iframe>

## Строчные элементы в нормальном потоке

Строчные элементы располагаются друг за другом, как слова в предложении. В зависимости от направления письма в конкретном языке элементы могут располагаться слева направо (например, в русском языке), справа налево (как, например, в иврите) и даже сверху вниз, как иероглифы в японском письме. Ширина и высота строчного элемента равна ширине и высоте содержимого. В отличие от блочного элемента, мы не можем управлять шириной и высотой строчного элемента через CSS. Несколько строчных элементов будут стремиться уместиться на одной строке, насколько хватает ширины родителя. Если ширины родителя не хватает, то лишний текст строчного элемента переносится на следующую строку.

<iframe title="Строчные элементы в нормальном потоке" src="demos/inline/" height="240"></iframe>

## Схлопывание и выпадение отступов

В рамках блочного контекста форматирования вертикальные расстояния между блоками задаются CSS-свойством [`margin`](/css/margin/). Если блоку задан нижний отступ, а следующему за ним — верхний, то можно ожидать, что итоговый отступ между блоками будет равен сумме этих двух отступов. Но в соответствии со спецификацией соприкасающиеся отступы «схлопываются». То есть как бы проваливаются один в другой. Итоговый отступ будет равен бо́льшему отступу из двух.

<iframe title="Схлопывание отступов" src="demos/margin-collapse-siblings/" height="650"></iframe>

Если первому дочернему элементу в блоке задан верхний отступ или последнему элементу — нижний, то эти отступы «выпадают» во внешний мир из своего родителя.

<iframe title="Выпадение отступов" src="demos/margin-collapse-empty/" height="590"></iframe>

Выпадение отступов из родителя можно предотвратить несколькими способами:

- Задать родителю вертикальный внутренний отступ [`padding-top`](/css/padding/) или [`padding-bottom`](/css/padding/) в зависимости от того, с какой стороны мы хотим предотвратить выпадение.
- Задать родителю верхнюю или нижнюю [рамку](/css/border/) по такой же логике. Рамка может быть прозрачной, главное, чтобы она была :)
- Задать родителю свойство [`overflow`](/css/overflow/) со значением, отличным от `visible`.
- Переопределить родителю свойство [`display`](/css/display/) на `flex` или `grid`.

## Выход из потока

Ранее мы выяснили, что все элементы по умолчанию находятся в нормальном потоке. Но это поведение можно поменять при помощи некоторых CSS-свойств. При изменении значений этих свойств элемент перестаёт взаимодействовать с остальными блоками в потоке. Говорят, что он «вышел из потока».

Тут нужно отметить, что элементы, вышедшие из потока, создают внутри себя своего рода мини-поток. Их дочерние элементы будут подчиняться правилам взаимодействия в потоке в пределах родителя.

### Обтекание при помощи [`float`](/css/float/)

Когда мы делаем элемент плавающим, он перестаёт взаимодействовать с другими элементами блочного контекста. При этом со строчным контекстом наш плавающий блок продолжает взаимодействовать. Текстовые элементы обтекают такой блок с одной из сторон.

<iframe title="Обтекание при помощи float" src="demos/float/" height="640"></iframe>

### Позиционирование элемента при помощи [`position`](/css/position/)

Если задать элементу абсолютное или фиксированное позиционирование, это также приводит к выходу из потока. Но только в этом случае наш элемент не участвует даже в строчном контексте.

<iframe title="Позиционирование элемента при помощи position" src="demos/absolute/" height="460"></iframe>

При абсолютном или фиксированном позиционировании элемент как бы поднимается над содержимым страницы, и становится «не виден» всем остальным блокам.