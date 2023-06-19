---
layout: default
---

<h2 id="toc">Tabla de contenido</h2>

<div markdown="1">
### [HTML](#html)

- [Sintaxis](#html-syntax)
- [HTML5 doctype](#html5-doctype)
- [Atributo de idioma](#language-attribute)
- [Modo de compatibilidad con IE](#ie-compatibility-mode)
- [Codificación de caracteres](#character-encoding)
- [Vinculación de archivos CSS y JavaScript](#css-and-javascript-includes)
- [Practicidad sobre pureza](#practicality-over-purity)
- [Orden de los atributos](#attribute-order)
- [Atributos booleanos](#boolean-attributes)
- [Reducir las etiquetas](#reduce-markup)
- [Preferencias del editor](#editor-preferences)
</div>

<div markdown="1">
### [CSS](#css)

- [CSS syntax](#css-syntax)
- [Declaration order](#declaration-order)
- [Colors](#colors)
- [Logical properties](#logical-properties)
- [Avoid @import`s](#avoid-imports)
- [Media query placement](#media-query-placement)
- [Single declarations](#single-declarations)
- [Shorthand notation](#shorthand-notation)
- [Nesting in preprocessors](#nesting-in-preprocessors)
- [Operators in preprocessors](#operators-in-preprocessors)
- [Comments](#comments)
- [Class names](#class-names)
- [Selectors](#selectors)
- [Child and descendant selectors](#child-and-descendant-selectors)
- [Organization](#organization)
</div>

## Regla de oro

Cumpla los siguientes estándares, o los suyos, en todo momento. No importa si el error es pequeño o grande, evite lo que es incorrecto. Para adiciones o contribuciones a esta Guía de código, [cree un issue en GitHub](https://github.com/mdo/code-guide/issues/new).

> Cada línea de código debe parecer escrita por una sola persona, no importa el número de contribuyentes que tenga el proyecto.

## HTML

<div markdown="1">
### Sintaxis
{: #html-syntax }

- No use mayúsculas en las etiquetas HTML, incluido el `doctype`.
- Use dos espacios en blanco para formatear y definir niveles entre las etiquetas HTML—es la única forma de garantizar que el código se renderice de la misma manera en cualquier entorno.
- Elementos anidados deben indentarse una vez (con dos espacios).
- Utilice siempre comillas dobles, nunca comillas simples para los atributos.
- No incluya una barra inclinada final en los elementos de cierre automático—la [especificación de HTML5](https://html.spec.whatwg.org/multipage/syntax.html#syntax-start-tag) nos dice que es opcional.
- No omita las etiquetas de cierre opcionales (p. ej. `</li>` o `</body>`).
</div>

```html
<!doctype html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```

<div markdown="1">
### HTML5 doctype
{: #html5-doctype }

Utilice el [modo estándar](https://developer.mozilla.org/es/docs/Web/HTML/Quirks_Mode_and_Standards_Mode) para una representación más consistente en todos los navegadores declarando el `doctype` simple al comienzo de cada página HTML. Manteniendo la sintaxis sugerida use siempre minúsculas.

</div>

```html
<!doctype html>
<html>
  <head>
    <!-- ... -->
  </head>
  <body>
    <!-- ... -->
  </body>
</html>
```

<div markdown="1">
### Atributo de idioma
{: #language-attribute }

De acuerdo a las especificaciones HTML5:

> Se recomienda a los autores a especificar el atributo lang en el elemento html raíz, dando el idioma del documento. Esto ayuda a las herramientas de síntesis de voz a determinar qué pronunciaciones usar y a las herramientas de traducción a determinar qué reglas usar, etc.

Lea más información sobre el atributo `lang` en las [especificaciones de HTML5](https://html.spec.whatwg.org/multipage/semantics.html#the-html-element). Dirígase a la <abbr title="Internet Assigned Numbers Authority">IANA</abbr> para obtener una [lista de códigos de idioma](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry).
</div>

```html
<html lang="es">
  <!-- ... -->
</html>
```

<div markdown="1">
### Modo de compatibilidad con IE
{: #ie-compatibility-mode }

No es necesario incluir la etiqueta `<meta>` para compatibilidad de documentos de Internet Explorer en estos días, a menos que necesite soporte para IE10 y versiones anteriores. La etiqueta se eliminó en IE11 y no se usa en Microsoft Edge (heredado o no).

Para más información, [lea este increíble artículo de Stack Overflow](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do).
</div>

```html
<!-- IE10 y versiones anteriores solamente -->
<meta http-equiv="x-ua-compatible" content="ie=edge">
```

<div markdown="1">
### Codificación de caracteres
{: #character-encoding }

Garantice una representación adecuada del contenido declarando una codificación de caracteres explícita. Esto también le permite usar caracteres regulares en lugar de sus entidades HTML, como `—` en lugar de `&emdash;`, siempre que su codificación coincida con la del documento. Para algunos caracteres XML reservados, como ampersand, espacios de no separación, menor/mayor que y comillas, es posible que aún necesite usar las entidades HTML.

UTF-8 es la codificación recomendada.
</div>

```html
<head>
  <meta charset="utf-8">
</head>
<body>
  <p>Para usar un guión largo como — no es requerido una entidad HTML.</p>
</body>
```

<div markdown="1">
### Vinculación de archivos CSS y JavaScript
{: #css-and-javascript-includes }

Según la especificación de HTML5, normalmente no es necesario especificar el atributo `type` cuando se incluyen archivos CSS y JavaScript, ya que `text/css` y `text/javascript` son sus respectivos valores predeterminados.

####  Especificaciones HTML5

- [Usando link](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [Usando style](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [Usando script](https://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)
</div>

```html
<!-- CSS externo -->
<link rel="stylesheet" href="code-guide.css">

<!-- CS dentro del documento -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

<div markdown="1">
### Practicidad sobre pureza
{: #practicality-over-purity }

Esfuércese por mantener los estándares y semántica HTML, pero no a costa de la practicidad. Use la menor cantidad de marcado con la menor cantidad de complejidades, siempre que sea posible.
</div>

```html
<!-- Correcto -->
<button>...</button>

<!-- Incorrecto -->
<div class="btn" onClick="...">...</div>
```

<div markdown="1">
### Orden de los atributos
{: #attribute-order }

Los atributos HTML deben seguir este orden particular para facilitar la lectura del código.

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`, `value`
- `title`, `alt`
- `role`, `aria-*`
- `tabindex`
- `style`

Los atributos que más se usan para identificar elementos deben ir primero— atributos `class`, `id`, `name` y `data`. Los atributos misceláneos exclusivos de elementos específicos ocupan el segundo lugar, seguidos de los atributos relacionados con la accesibilidad y el estilo.
</div>

```html
<a class="..." id="..." data-toggle="modal" href="#">
  Link de ejemplo
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

<div markdown="1">
### Atributos booleanos
{: #boolean-attributes }

Un atributo booleano es aquel que no necesita un valor declarado. XHTML requería que declarara un valor, pero HTML5 no tiene tal requisito.

Para más información, consulte la [sección de WhatWG sobre atributos booleanos](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes)

> La presencia de un atributo booleano en un elemento representa el valor verdadero y la ausencia del atributo representa el valor falso.

Si <em>debe</em> incluir el valor del atributo y **no es necesario**, siga esta guía de WhatWG:

> Si el atributo está presente, su valor debe ser la cadena vacía o […] el nombre canónico del atributo, sin espacios en blanco al principio o al final.

En resumen, **no añada un valor**.
</div>

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

<div markdown="1">
### Reducir las etiquetas
{: #reduce-markup }

Siempre que sea posible, evite los elementos padres redundantes al escribir HTML. Muchas veces esto requiere iteración y refactorización de código, pero produce menos HTML.
</div>

```html
<!-- No tan bueno -->
<span class="avatar">
  <img src="...">
</span>

<!-- Mejor -->
<img class="avatar" src="...">
```

<div markdown="1">
### Preferencias del editor
{: #editor-preferences }

Pepare su editor con las siguientes configuraciones para evitar inconsistencias de código comunes y diferencias:

- Usar tabulaciones suaves con dos espacios.
- Eliminar el espacio en blaco al final de cada línea al guardar.
- Establecer la codificación en UTF-8.
- Agregar una nueva línea en blanco al final de cada archivos.

Considere documentar y aplicar estas preferencias al archivo `.editorconfig` de su proyecto. Para ver un ejemplo, revise [el de Bootstrap](https://github.com/twbs/bootstrap/blob/main/.editorconfig). Obtenga más información [sobre EditorConfig](https://editorconfig.org).
</div>

## CSS

<div markdown="1">
### Syntax
{: #css-syntax }

- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Use space-separated values for color properties (e.g., `color: rgb(0 0 0 / .5)`). [See the Colors section for more information.](#colors)
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`. [They’re only optional in some cases](https://mathiasbynens.be/notes/unquoted-attribute-values#css), and it’s a good practice for consistency.
- Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.

Questions on the terms used here? See the [syntax section of the Cascading Style Sheets article](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) on Wikipedia.
</div>

```scss
// Bad CSS
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

// Good CSS
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgb(0 0 0 / .5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

<div markdown="1">
### Declaration order

Property declarations should be grouped together in the following order:

1. Positioning
2. Box model
3. Typographic
4. Visual
5. Misc

Positioning comes first because it can remove an element from the normal document flow and override box model related styles. The box model—whether it's flex, float, grid, or table—follows as it dictates a component's dimensions, placement, and alignment. Everything else takes place _inside_ the component or without impacting the previous two sections, and thus they come last.

While `border` is part of the box model, most systems globally reset the [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) to `border-box` so that `border-width` doesn't affect overall dimensions. This, combined with keeping `border` near `border-radius`, is why it's under the Visual section instead.

Preprocessor mixins and functions should appear wherever most appropriate. For example, a `border-top-radius()` mixin would go in place of `border-radius` properties, while a `responsive-font-size()` function would go in place of `font-size` properties.

For a complete list of properties and their order, please see the [property order for Stylelint](https://github.com/stormwarning/stylelint-config-recess-order) used by [Bootstrap](https://getbootstrap.com).
</div>

```scss
.declaration-order {
  // Positioning
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  // Box model
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;

  // Typography
  font: normal 14px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  text-decoration: underline;

  // Visual
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  // Misc
  opacity: 1;
}
```

<div markdown="1">
### Logical properties

Logical properties are alternatives to directional and dimensonal properties based on abstract terms like *block* and *inline*. By default, block refers to the vertical direction (top and bottom) while inline refers to the horizontal direction (right and left). You can begin to use these values in your CSS in all modern, evergreen browsers.

**Why use logical properties?** Not every language flows left-ro-right like English, so the [writing mode](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode) needs to be flexible. With logical properties, you can easily support languages that can be written horizontally or vertically (like Chinese, Japanese, and Korean). Plus, they're usually shorter and simpler to write.

**Additional reading:**

- [CSS Logical Properties and Values – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties)
- [CSS Logical Properties and Values — CSS Tricks](https://css-tricks.com/css-logical-properties-and-values/)
- [CSS Writing Modes – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes)
</div>

```scss
// Without logical properties
.element {
  margin-right: auto;
  margin-left: auto;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
}

// With logical properties
.element {
  margin-inline: auto;
  border-block: 1px solid #eee;
}
```

<div markdown="1">
### Colors

With the support of [CSS Color Levels 4](https://www.w3.org/TR/css-color-4/) [in all major browsers](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb#space-separated_values), `rgba()` and `hsla()` are now aliases for `rgb()` and `hsl()`, meaning you can modify alpha values in `rgb()` and `hsl()`. Along with this comes support for new space-separated syntax for color values. For compability with future CSS color functions, use this new syntax.

Regardless of your color values and syntax, always ensure your color choices meet [WCAG minimum contrast ratios](https://webaim.org/articles/contrast/) (4.5:1 for 16px and smaller, 3:1 for larger).

**Additional reading:**

- [Smashing Magazine - A Guide To Modern CSS Colors](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/)
- [`rgb()` - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb)
</div>

```css
.element {
  color: rgb(255 255 255 / .65);
  background-color: rgb(0 0 0 / .95);
}
```

<div markdown="1">
### Avoid `@import`s

Compared to `<link>`s, `@import` is slower, adds extra page requests, and can cause other unforeseen problems. Avoid them and instead opt for an alternate approach:

- Use multiple `<link>`elements
- Compile your CSS with a preprocessor like [Sass](https://sass-lang.com/) or [Less](https://lesscss.org/) into a single file
- Concatenate your CSS files with features provided in Rails, Jekyll, and other environments

For more information, [read this article by Steve Souders](https://www.stevesouders.com/blog/2009/04/09/dont-use-import/).
</div>

```html
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Avoid @imports -->
<style>
  @import url("more.css");
</style>
```

<div markdown="1">
### Media query placement

Place media queries as close to their relevant rule sets whenever possible. Don't bundle them all in a separate stylesheet or at the end of the document. Doing so only makes it easier for folks to miss them in the future. Here's a typical setup.
</div>

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ... }
  .element-avatar { ... }
  .element-selected { ... }
}
```

<div markdown="1">
### Single declarations

In instances where a rule set includes **only one declaration**, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

The key factor here is error detection—e.g., a CSS validator stating you have a syntax error on Line 183. With a single declaration, there's no missing it. With multiple declarations, separate lines is a must for your sanity.
</div>

```scss
// Single declarations on one line
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

// Multiple declarations, one per line
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url("../img/sprite.png");
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
```

<div markdown="1">
### Shorthand notation

Limit shorthand declaration usage to instances where you must explicitly set all available values. Frequently overused shorthand properties include:

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Usually we don't need to set all the values a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. A `0` value implies an override of either a browser default or previously specified value.

Excessive use of shorthand properties leads to sloppier code with unnecessary overrides and unintended side effects.

The Mozilla Developer Network has a great article on [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) for those unfamiliar with notation and behavior.
</div>

```scss
// Bad example
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

// Good example
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

<div markdown="1">
### Nesting in preprocessors

Avoid unnecessary nesting in preprocessors whenever possible—keep it simple and avoid reverse nesting. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.

**Additional reading:**

- <a href="https://markdotto.com/2015/07/20/css-nesting/">Nesting in Sass and Less</a>
</div>

```scss
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
  > th { … }
  > td { … }
}
```

<div markdown="1">
### Operators in preprocessors

For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.
</div>

```scss
// Bad example
.element {
  margin: 10px 0 @variable*2 10px;
}

// Good example
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

<div markdown="1">
### Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Use the `//` syntax when writing CSS with preprocessors. When shipping CSS to production, remove all comments.

Be sure to write in complete sentences for larger comments and succinct phrases for general notes.
</div>

```scss
// Bad example
// Modal header
.modal-header {
  ...
}

// Good example
// Wrapping element for .modal-title and .modal-close
.modal-header {
  ...
}
```

<div markdown="1">
### Class names

- Keep classes lowercase and use dashes (not underscores or camelCase). Dashes serve as natural breaks in related class (e.g., `.btn` and `.btn-danger`).
- Avoid excessive and arbitrary shorthand notation. `.btn` is useful for _button_, but `.s` doesn't mean anything.
- Keep classes as short and succinct as possible.
- Use meaningful names; use structural or purposeful names over presentational.
- Prefix classes based on the closest parent or base class.
- Use `.js-*` classes to denote behavior (as opposed to style), but keep these classes out of your CSS.

It's also useful to apply many of these same rules when creating custom properties and preprocessor variable names.
</div>

```scss
// Bad example
.t { ... }
.red { ... }
.header { ... }

// Good example
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

<div markdown="1">
### Selectors

- Use classes over generic element tags for more explicit and reliable styling that isn't dependent on your markup.
- Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is known to be impacted by these.
- Keep selectors short and strive to limit the number of elements in each selector to three.
- Scope classes to the closest parent `only` when necessary (e.g., when not using prefixed classes).

**Additional reading:**

- [Scope CSS classes with prefixes](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade](https://markdotto.com/2012/03/02/stop-the-cascade/)
</div>

```scss
// Bad example
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

// Good example
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

<div markdown="1">
### Child and descendant selectors

When necessary, it may be helpful to use [the child combinator (`>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) to limit the cascade of some styles in elements like `<table>`s that are often recursively nested. Use it to limit styles to the immediate children elements of a parent element to avoid unnecessary overrides later on.
</div>

```css
.custom-table > tbody > tr > td,
.custom-table > tbody > tr > th {
  /* ... */
}
```

<div markdown="1">
### Organization

- Organize sections of code by component.
- Develop a consistent commenting hierarchy.
- Use consistent white space to your advantage when separating sections of code for scanning larger documents.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.
</div>

```scss
//
// Component section heading
//

.element { ... }


//
// Component section heading
//
// Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
//

.element { ... }

// Contextual sub-component or modifer
.element-heading { ... }
```
