---
title: Auftragen von SVG-Effekten auf HTML-Inhalt
short-title: SVG-Effekte für HTML
slug: Web/SVG/Guides/Applying_SVG_effects_to_HTML_content
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

Moderne Browser unterstützen die Verwendung von [SVG](/de/docs/Web/SVG) innerhalb von [CSS](/de/docs/Web/CSS)-Stilen, um grafische Effekte auf HTML-Inhalt anzuwenden.

Sie können SVG in Stilen entweder innerhalb desselben Dokuments oder eines externen Stylesheets angeben. Es gibt 3 Eigenschaften, die Sie verwenden können: [`mask`](/de/docs/Web/CSS/mask), [`clip-path`](/de/docs/Web/CSS/clip-path) und [`filter`](/de/docs/Web/CSS/filter).

> [!NOTE]
> Referenzen zu SVG in externen Dateien müssen sich auf dasselbe [Herkunftsprinzip](/de/docs/Web/Security/Same-origin_policy) wie das referenzierende Dokument beziehen.

## Verwendung eingebetteter SVGs

Um einen SVG-Effekt mittels CSS-Stilen anzuwenden, müssen Sie zunächst den CSS-Stil erstellen, der auf das anzuwendende SVG verweist.

```html
<style>
  p {
    mask: url(#my-mask);
  }
</style>
```

Im obigen Beispiel werden alle Absätze mit einer [SVG `<mask>`](/de/docs/Web/SVG/Reference/Element/mask) mit der [ID](/de/docs/Web/HTML/Global_attributes/id) `my-mask` maskiert.

### Beispiel: Maskieren

Zum Beispiel können Sie eine Verlaufsmaske für HTML-Inhalte erstellen, indem Sie SVG- und CSS-Code ähnlich dem folgenden in Ihr HTML-Dokument einfügen:

```html
<svg height="0">
  <mask id="mask-1">
    <linearGradient id="gradient-1" y2="1">
      <stop stop-color="white" offset="0" />
      <stop stop-opacity="0" offset="1" />
    </linearGradient>
    <circle cx="0.25" cy="0.25" r="0.25" id="circle" fill="white" />
    <rect x="0.5" y="0.2" width="300" height="100" fill="url(#gradient-1)" />
  </mask>
</svg>
```

```css
.target {
  mask: url(#mask-1);
}
p {
  width: 300px;
  border: 1px solid #000;
  display: inline-block;
}
```

Beachten Sie, dass im CSS die Maske mittels einer URL zur ID `#mask-1` angegeben wird, welche die ID der unten spezifizierten SVG-Maske ist. Alles andere definiert Details über die Verlaufsmaske selbst.

Die Anwendung des SVG-Effekts auf HTML erfolgt durch Zuweisung der oben definierten `target`-Klasse zu einem Element, etwa so:

```html
<p class="target" style="background:lime;">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing
  <em class="target"
    >elit, sed do eiusmod tempor incididunt ut labore et dolore magna
    aliqua.</em
  >
  Ut enim ad minim veniam.
</p>
```

Das obige Beispiel würde mit der darauf angewendeten Maske gerendert werden.

{{EmbedLiveSample('Example_Masking', 650, 200)}}

### Beispiel: Clipping

Dieses Beispiel veranschaulicht die Verwendung von SVG, um HTML-Inhalte zu clippen. Beachten Sie, dass sogar die anklickbaren Bereiche von Links geclippt sind.

```html
<p class="target" style="background:lime;">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.
</p>
<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing
  <em class="target"
    >elit, sed do eiusmod tempor incididunt ut labore et dolore magna
    aliqua.</em
  >
  Ut enim ad minim veniam.
</p>

<button onclick="toggleRadius()">Toggle radius</button>

<svg height="0">
  <clipPath id="clipping-path-1" clipPathUnits="objectBoundingBox">
    <circle cx="0.25" cy="0.25" r="0.25" id="circle" />
    <rect x="0.5" y="0.2" width="0.5" height="0.8" />
  </clipPath>
</svg>
```

```css
.target {
  clip-path: url(#clipping-path-1);
}
p {
  width: 300px;
  border: 1px solid #000;
  display: inline-block;
}
```

Dies legt ein Clipping-Gebiet aus einem Kreis und einem Rechteck fest, weist ihm die ID `#clipping-path-1` zu und referenziert es im CSS. Der Clipping-Pfad kann jedem Element mit der `target`-Klasse zugewiesen werden.

Sie können Änderungen am SVG in Echtzeit vornehmen und sehen, wie sie sofort die Darstellung des HTMLs beeinflussen. Zum Beispiel können Sie den Kreis im oben festgelegten Clipping-Pfad vergrößern:

```js
function toggleRadius() {
  const circle = document.getElementById("circle");
  circle.r.baseVal.value = 0.4 - circle.r.baseVal.value;
}
```

{{EmbedLiveSample('Example_Clipping', 650, 200)}}

### Beispiel: Filtern

