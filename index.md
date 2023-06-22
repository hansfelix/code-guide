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

- [Sintaxis CSS](#css-syntax)
- [Orden en la declaración](#declaration-order)
- [Colores](#colors)
- [Propiedades lógicas](#logical-properties)
- [Evite los `@import`s](#avoid-imports)
- [Ubicación de los media query](#media-query-placement)
- [Declaraciones de una línea](#single-declarations)
- [Notaciones abreviadas](#shorthand-notation)
- [Anidamiento en preprocesadores](#nesting-in-preprocessors)
- [Operadores en preprocesadores](#operators-in-preprocessors)
- [Comentarios](#comments)
- [Nombre de las clases](#class-names)
- [Selectores](#selectors)
- [Selectores de hijos y de descendientes](#child-and-descendant-selectors)
- [Organización](#organization)
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
### Sintaxis CSS
{: #css-syntax }

- Use tabulaciones suaves con dos espacios—son la única forma de garantizar que el código se reproduzca de la misma manera en cualquier entorno.
- Cuando agrupe selectores, mantenga los selectores individuales en una sola línea.
- Incluya un espacio en blanco antes de la llave de apertura de los bloques de declaración, para facilitar la legibilidad.
- Coloque las llaves de cierre de los bloques de declaración en una nueva línea.
- Incluya un espacio en blanco después de `:` para cada declaración.
- Cada declaración debe aparecer en su propia línea para un informe de errores más preciso.
- Termine todas las declaraciones con un punto y coma. En la última declaración es opcional, pero su código es más propenso a errores sin ella.
- Los valores de propiedad separados por comas deben incluir un espacio después de cada coma (por ejemplo: `box-shadow`).
- Usar valores separados por espacios para las propiedades de color (por ejemplo: `color: rgb(0 0 0 / .5)`). [Consulte la sección Colores de esta guía para más información.](#colors)
- No prefije los valores de propiedad o los parámetros de color con un cero inicial (por ejemplo: `.5` en vez de `0.5` y `-.5px` en vez de `-0.5px`).
- Ponga en minúsculas todos los valores hexadecimales, por ejemplo, `#fff`. Las letras minúsculas son mucho más fáciles de distinguir al escanear un documento, ya que tienden a tener formas más únicas.
- Utilice valores hexadecimales abreviados cuando estén disponibles, por ejemplo, `#fff` en vez de `#ffffff`.
- Utilice valores de atributo en selectores, por ejemplo, `input[type="text"]`. [Solo son opcionales en algunos casos](https://mathiasbynens.be/notes/unquoted-attribute-values#css), y es una buena práctica para mantener la coherencia.
- Evite especificar unidades para valores cero, por ejemplo, `margin: 0;` en vez de `margin: 0px;`.

¿Preguntas sobre los términos utilizados aquí? Consulte la [sección de sintaxis del artículo Hojas de Estilo en Cascada](https://es.wikipedia.org/wiki/CSS) en Wikipedia.
</div>

```scss
// Mal CSS
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

// Buen CSS
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
### Orden en la declaración
{: #declaration-order }

Las declaraciones de las propiedades CSS deben agruparse en el siguiente orden:

1. Posicionamiento
2. Modelo de caja
3. Tipografía
4. Visual
5. Misceláneo

El posicionamiento es lo primero porque puede eliminar un elemento del flujo normal del documento y anular los estilos relacionados con el modelo de caja. El modelo de caja—ya sea `flex`, `float`, `grid` o `table`—es lo siguiente, ya que dicta las dimensiones, la ubicación y la alineación del componente. Todo lo demás tiene lugar _dentro_ del componente o no afecta a las dos grupos anteriores, por lo que quedan en último lugar.

Si bien `border` es parte del modelo de caja, la mayoría de los sistemas restablecen globalmente el [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) a `border-box` para que `border-width` no afecte las dimensiones generales.
Todo esto, combinado con mantener el `border` cerca de `border-radius`, es la razón por la que está en la sección visual.

Los mixins y funciones de los preprocesadores deben aparecer donde sea más apropiado. Por ejemplo, un mixin `border-top-radius()` reemplazaría las propiedades `border-radius`, mientras que una función `responsive-font-size()` reemplazaría las propiedades `font-size`.

Para obtener una lista completa de propiedades y su orden, consulte el [orden de propiedades de Stylelint](https://github.com/stormwarning/stylelint-config-recess-order) utilizado por [Bootstrap](https://getbootstrap.com).
</div>

```scss
.declaration-order {
  // Posicionamiento
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  // Modelo de caja
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;

  // Tipografía
  font: normal 14px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  text-decoration: underline;

  // Visual
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  // Misceláneo
  opacity: 1;
}
```

<div markdown="1">
### Propiedades lógicas
{: #logical-properties }

Las propiedades lógicas son alternativas a las propiedades direccionales y dimensionales basadas en términos como *block* e *inline*. Por defecto, *block* se refiere a la dirección vertical (arriba y abajo) mientras que *inline* se refiere a la dirección horizontal (derecha e izquierda). Puede comenzar a usar estos valores en su CSS en todos los navegadores modernos y futuros.

**¿Por qué usar propiedades lógicas?** No todos los idiomas se escriben de izquierda a derecha como el español o inglés, por lo que el [writing mode](https://developer.mozilla.org/es/docs/Web/CSS/writing-mode) debe ser flexible. Con propiedades lógicas, puede admitir fácilmente idiomas que se pueden escribir horizontal o verticalmente (como el chino, japonés y coreano). Además, estas propiedades suelen ser más breves y fáciles de escribir.

**Más información:**

- [Propiedades y Valores Lógicos de CSS – MDN](https://developer.mozilla.org/es/docs/Web/CSS/CSS_logical_properties_and_values)
- [CSS Logical Properties and Values — CSS Tricks](https://css-tricks.com/css-logical-properties-and-values/)
- [CSS Writing Modes – MDN](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Writing_Modes)
</div>

```scss
// Sin propiedades lógicas
.element {
  margin-right: auto;
  margin-left: auto;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
}

// Con propiedades lógicas
.element {
  margin-inline: auto;
  border-block: 1px solid #eee;
}
```

<div markdown="1">
### Colores
{: #colors }

Con el soporte de [CSS Color Levels 4](https://www.w3.org/TR/css-color-4/) [en todos los principales navegadores](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb#browser_compatibility), `rgba()` y `hsla()` ahora son alias para `rgb()` y `hsl()`, lo que significa que puede modificar los valores alpha en `rgb()` y `hsl()`. Junto con esto viene el soporte para la nueva sintaxis separada por espacios para los valores de color. Para compatibilidad con futuras funciones de color CSS use esta nueva sintaxis.

Independientemente de los valores y la sintaxis de color, siempre asegúrese de que sus opciones de color cumplan con las [relaciones de contraste mínimas de WCAG](https://webaim.org/articles/contrast/) (4,5:1 para 16 px y más pequeños, 3:1 para más grandes).

**Más información:**

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
### Evite los `@import`s
{: #avoid-imports }

En comparación con `<link>`, `@import` es más lento, ya que agrega solicitudes de página adicionales y puede causar otros problemas no previstos. Evítelos y opte por un enfoque alternativo:

Compared to `<link>`s, `@import` is slower, adds extra page requests, and can cause other unforeseen problems. Avoid them and instead opt for an alternate approach:

- Use elementos `<link>`
- Compile su CSS en un solo archivo con preprocesadores como [Sass](https://sass-lang.com/) o [Less](https://lesscss.org/)
- Concatene sus archivos CSS con funciones proporcionadas en Rails, Jekyll y otros entornos

Para más información, [puede leer este artículo de Steve Souders](https://www.stevesouders.com/blog/2009/04/09/dont-use-import/).
</div>

```html
<!-- Use elementos <link> -->
<link rel="stylesheet" href="core.css">

<!-- Evite los @imports -->
<style>
  @import url("more.css");
</style>
```

<div markdown="1">
### Ubicación de los media query
{: #media-query-placement }

Ubique las sentencias media query lo más cerca posible de sus conjuntos de reglas relevantes, siempre que sea posible. No los agrupe todos en una hoja de estilo separada o al final del documento, hacer esti solo hará que sea más fácil que los desarrolladores los olviden a futuro. 
Aquí hay una configuración de ejemplo.
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
### Declaraciones de una línea
{: #single-declarations }

En los casos en que un conjunto de reglas incluya **solo una declaración**, considere eliminar los saltos de línea para facilitar la lectura y una edición más rápida. Cualquier conjunto de reglas con múltiples declaraciones debe dividirse en líneas separadas.

El factor clave aquí es la detección de errores, por ejemplo, un validador de CSS que indica que tiene un error de sintaxis en la línea 183. Con una sola declaración, no se puede perder. Con múltiples declaraciones, las líneas separadas son imprescindibles para su entendimiento.
</div>

```scss
// Declaración de una sola línea
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

// Declaraciones de varias líneas, una por línea
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
### Notaciones abreviadas
{: #shorthand-notation }

Limite el uso de propiedades abreviadas a instancias en las que debe establecer explícitamente todos los valores disponibles. Las propiedades abreviadas que se suelen usar en exceso frecuentemente incluyen:

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Por lo general, no necesitamos establecer todos los valores que representa una propiedad abreviada. Por ejemplo, los encabezados HTML solo establecen el margen superior e inferior, por lo que si es necesario, solo anule esos dos valores. Un valor `0` implica una anulación de un valor predeterminado del navegador o un valor especificado previamente.

El uso excesivo de propiedades abreviadas conduce a un código más descuidado con anulaciones innecesarias y efectos secundarios no deseados.

La *Mozilla Developer Network* tiene un excelente artículo sobre [propiedades abreviadas](https://developer.mozilla.org/es/docs/Web/CSS/Shorthand_properties) para aquellos que no esten familiarizados con su notación y comportamiento.
</div>

```scss
// Mal ejemplo
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

// Buen ejemplo
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

<div markdown="1">
### Anidamiento en preprocesadores
{: #nesting-in-preprocessors }

Evite el anidamiento innecesario en los preprocesadores siempre que sea posible—manténgalo simple y evite el anidamiento inverso. Considere anidar solo si debe aplicar estilos a un padre y si este tiene varios elementos para anidar.

**Más información:**

- <a href="https://markdotto.com/2015/07/20/css-nesting/">Nesting in Sass and Less</a>
</div>

```scss
// Sin anidamiento
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// Con anidamiento
.table > thead > tr {
  > th { … }
  > td { … }
}
```

<div markdown="1">
### Operadores en preprocesadores
{: #operators-in-preprocessors }

Para mejorar la legibilidad, encierre todas las operaciones matemáticas entre paréntesis separadas con un espacio en blanco entre valores, variables y operadores.
</div>

```scss
// Mal ejemplo
.element {
  margin: 10px 0 @variable*2 10px;
}

// Buen ejemplo
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

<div markdown="1">
### Comentarios
{: #comments }

El código es escrito y mantenido por varias personas. Asegúrese de que su código sea descriptivo, correctamente comentado y accesible para los demás. Los grandes comentarios de código transmiten contexto o propósito. No reitere simplemente el nombre de un componente o clase. Utilice la sintaxis de comentario `//` al escribir CSS con preprocesadores. Al enviar CSS a producción elimine todos los comentarios.

Asegúrese de escribir oraciones completas para comentarios más extensos y frases breves para notas generales.
</div>

```scss
// Mal ejemplo
// Cabecera del modal
.modal-header {
  ...
}

// Buen ejemplo
// Elemento que encierra a .modal-title y .modal-close
.modal-header {
  ...
}
```

<div markdown="1">
### Nombre de las clases
{: #class-names }

- Mantenga las clases en minúsculas y use guiones (no guiones bajos ni camelCase). Los guiones sirven como separaciones naturales en el nombre de la clase (por ejemplo, `.btn` y `.btn-danger`).
- Evite una notación abreviada excesiva y arbitraria. `.btn` es útil para referirse a un _button_, pero `.s` no significa nada.
- Mantenga las clases tan cortas y concisa como sea posible.
- Use nombres significativos; use nombres con estructuras o con un propósito definido por encima de que sea vistoso.
- Los prefijos de las clases deben estar basadas en la clase padre o base más cercana.
- Use clases `.js-*` para indicar el comportamiento (a diferencia del estilo), y mantenga estas clases fuera de sus estilos CSS.

También es útil aplicar muchas de estas mismas reglas al crear propiedades personalizadas y nombres de variables de preprocesadores.
</div>

```scss
// Mal ejemplo
.t { ... }
.red { ... }
.header { ... }

// Buen ejemplo
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

<div markdown="1">
### Selectores
{: #selectors }

- Prefiera usar clases sobre elementos HTML genéricos para un estilo más explícito y confiable que no dependa de su marcado.
- Evite usar varios selectores de atributos (por ejemplo, `[class^="..."]`) en componentes comunes. Se sabe que el rendimiento del navegador se ve afectado por este tipo de selectores.
- Mantenga los selectores cortos y esfuércese por limitar la cantidad de elementos en cada selector a tres.
- Utilice el alcance de las clases al padre más cercano `solo` cuando sea necesario (por ejemplo, cuando no se usen clases prefijadas).

**Más información:**

- [Scope CSS classes with prefixes](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade](https://markdotto.com/2012/03/02/stop-the-cascade/)
</div>

```scss
// Mal ejemplo
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

// Buen ejemplo
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

<div markdown="1">
### Selectores de hijos y de descendientes
{: #child-and-descendant-selectors }

Cuando sea necesario, puede ser útil usar el [selector de hijos (`>`)](https://developer.mozilla.org/es/docs/Web/CSS/Child_combinator) para limitar la cascada de algunos estilos en elementos como `<table>` que a menudo están anidados recursivamente. Úselo para limitar los estilos a los elementos secundarios inmediatos de un elemento principal para evitar anulaciones innecesarias más adelante.
</div>

```css
.custom-table > tbody > tr > td,
.custom-table > tbody > tr > th {
  /* ... */
}
```

<div markdown="1">
### Organización
{: #organization }

- Organice secciones de código por componente.
- Desarrolle una jerarquía de comentarios consistente.
- Utilice saltos de línea consistentes a su favor cuando separe secciones de código para leer archivos más grandes.
- Cuando utilice varios archivos CSS, divídalos por componente en lugar de por página. Las páginas se pueden reorganizar y los componentes se pueden mover.
</div>

```scss
//
// Encabezado de la sección de componentes
//

.element { ... }


//
// Encabezado de la sección de componentes
//
// A veces es necesario incluir un contexto opcional para todo el componente. Haz eso aquí arriba si es algo importante.
//

.element { ... }

// Subcomponente contextual o modificador
.element-heading { ... }
```
