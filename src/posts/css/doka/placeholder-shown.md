---
title: ":placeholder-shown"
name: placeholder-shown
author: ezhkov_d
co-authors:
designers:
contributors:
summary:
  - форма
  - плейсхолдер
  - валидация
---

## Кратко

Псевдокласс `:placeholder-shown` выбирает на странице все [`<input>`](/html/doka/input) или [`<textarea>`](/html/doka/textarea), у которых показывается плейсхолдер.

## Пример

```html
<input placeholder="Введите ваше имя">
```

```css
input {
  border: 1px solid black;
}

input:placeholder-shown {
  border-color: teal;
}
```

## Как это понять

Если полю ввода задан атрибут `placeholder` с каким-то значением, то внутри поля будет показана текстовая подсказка. Она пропадёт, если пользователь введёт хотя бы один символ. По сути псевдокласс `:placeholder-shown` будет применять стили к пустым полям ввода.

## Как пишется

```css
:placeholder-shown {
  color: teal;
}
```

## Подсказки

💡 Псевдокласс `:placeholder-shown` — это **не то же самое**, что псевдоэлемент [`::placeholder`](/css/doka/placeholder). Псевдокласс применит стили к самому полю ввода. А стили, примененные к псевдоэлементу [`::placeholder`](/css/doka/placeholder), изменят внешний вид текста подсказки, но никак не затронут само поле ввода.

## В работе

🛠 Этот псевдокласс можно использовать совместно с псевдоклассом [`:invalid`](/css/doka/invalid-valid) для стилизации некорректно заполненных полей ввода.

🛠 Иногда длина плейсхолдера больше ширины текстового поля. В результате плейсхолдер некрасиво обрезается. Можно использовать псевдокласс `:placeholder-shown`, чтобы сделать обрезку чуть симпатичнее:

```html
<p>Обычная обрезка</p>
<input type="text" placeholder="Можно искать по номеру телефона, фамилии или email">

<p>Красивая обрезка</p>
<input type="text" placeholder="Можно искать по номеру телефона, фамилии или email" class="ellipsis">
```

```css
.ellipsis:placeholder-shown {
  text-overflow: ellipsis;
}
```

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="html,result" data-user="ezhkov" data-slug-hash="WNoxXbW" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="placeholder-shown">
  <span>See the Pen <a href="https://codepen.io/ezhkov/pen/WNoxXbW">
  placeholder-shown</a> by Denis Ezhkov (<a href="https://codepen.io/ezhkov">@ezhkov</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

{% include "authors/ezhkov_d/author.njk" %}
