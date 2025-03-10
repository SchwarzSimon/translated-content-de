---
title: border-inline-width
slug: Web/CSS/border-inline-width
l10n:
  sourceCommit: 429d45679a29f386af0ddfcf2a64498843c3e1e5
---

{{CSSRef}}

Die **`border-inline-width`** [CSS](/de/docs/Web/CSS) Eigenschaft definiert die Breite der logischen Inline-Ränder eines Elements. Diese Eigenschaft wird in Abhängigkeit vom Schreibmodus, der Richtung und der Textausrichtung des Elements einer physischen Randbreite zugeordnet. Sie entspricht der {{cssxref("border-top-width")}} und {{cssxref("border-bottom-width")}}, oder {{cssxref("border-left-width")}} und {{cssxref("border-right-width")}}-Eigenschaft, je nachdem, welche Werte für {{cssxref("writing-mode")}}, {{cssxref("direction")}} und {{cssxref("text-orientation")}} definiert sind.

{{InteractiveExample("CSS Demo: border-inline-width")}}

```css interactive-example-choice
border-inline-width: thick;
writing-mode: horizontal-tb;
```

```css interactive-example-choice
border-inline-width: thick;
writing-mode: vertical-rl;
```

```css interactive-example-choice
border-inline-width: 4px;
writing-mode: horizontal-tb;
direction: rtl;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="transition-all" id="example-element">
    This is a box with a border around it.
  </div>
</section>
```

```css interactive-example
#example-element {
  background-color: palegreen;
  color: #000;
  border: 0 solid crimson;
  padding: 0.75em;
  width: 80%;
  height: 100px;
  unicode-bidi: bidi-override;
}
```

Die Randbreite in der anderen Dimension kann mit {{cssxref("border-block-width")}} festgelegt werden, die {{cssxref("border-block-start-width")}} und {{cssxref("border-block-end-width")}} setzt.

## Syntax

```css
/* <'border-width'> values */
border-inline-width: 5px 10px;
border-inline-width: 5px;
border-inline-width: thick;

/* Global values */
border-inline-width: inherit;
border-inline-width: initial;
border-inline-width: revert;
border-inline-width: revert-layer;
border-inline-width: unset;
```

### Werte

- `<'border-width'>`
  - : Die Breite des Randes. Siehe {{ cssxref("border-width") }}.

## Formale Definition

{{CSSInfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### HTML

```html
<div>
  <p class="exampleText">Example text</p>
</div>
```

### CSS

```css
div {
  background-color: yellow;
  width: 120px;
  height: 120px;
}

.exampleText {
  writing-mode: vertical-lr;
  border: 1px solid blue;
  border-inline-width: 5px 10px;
}
```

{{EmbedLiveSample("Examples", 140, 140)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [CSS Logical Properties and Values](/de/docs/Web/CSS/CSS_logical_properties_and_values)
- Diese Eigenschaft wird einer der physischen Randeigenschaften zugeordnet: {{cssxref("border-top-width")}}, {{cssxref("border-right-width")}}, {{cssxref("border-bottom-width")}}, und {{cssxref("border-left-width")}}
- {{cssxref("writing-mode")}}, {{cssxref("direction")}}, {{cssxref("text-orientation")}}
