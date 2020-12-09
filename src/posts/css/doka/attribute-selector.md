---
title: Селектор по атрибуту (div[attr=""] {})
name: attribute-selector
author: ezhkov_d
co-authors:
designers:
contributors:
summary:
  - селектор
  - атрибут
---

## Кратко

Селектор по атрибуту находит элемент на странице по значению либо по наличию атрибута.

## Пример

```html
<blockquote cite="А.С.Пушкин">
  Октябрь уж наступил — уж роща отряхает <br />
  Последние листы с нагих своих ветвей;
</blockquote>
```

```css
/* Если у цитаты указан атрибут с источником */
blockquote[cite] {
  background-color: lightgreen;
}
```

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="ezhkov" data-slug-hash="mdrJNzP" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="attribute selector (div[attr] {})">
  <span>See the Pen <a href="https://codepen.io/ezhkov/pen/mdrJNzP">
  attribute selector (div[attr] {})</a> by Denis Ezhkov (<a href="https://codepen.io/ezhkov">@ezhkov</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.sfo2.cdn.digitaloceanspaces.com/assets/embed/ei.js"></script>

## Как пишется

```css
/* Теги <a>, у которых есть атрибут title  */
a[title] {
  font-size: 2em;
}

/* Теги <a>, у которых атрибут href в точности равен https://example.org */
a[href="https://example.org"]
{
  background-color: blue;
}

/* Теги <a>, у которых в атрибут href входит подстрока example */
/* Этот селектор, например, применится для тега <a href="https://example.org">Ссылка</a> */
a[href*="example"] {
  font-size: 2em;
}

/* Теги <a>, у которых атрибут href ОКАНЧИВАЕТСЯ на .ru */
a[href$=".ru"] {
  font-style: italic;
}

/* <a> elements whose class attribute contains the word "logo" */
a[class~="logo"] {
  padding: 2px;
}
```

## Как это понять

Этот тип селектора помогает нам стилизовать элементы, опираясь либо на наличие самого атрибута, либо на его значение. Мы можем стилизовать элементы, опираясь на следующие варианты записи селектора:

`[attr]` — селектор выберет все элементы, у которых присуствует атрибут `attr`.

```html
<button disabled>OK</button>
```

```css
[disabled] {
  opacity: 0.5;
}
```

`[attr=value]` или `[attr="value"]` — селектор выберет все элементы, атрибут `attr` которых в точности равен `value`. Здесь и далее: значение атрибута можно писать в кавычках или без них. Если в значении атрибута есть пробелы, или знаки, отличные от цифр и букв, то значение нужно указывать в кавычках.

```html
<a href="#">Пустая ссылка</a> <a href="#one">Эта ссылка не стилизуется</a>
```

```css
[href="#"] {
  color: red;
}
```

`[attr~=value]` — селектор выбирает все элементы, значение атрибута `attr` которых — это перечень слов, разделенных пробелом, и среди этих слов есть такое, чьё значение равно `value`

```html
<blockquote cite="Александр Сергеевич Пушкин">...</blockquote>
<blockquote cite="Лев Николаевич Толстой ">...</blockquote>
```

```css
[cite~="Пушкин"] {
  border: 1px solid green;
}
```

`[attr|=value]` — селектор выберет все элементы, значение атрибута `attr` которых либо в точности равно `value`, либо начинается с `value`, за которым следует символ дефиса `-` (U+002D). Подобный вариант селектора чаще всего используется для выбора по коду языка (например `en-US` или `en-GB`)

```html
<div lang="en-us en-gb en-au en-nz">Hello World!</div>
<div lang="zh-CN">世界您好！</div>
<div lang="zh-TW">世界您好！</div>
```

```css
[lang|="en"] {
  /* Выберет первый div */
  color: blue;
}

[lang|="zh"] {
  /* Выберет два других div */
  color: red;
}
```

`[attr^=value]` — селектор выберет все элементы, значение атрибута `attr` которых **наичнается** с `value`

```html
<a href="https://secure.com/">Ссылка по протоколу HTTPS</a>
<a href="http://secure.com/">Ссылка по протоколу HTTP</a>
```

```css
[href^="https"]::after {
  content: "🔐";
  margin-left: 3px;
}
/* У ссылок по протоколу HTTPS справа отображается замок */
```

`[attr$=value]` — селектор выберет все элементы, значение атрибута `attr` которых **оканчивается** на `value`

```html
<a href="https://apple.com">Apple US</a>
<a href="https://apple.ru">Apple Russia</a>
<a href="https://apple.it">Apple Italy</a>
```

```css
[href$=".com"]::after {
  content: "🇺🇸";
}
[href$=".ru"]::after {
  content: "🇷🇺";
}
[href$=".it"]::after {
  content: "🇮🇹";
}
```

`[attr*=value]` — селектор выберет все элементы атрибут `attr` которых содержит в себе значение `value`

```html
<img src="/img/myadvertisingbanner.png" />
<img src="/img/other-advert-banner.png" />
<img src="/img/Advert-image.png" />
```

```css
img[src*="advert"] {
  display: none;
}
/**
 Спрячет две первых рекламных картинки. Оба изображения в атрибуте src содержат подстроку advert.
 Третья картинка не спрячется, потому что не совпал регистр символов
 (Advert и advert — это разные значения с точки зрения браузера)
**/
```

`[attr operator value i]` — если добавить в скобки после значения атрибута `i` или `I`, то браузер будет игнорировать регистр сиволов

```html
<img src="/img/myadvertisingbanner.png" />
<img src="/img/other-advert-banner.png" />
<img src="/img/Advert-image.png" />
```

```css
/* Теперь уберутся все три картинки */
img[src*="advert" i] {
  display: none;
}
```

## В работе

При помощи селектора по трибуту круто стилизовать ссылки, основываясь на значении атрибута `href`. Можно визуально разделять ссылки, ведущие на соседние страницы сайта, и ссылки, ведущие на другие сайты:

```html
<a href="http://mysite.ru/about">О нас</a>
<a href="http://mysite.ru/delivery">Доставка</a>
<a href="http://mysite.ru/contacts">Контакты</a>
<a href="http://medium.com/mysite-blog">Мы на Medium</a>
```

```css
[href^="http"]::after {
  content: "↗️"; /* Все ссылки с иконкой стрелочки */
}

[href*="/mysite.ru/"]::after {
  display: none; /* внутренние ссылки без иконок */
}
```

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="ezhkov" data-slug-hash="qBaaYJX" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="attribute selector (div[attr] {})">
  <span>See the Pen <a href="https://codepen.io/ezhkov/pen/qBaaYJX">
  attribute selector (div[attr] {})</a> by Denis Ezhkov (<a href="https://codepen.io/ezhkov">@ezhkov</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

{% include "authors/ezhkov_d/author.njk" %}
