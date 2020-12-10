---
title: Element.style
name: element-style
author: bespoyasov
co-authors:
designers:
contributors:
summary:
---

## Кратко

[`HTMLElement.style`](http://htmlelement.style) получает и устанавливает инлайновые стили элемента, то есть те, что записываются через атрибут `style`.

С помощью него можно управлять стилем элемента. [Специфичность]() этого свойства такая же, как у атрибута `style`.

## Как пишется

Чтобы получить значения инлайновых стилей с помощью свойства `style`, мы можем записать:

```jsx
const element = document.getElementById("someElement")
const inlineStyles = element.style
```

В этом случае в значение `inlineStyles` запишется объект [`CSSStyleDeclaration`](https://developer.mozilla.org/ru/docs/Web/API/CSSStyleDeclaration), который будет в себе содержать все инлайновые стили, которые содержит элемент `element`.

Чтобы задать стили для элемента, мы можем использовать несколько способов. Либо через `cssText`, чтобы указать несколько свойств разом. (Тем же эффектом обладает установка стиля через `setAttribute()`.) Либо через отдельные свойства в `style.[propertyName]`.

```jsx
// Следующие две записи работают одинаково
// и устанавливают несколько стилей в одном выражении:
element.style.cssText = "color: blue; border: 1px solid black"
element.setAttribute("style", "color:red; border: 1px solid blue;")

// Следующая — устанавливает значение определенного свойства,
// оставляя другие значения стиля нетронутыми:
element.style.color = "blue"
```

## Как понять

[`HTMLElement.style`](http://htmlelement.style) — это механизм для работы со стилями на элементе. С его помощью можно управлять отображением элементов в «рантайме», то есть во время выполнения скрипта.

Этот механизм позволяет «перетирать» стили, описанные в CSS-таблицах, так как специфичность стилей в атрибуте `style` выше (за иcключением стилей с `!important`).

Чтобы указать значение конкретного CSS-свойства, мы можем использовать одноимённое отображение в `style`:

```jsx
// Если мы хотим указать color:
element.style.color = "red" // или 'rgb(255,0,0)', или '#f00'

// Если хотим указать font-family:
element.style.fontFamily = "Arial"
```

Обратите внимание, что имена свойств в `style.[propertyName]` записываются в camelCase, в отличие от CSS-свойств, которые записываются через дефис.

Таким образом `font-family` превращается в `fontFamily`, а, например, `background-color` — в `backgroundColor`.

При сомнениях в том, как правильно называется то или иное свойство, воспользуйтесь списком соответствий:

<details class="article__table article__table_all-half">
  <summary>CSS-свойства в JS-нотации</summary>

| CSS                       | JavaScript           |
| ------------------------- | -------------------- |
| [background]()            | background           |
| [background-attachment]() | backgroundAttachment |
| [background-color]()      | backgroundColor      |
| [background-image]()      | backgroundImage      |
| [background-position]()   | backgroundPosition   |
| [background-repeat]()     | backgroundRepeat     |
| [border]()                | border               |
| [border-bottom]()         | borderBottom         |
| [border-bottom-color]()   | borderBottomColor    |
| [border-bottom-style]()   | borderBottomStyle    |
| [border-bottom-width]()   | borderBottomWidth    |
| [border-color]()          | borderColor          |
| [border-left]()           | borderLeft           |
| [border-left-color]()     | borderLeftColor      |
| [border-left-style]()     | borderLeftStyle      |
| [border-left-width]()     | borderLeftWidth      |
| [border-right]()          | borderRight          |
| [border-right-color]()    | borderRightColor     |
| [border-right-style]()    | borderRightStyle     |
| [border-right-width]()    | borderRightWidth     |
| [border-style]()          | borderStyle          |
| [border-top]()            | borderTop            |
| [border-top-color]()      | borderTopColor       |
| [border-top-style]()      | borderTopStyle       |
| [border-top-width]()      | borderTopWidth       |
| [border-width]()          | borderWidth          |
| [clear]()                 | clear                |
| [clip]()                  | clip                 |
| [color]()                 | color                |
| [cursor]()                | cursor               |
| [display]()               | display              |
| [filter]()                | filter               |
| [float]()                 | cssFloat             |
| [font]()                  | font                 |
| [font-family]()           | fontFamily           |
| [font-size]()             | fontSize             |
| [font-variant]()          | fontVariant          |
| [font-weight]()           | fontWeight           |
| [height]()                | height               |
| [left]()                  | left                 |
| [letter-spacing]()        | letterSpacing        |
| [line-height]()           | lineHeight           |
| [list-style]()            | listStyle            |
| [list-style-image]()      | listStyleImage       |
| [list-style-position]()   | listStylePosition    |
| [list-style-type]()       | listStyleType        |
| [margin]()                | margin               |
| [margin-bottom]()         | marginBottom         |
| [margin-left]()           | marginLeft           |
| [margin-right]()          | marginRight          |
| [margin-top]()            | marginTop            |
| [overflow]()              | overflow             |
| [padding]()               | padding              |
| [padding-bottom]()        | paddingBottom        |
| [padding-left]()          | paddingLeft          |
| [padding-right]()         | paddingRight         |
| [padding-top]()           | paddingTop           |
| [page-break-after]()      | pageBreakAfter       |
| [page-break-before]()     | pageBreakBefore      |
| [position]()              | position             |
| [stroke-dasharray]()      | strokeDasharray      |
| [stroke-dashoffset]()     | strokeDashoffset     |
| [stroke-width]()          | strokeWidth          |
| [text-align]()            | textAlign            |
| [text-decoration]()       | textDecoration       |
| [text-indent]()           | textIndent           |
| [text-transform]()        | textTransform        |
| [top]()                   | top                  |
| [vertical-align]()        | verticalAlign        |
| [visibility]()            | visibility           |
| [width]()                 | width                |

</details>

## В работе

В целом для управления стилями лучше использовать CSS. Можно использовать классы-модификаторы, чтобы придавать какие-то наборы стилей элементу.

Инлайновые стили имеют более высокую специфичность — их труднее переопределить, и это мешает нормальной работе со стилями элемента.

**Пример.** Мы пишем библиотеку, которая умеет красиво рисовать кнопки. Если мы установим цвет и размер кнопки с помощью инлайновых стилей, то пользователь библиотеки не сможет их легко поменять. Использовать такую библиотеку никто не захочет

Однако, есть некоторые случаи, когда манипуляция инлайн-стилями — это ок. Например, если мы хотим управлять отображением элемента точечно, и описывать это в CSS невозможно.

Представьте, что вы хотите сделать анимацию движения точки на экране так, чтобы движение было случайным. В CSS (пока что) этого сделать нельзя, только скриптами. И вот здесь изменение инлайновых стилей как раз кстати.

Для изменения таких стилей используется `HTMLElement.style`.

Используйте [`HTMLElement.style`](http://htmlelement.style), чтобы изменить или получить инлайновые стили элемента.

🛠 Чтобы переписать стиль элемента полностью, можно использовать `cssText` или `setAttribute`.

```jsx
element.style.cssText = "color: blue; border: 1px solid black"
element.setAttribute("style", "color:red; border: 1px solid blue;")
```

🛠 Чтобы обновить значение конкретного свойства, а остальные оставить нетронутыми, используйте `style.[propertyName]`:

```jsx
element.style.color = "red"
element.style.fontFamily = "Arial"
```

🛠 Чтобы сбросить значение, присвойте ему `null`.

```jsx
// Если у элемента прописано style="background-color: red; color: black;",
// то такая запись:
element.style.backgroundColor = null

// ...оставит только style="color: black;".
```

🛠 Численным свойствам, таким как `margin`, `padding`, `border-width` и другим, [следует](https://developer.mozilla.org/ru/docs/Web/API/HTMLElement/style#Получение_стиль-информации) указывать не только значение, но и единицу измерения:

```jsx
element.style.marginTop = "50px"
```

{% include "authors/bespoyasov/author.njk" %}
