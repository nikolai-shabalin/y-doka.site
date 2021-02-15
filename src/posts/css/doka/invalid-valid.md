---
title: ":invalid / :valid"
name: invalid-valid
author: ezhkov_d
co-authors:
designers:
contributors:
summary:
- invalid
- valid
- валидация
- форма
---

## Кратко

Псевдоклассы используются для стилизации полей формы:

- `:invalid` для заполненых с ошибкой;
- `:valid` для заполненных верно.

## Пример

```html
<form>
  <div class="form-row">
    <label for="first-name">Имя:</label>
    <input type="text" name="first-name" id="first-name" required>
    <span class="validity-icon"></span>
  </div>
  <div class="form-row">
    <label for="email">E-mail:</label>
    <input type="email" name="email" id="email">
    <span class="validity-icon"></span>
  </div>
  <div class="form-row">
    <label>
      <input type="checkbox" name="agree" id="agree" required>
      Я согласен с политикой обработки персональных данных
    </label>
  </div>
  <div class="form-row">
    <button type="submit">Отправить</button>
  </div>
</form>
```

```css
input:invalid {
  border: 2px solid red;
}

input:invalid + .validity-icon::before {
  content: '✖';
  color: red;
}

input:valid + .validity-icon::before {
  content: '✓';
  color: green;
}

[type=checkbox]:invalid {
  outline: 2px solid red;
  outline-offset: 2px;
}
```

## Как это понять

Часто на сайтах мы встречаем формы. Это могут быть формы регистрации или формы оплаты покупки в интернет-магазине. Часть полей ввода и других элементов управления на этих формах могут иметь особые требования к заполнению. Некоторые поля ввода должны быть обязательно заполнены, некоторые — иметь определённый формат данных (например, текст в поле с типом `email` должен содержать знак `@` и точку).

Чтобы показать, что поле ввода заполнено корректно, к нему можно применить особые стили, используя псевдокласс `:valid`. Аналогично, для не корректно заполненного поля мы можем применить особые стили, используя псевдокласс `:invalid`.

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="css,result" data-user="ezhkov" data-slug-hash="ZEpdbje" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title=":invalid / :valid">
  <span>See the Pen <a href="https://codepen.io/ezhkov/pen/ZEpdbje">
  :invalid / :valid</a> by Denis Ezhkov (<a href="https://codepen.io/ezhkov">@ezhkov</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

На примере выше можно увидеть пару моментов:

- поле ввода имени и чекбокс обязательны к заполнению, но не заполнены, поэтому псевдокласс `:invalid` применяется к ним сразу же.
- поле ввода электронной почты не обязателен к заполнению, поэтому к нему сразу же применён псевдокласс `:valid`.

Но если ввести в поле хотя бы один символ, браузер запускает проверку на корректность ввода email (из-за того, что мы указали `type="email"`) и применяет псевдокласс `:invalid` до тех пор, пока не будет введён корректный адрес электронной почты.

## Как пишется

```css
:invalid { ... }

:valid { ... }
```

## Подсказки

💡 Если на форме есть группа связанных радиокнопок (`<input type="radio">`), то, если хотя бы у одной есть [атрибут `required`](/html/doka/form/#атрибуты), псевдокласс `:invalid` будет применён ко всем радиокнопкам сразу.

## В работе

В настоящий момент стили для псевдокласса `:invalid` применяются к невалидному полю сразу же, что не всегда удобно. Было бы круто, если бы валидация включалась только если пользователь начал что-то вводить, но к сожалению, пока нет такой возможности «из коробки».

В будущих версиях спецификации CSS должен появиться псевдокласс `:user-invalid`, который задуман как раз для целей, описанных выше. То есть, он будет применяться, например, к полю ввода только после того, как пользователь начал там что-то писать.

Но это пока перспективы, а что же можно сделать сейчас? В настоящий момент добиться похожего поведения можно только для полей ввода. При этом нужно выполнить два условия:

- добавить атрибут `placeholder`;
- использовать псевдокласс [`:placeholder-shown`](/css/doka/placeholder-shown).

```html
<form>
  <div class="form-row">
    <label for="first-name">Имя:</label>
    <input type="text" name="first-name" id="first-name" required placeholder="Например, Пётр">
    <span class="validity-icon"></span>
  </div>
  <div class="form-row">
    <label for="email">E-mail:</label>
    <input type="email" name="email" id="email" placeholder="Например, mymail@gmail.com">
    <span class="validity-icon"></span>
  </div>
  <div class="form-row">
    <button type="submit">Отправить</button>
  </div>
</form>
```

```css
input:invalid {
  border: 2px solid red;
}

input:invalid:placeholder-shown {
  border-color: black;
}

input:invalid:placeholder-shown + .validity-icon::before,
input:valid:placeholder-shown + .validity-icon::before {
  visibility: hidden;
}
```

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="css,result" data-user="ezhkov" data-slug-hash="GRNKxvy" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title=":invalid / :valid">
  <span>See the Pen <a href="https://codepen.io/ezhkov/pen/GRNKxvy">
  :invalid / :valid</a> by Denis Ezhkov (<a href="https://codepen.io/ezhkov">@ezhkov</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

{% include "authors/ezhkov_d/author.njk" %}
