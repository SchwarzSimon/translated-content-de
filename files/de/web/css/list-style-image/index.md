---
title: list-style-image
slug: Web/CSS/list-style-image
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{CSSRef}}

Die **`list-style-image`** [CSS](/de/docs/Web/CSS) Eigenschaft legt ein Bild fest, das als Listenmarkierung verwendet wird.

Es ist oft praktischer, die Kurzform {{ cssxref("list-style") }} zu verwenden.

{{InteractiveExample("CSS Demo: list-style-image")}}

```css interactive-example-choice
list-style-image: url("/shared-assets/images/examples/rocket.svg");
```

```css interactive-example-choice
list-style-image: none;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div>
    <p>NASA Notable Missions</p>
    <ul class="transition-all unhighlighted" id="example-element">
      <li>Apollo</li>
      <li>Hubble</li>
      <li>Chandra</li>
      <li>Cassini-Huygens</li>
      <li>Spitzer</li>
    </ul>
  </div>
</section>
```

```css interactive-example
.default-example {
  font-size: 1.2rem;
}

#example-element {
  width: 100%;
  background: #be094b;
  color: white;
}

section {
  text-align: left;
  flex-direction: column;
}

hr {
  width: 50%;
  color: lightgray;
  margin: 0.5em;
}

.note {
  font-size: 0.8rem;
}

.note a {
  color: #009e5f;
}

@counter-style space-counter {
  symbols: "\1F680" "\1F6F8" "\1F6F0" "\1F52D";
  suffix: " ";
}
```

> [!NOTE]
> Diese Eigenschaft wird auf Listenelemente angewendet, d.h. auf Elemente mit dem `{{cssxref("display")}}: list-item;` [standardmäßig](https://html.spec.whatwg.org/multipage/rendering.html#lists) schließt dies {{HTMLElement("li")}} Elemente ein. Da diese Eigenschaft vererbt wird, kann sie auf dem Elternelement (normalerweise {{HTMLElement("ol")}} oder {{HTMLElement("ul")}}) gesetzt werden, um auf alle Listenelemente anzuwenden.

## Syntax

```css
/* Keyword values */
list-style-image: none;

/* <url> values */
list-style-image: url("star-solid.gif");

/* valid image values */
list-style-image: linear-gradient(to left bottom, red, blue);

/* Global values */
list-style-image: inherit;
list-style-image: initial;
list-style-image: revert;
list-style-image: revert-layer;
list-style-image: unset;
```

### Werte

- {{cssxref("&lt;image&gt;")}}
  - : Ein gültiges Bild, das als Markierung verwendet werden soll.
- `none`
  - : Gibt an, dass kein Bild als Markierung verwendet wird. Wenn dieser Wert gesetzt ist, wird stattdessen die in {{ Cssxref("list-style-type") }} definierte Markierung verwendet. Dies ist der Standardwert für {{cssxref("list-style")}}.

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### Verwendung eines url-Wertes

Dieses Beispiel hat einen Stern als Markierung, den wir mit der {{cssxref("url_value", "&lt;url&gt;")}} Bildfunktion einfügen.

#### HTML

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

#### CSS

```css
ul {
  list-style-image: url("star-solid.gif");
}
```

#### Ergebnis

{{ EmbedLiveSample('Using_a_url_value') }}

### Verwendung eines Gradienten

Dieses Beispiel hat einen [CSS-Gradienten](/de/docs/Web/CSS/CSS_images/Using_CSS_gradients) als Markierung, den wir mit der {{cssxref("gradient/linear-gradient", "linear-gradient()")}} Bildfunktion erstellen.

#### HTML

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

#### CSS

```css
ul {
  font-size: 200%;
  list-style-image: linear-gradient(to left bottom, red, blue);
}
```

#### Ergebnis

{{ EmbedLiveSample('Using_a_gradient') }}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{Cssxref("list-style")}} Kurzform
- {{Cssxref("list-style-type")}} Eigenschaft
- {{Cssxref("list-style-position")}} Eigenschaft
- {{cssxref("::marker")}} Pseudo-Element
- [CSS-Listen und Zähler](/de/docs/Web/CSS/CSS_lists) Modul
- [CSS-Zählerstile](/de/docs/Web/CSS/CSS_counter_styles) Modul
