---
title: "<style>"
name: style
author: grachev
co-authors:
  - ABatickaya
  - vladimir
designers:
contributors: skorobaeus
summary:
  - тэг
  - тег
  - style
  - <style>
  - стайл
  - стили в HTML
---

## Кратко

Внутри тега `<style>` можно задать параметры для CSS-стилей, которые применяются на странице. В общем, тут ты описываешь, как будут выглядеть заголовки, ссылки, обычный текст и другие элементы страницы.

## Пример

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      p {
        color: red;
      }
    </style>
  </head>
  <body>
    <p>This is my paragraph.</p>
  </body>
</html>
```

## Как пишется

Тег `<style>` помещается в элемент `<head>`, где находится информация, которую не видит пользователь.

```html
<head>
  <style type="text/css">
    ...;
  </style>
</head>
```

## Атрибуты

- `media` — укажите этот атрибут, чтобы один и тот же элемент на странице отображался по-разному на разных устройствах: например, телефоне или проекторе. К примеру, хочется, чтобы основной текст выглядел крупнее на проекторе, чем при просмотре на экране компьютера. Для этого добавь атрибут `media` со значением `"projection"` и пропиши размер шрифта, например, `font-size: 120%;`. Вот какие есть варианты устройств, можно указать несколько через запятую:
  - `all` — все устройства;
  - `braille` — устройства, основанные на системе Брайля, которая создана для слепых людей;
  - `handheld` — смартфоны и другие устройства с узким экраном;
  - `print` — принтер;
  - `screen` — стандартный экран компьютера — это значение по умолчанию;
  - `speech` — речевые синтезаторы, а также программы для воспроизведения текста вслух и речевые браузеры;
  - `projection` — проектор;
  - `tty` — телетайпы, терминалы, портативные устройства с ограниченными возможностями экрана;
  - `tv` — телевизор.
- `type` — укажи этот атрибут со значением `"text/css"`, чтобы старые браузеры правильно отобразили CSS-стили на странице: `type="text/css"`.

## Ещё примеры

Попробуем сделать основной заголовок на странице ещё крупнее, зададим шрифты без засечек и жёлтый цвет:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Кулинаный блог Марфы</title>
    <style type="text/css">
      h1 {
        font-size: 150%;
        font-family: Roboto, Arial, sans-serif;
        color: #ffd829;
      }
    </style>
  </head>
  <body>
    <h1>Как испечь настоящие круассаны</h1>
  </body>
</html>
```

{% demo "/style/header", "Стилизация заголовка", 160 %}

А в этом примере цвет и фон текста в абзаце будет меняться в зависимости от ширины экрана:

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      p {
        color: white;
        background-color: #1a5ad7;
      }
    </style>
    <style media="all and (max-width: 500px)">
      <!-- Будет работать на экранах шириной до 500px -- > p {
        color: #ed6742;
        background-color: #ffd829;
      }
    </style>
  </head>
  <body>
    <p>This is my paragraph.</p>
  </body>
</html>
```

{% demo "/style/p", "Стилизация параграфа", 90 %}

## В работе

{% include "authors/ABatickaya/in-work.njk" %}

🛠 Многие начинающие разработчики <i>грешат</i> тем, что прописывают стили прямо внутри HTML-разметки при помощи тега `style`. Так делать не нужно.

Один из принципов вёрстки: разделение содержимого и оформления. Содержимое это разметка страницы, а оформление, соответственно, CSS-стили.

Почему так? 🤔

Не редки ситуации, когда после вёрстки сайт <i>натягивается</i> на систему управления — CMS. Из HTML-разметки создаются шаблоны, для подтягивания данных из панели администратора используется PHP.

Как итог после таких манипуляций менять HTML будет достаточно проблематично и потребует дополнительных знаний. А вот доступ к стилям, если они вынесены в отдельный файл, у тебя останется. Таким образом можно будет полностью преобразить сайт, не меняя при этом разметки.

Если стили будут <i>зашиты</i> в HTML поменять внешний вид сайта будет также сложно, как изменить разметку.

🛠 Тег `style` можно использовать для быстрой проверки гипотез. Например, у тебя есть догадка, как решить задачу, но нет уверенности. Накидай варианты решения прямо в HTML и проверь в браузере.

Хотя удобнее делать то же самое в инструментах разработчика самого браузера 🤗

🛠 На самом деле тег `<style>` можно размещать вообще в любом месте страницы, не обязательно в `<head>` и это будет работать! Но делать так не стоит 🌚

{% include "authors/vladimir/in-work.njk" %}

🛠 Лайфхак: чтобы быстрее загружался сайт, особенно на телефоне или при медленном интернете, нужно тот код, который отвечает за отображение верхней части сайта, вставлять в `<head>` в формате `<style>/* Наш CSS-код */</style>`.

То есть туда можно встроить шапку сайта, верхние баннеры, заголовки — то, что отображается сразу при открытии. А всё, что ниже можно потом подгрузить через JavaScript после загрузки всей страницы. Так мы сразу показываем пользователю контент, он начинает его читать, а тем временем догружается нижняя часть сайта.

Больше информации о таком подходе можно найти по запросу «критический CSS».

{% include "authors/grachev/author.njk" %}