Dies zeigt, wie ein Filter auf HTML-Inhalte mittels SVG angewendet wird. Es werden mehrere Filter festgelegt, die mit CSS auf drei Elemente sowohl im normalen als auch im Maus-[Hover](/de/docs/Web/CSS/:hover)-Status angewendet werden.

```html
<p class="target" style="background: lime;">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.
</p>
<pre class="target">lorem</pre>
<p>
  Lorem ipsum dolor sit amet, consectetur adipisicing
  <em class="target"
    >elit, sed do eiusmod tempor incididunt ut labore et dolore magna
    aliqua.</em
  >
  Ut enim ad minim veniam.
</p>
```

Jeder SVG-Filter kann auf diese Weise angewendet werden. Um beispielsweise einen Weichzeichnereffekt anzuwenden, könnten Sie folgendes verwenden:

```html
<svg height="0">
  <filter id="f1">
    <feGaussianBlur stdDeviation="3" />
  </filter>
</svg>
```

Sie könnten auch eine Farbmatrix anwenden:

```html
<svg height="0">
  <filter id="f2">
    <feColorMatrix
      values="0.3333 0.3333 0.3333 0 0
              0.3333 0.3333 0.3333 0 0
              0.3333 0.3333 0.3333 0 0
              0      0      0      1 0" />
  </filter>
</svg>
```

Und noch einige weitere Filter:

```html
<svg height="0">
  <filter id="f3">
    <feConvolveMatrix
      filterRes="100 100"
      style="color-interpolation-filters:sRGB"
      order="3"
      kernelMatrix="0 -1 0   -1 4 -1   0 -1 0"
      preserveAlpha="true" />
  </filter>
  <filter id="f4">
    <feSpecularLighting
      surfaceScale="5"
      specularConstant="1"
      specularExponent="10"
      lighting-color="white">
      <fePointLight x="-5000" y="-10000" z="20000" />
    </feSpecularLighting>
  </filter>
  <filter id="f5">
    <feColorMatrix
      values="1 0 0 0 0
                           0 1 0 0 0
                           0 0 1 0 0
                           0 1 0 0 0"
      style="color-interpolation-filters:sRGB" />
  </filter>
</svg>
```

Die fünf Filter werden mittels des folgenden CSS angewendet:

```css
p.target {
  filter: url(#f3);
}
p.target:hover {
  filter: url(#f5);
}
em.target {
  filter: url(#f1);
}
em.target:hover {
  filter: url(#f4);
}
pre.target {
  filter: url(#f2);
}
pre.target:hover {
  filter: url(#f3);
}
```

{{EmbedLiveSample('Example_Filtering', 650, 200)}}

### Beispiel: Verschwommener Text

Um Text zu verwischen, gibt es eine CSS-Filterfunktion namens [`blur()`](/de/docs/Web/CSS/filter-function/blur). Sie können denselben Effekt mittels SVG-Filtern erreichen.

```html
<p class="blur">Time to clean my glasses</p>
<svg height="0">
  <defs>
    <filter id="wherearemyglasses" x="0" y="0">
      <feGaussianBlur in="SourceGraphic" stdDeviation="1" />
    </filter>
  </defs>
</svg>
```

Sie können den SVG- und den CSS-Filter in derselben Klasse anwenden:

```css
.blur {
  filter: url(#wherearemyglasses);
}
```

{{ EmbedLiveSample('Example_Blurred_Text', 300, 100) }}

Das Verwischen ist rechentechnisch aufwändig, verwenden Sie es also sparsam, insbesondere bei Elementen, die gescrollt oder animiert werden.

### Beispiel: Texteffekte

SVG-Effekte können auch verwendet werden, um einen dynamischeren und flexibleren Ansatz zum Hinzufügen von Text im Vergleich zu normalem HTML-Text zu bieten.

Indem Sie den Text mit SVG-Elementen in Kombination mit HTML erstellen, können Sie eine Vielzahl unterschiedlicher Texteffekte erzeugen. Beispielsweise können Sie den Text rotieren:

```html
<svg height="60" width="200">
  <text x="0" y="15" fill="blue" transform="rotate(30 20,50)">
    Example text
  </text>
</svg>
```

## Verwendung externer Referenzen

SVG, das für Clipping, Masking und Filterung verwendet wird, kann aus einer externen Quelle geladen werden, solange diese Quelle aus dem gleichen Ursprung wie das HTML-Dokument stammt, auf das es angewendet wird.

Wenn Ihr CSS beispielsweise in einer Datei namens `default.css` ist, könnte es so aussehen:

```css
.target {
  clip-path: url(resources.svg#c1);
}
```

Das SVG wird dann aus einer Datei namens `resources.svg` importiert, wobei der Clipping-Pfad mit der ID `c1` verwendet wird.

## Siehe auch

- [SVG](/de/docs/Web/SVG)
- {{CSSXref('clip-path')}}-Eigenschaft
- {{CSSXref('mask')}}-Eigenschaft
- [Formen in Clipping und Masking – und wie man sie verwendet](https://hacks.mozilla.org/2017/06/css-shapes-clipping-and-masking/)
