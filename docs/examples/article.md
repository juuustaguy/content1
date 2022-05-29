# Пример статьи

**Статья** — это расширенный материал, посвящённый определённому вопросу, с авторским мнением, примерами и рассуждениями. Например, «Руководство по флексбоксам» не только познакомит вас со спецификацией флексбокса, но и расскажет о раскладке в целом, научит делать её при помощи флексбоксов и покажет примеры из жизни — для этого у нас есть специальный раздел «На практике», где разработчики делятся своим личным опытом по теме.

Мы помечаем статью тегом _article_ в шапке.

Структура статьи примерно такова:

## Шапка

<details>
  <summary>Код шапки</summary>

```markdown
---
title: "Название статьи"
description: "Описание статьи для соцсетей, 160-200 символов"
cover:
  author: nick_name
  desktop: 'images/desktop.png'
  mobile: 'images/mobile.png'
  alt: 'Альтернативное описание для обложки'
authors:
  - Никнейм основного автора
contributors:
  - Никнеймы всех соавторов и контрибьюторов
editors:
  - Никнеймы всех редакторов
keywords:
  - Альтернативные теги для работы поиска
tags:
  - article
---

<!--
1. В description есть описание для соцсетей и поисковиков, не больше 200 символов
2. В authors есть ники авторов основного текста
3. В contributors перечислены ники всех соавторов и тех, кто работал над текстом (дописали «На практике»? Переписали блок? Вам сюда)
4. В keywords записаны ключевые слова для SEO: пишем сюда слова или фразы, которых нет в тексте статьи, но по ним могут искать этот материал
5. Удалены все пустые теги в шапке
6. Подпапка автора есть в папке _people/_
7. Демки лежат в подпапке _demos/_
-->
```

</details>

## Введение

Рассказываем, о чём будет эта статья, какие основные проблемы в ней поднимаются, зачем мы об этом пишем и т. п. Только не используйте заголовки «Введение» и «Заключение», придумайте что-нибудь менее формальное. Например: «Что это?» и «Что дальше?».

<details>
  <summary>Пример</summary>

Долгое время веб-интерфейсы были статичными — сайты разрабатывались и просматривались только на экранах мониторов стационарных компьютеров. Однако с десяток лет назад, совсем недавно по историческим меркам, у нас появилось огромное разнообразие экранов — от мобильных телефонов до телевизоров, — на которых мы можем взаимодействовать с сайтами. Так родилась необходимость в гибких системах раскладки.

Идея флексбоксов появилась ещё в 2009 году, и этот стандарт до сих пор развивается и прорабатывается. Основная идея флексов — гибкое распределение места между элементами, гибкая расстановка, выравнивание, гибкое управление. Ключевое слово — **гибкое**, что и отражено в названии (_flex — англ. гибко_).

</details>

## Основное содержание статьи

Детально описываем проблему и решения, рассказываем подробности, приводим примеры. Постарайтесь структурировать текст, добавить разделам понятные подзаголовки.

<details>
  <summary>Пример</summary>

```css
.container {
  display: flex;
}
```

Когда мы задаём какому-то элементу значение `flex` для свойства `display`, мы превращаем этот элемент в флекс-контейнер. Внутри него начинает действовать флекс-контекст, его дочерние элементы начинают подчиняться свойствам флексбокса.

Снаружи флекс-контейнер выглядит как блочный элемент — занимает всю ширину родителя, следующие за ним элементы в разметке переносятся на новую строку.

</details>

## Заключение

Здесь можно сделать выводы, а также дать дополнительные ссылки, подсказать, что ещё почитать по теме.

<details>
  <summary>Пример</summary>

1. [Как реально работает `flex-grow`](https://medium.com/p/557d406be844).
2. [Как реально работает `flex-shrink`](https://medium.com/p/c41e40767194).
3. [Песочница Флексбоксов](https://yoksel.github.io/flex-cheatsheet/).

</details>

## На практике

Мнения, рецепты и советы из личной практики разработчика, часто с примерами кода или демками. Если вы просто хотите добавить подсказку или дополнительную информацию — лучше добавьте её в тело статьи в соответствующий раздел.

Чтобы написать что-то в раздел «На практике», создайте в папке статьи подпапку _practice_, а в ней файл в формате Markdown, поименованный вашим ником.

<details>
  <summary>Пример</summary>

🛠 Раньше было затруднительно прижать футер к нижнему краю экрана вне зависимости от количества контента на странице. Приходилось идти на всякие ухищрения и городить костыли. Теперь с появлением флексов всё стало просто.

Оборачиваем всю страницу в блок, делаем его флекс-контейнером, внутрь вкладываем хэдер, мейн и футер. Родителю задаём `flex-direction: column` чтобы блоки встали друг под другом, а не в ряд, и `min-height: 100vh`, чтобы он занимал как минимум всю высоту экрана. Мейну задаём `flex: 1`, и вуаля! Центральный блок страницы будет всегда растягиваться на всё доступное свободное пространство. Из-за этого футер всегда будет прижиматься к нижнему краю страницы. При этом, если контента в мейне будет больше чем на один экран, то он растянется и подстроится, ничего не сломается.

</details>