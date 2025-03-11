---
title: <gradient>
slug: Web/CSS/gradient
l10n:
  sourceCommit: b17ca921175c0a92d21c6c4effbc7fa3dc348a8e
---

{{CSSRef}}

Der **`<gradient>`** [CSS](/de/docs/Web/CSS) [Datentyp](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_data_types) ist ein spezieller Typ von {{cssxref("&lt;image&gt;")}}, der einen stetigen Übergang zwischen zwei oder mehr Farben darstellt.

{{InteractiveExample("CSS Demo: &amp;lt;gradient&amp;gt;")}}

```css interactive-example-choice
background: linear-gradient(#f69d3c, #3f87a6);
```

```css interactive-example-choice
background: radial-gradient(#f69d3c, #3f87a6);
```

```css interactive-example-choice
background: repeating-linear-gradient(#f69d3c, #3f87a6 50px);
```

```css interactive-example-choice
background: repeating-radial-gradient(#f69d3c, #3f87a6 50px);
```

```css interactive-example-choice
background: conic-gradient(#f69d3c, #3f87a6);
```

```html interactive-example
<section class="display-block" id="default-example">
  <div id="example-element"></div>
</section>
```

```css interactive-example
#example-element {
  min-height: 100%;
}
```

Ein CSS-Gradient hat [keine intrinsischen Dimensionen](/de/docs/Web/CSS/image#description); das heißt, er hat keine natürliche oder bevorzugte Größe, noch ein bevorzugtes Verhältnis. Seine konkrete Größe entspricht der Größe des Elements, auf das er angewendet wird.

## Syntax

Der `<gradient>`-Datentyp wird durch einen der unten aufgelisteten Funktionstypen definiert.

### Linearer Gradient

Lineare Gradienten wechseln die Farben progressiv entlang einer imaginären Linie. Sie werden mit der {{cssxref("gradient/linear-gradient", "linear-gradient()")}}-Funktion generiert.

### Radialer Gradient

Radiale Gradienten wechseln die Farben progressiv von einem Mittelpunkt (Ursprung) aus. Sie werden mit der {{cssxref("gradient/radial-gradient", "radial-gradient()")}}-Funktion generiert.

### Kegelförmiger Gradient

Kegelförmige Gradienten wechseln die Farben progressiv um einen Kreis herum. Sie werden mit der {{cssxref("gradient/conic-gradient", "conic-gradient()")}}-Funktion generiert.

### Wiederholender Gradient

Wiederholende Gradienten duplizieren einen Gradienten so oft wie nötig, um einen gegebenen Bereich zu füllen. Sie werden mit den Funktionen {{cssxref("gradient/repeating-linear-gradient", "repeating-linear-gradient()")}}, {{cssxref("gradient/repeating-radial-gradient", "repeating-radial-gradient()")}} und {{cssxref("gradient/repeating-conic-gradient", "repeating-conic-gradient()")}} generiert.

## Interpolation

Wie bei jeder Interpolation, die Farben beinhaltet, werden Gradienten im alpha-vormultiplizierten Farbraum berechnet. Dies verhindert unerwartete Grautöne, wenn sowohl die Farbe als auch die Deckkraft sich ändern. (Beachten Sie, dass ältere Browser dieses Verhalten möglicherweise nicht verwenden, wenn das [transparente Schlüsselwort](/de/docs/Web/CSS/named-color#transparent) verwendet wird.)

## Formale Syntax

{{csssyntax}}

## Beispiele

### Beispiel für linearen Gradient

Ein linearer Gradient.

```html hidden
<div class="linear-gradient">Linear gradient</div>
```

```css hidden
div {
  width: 240px;
  height: 80px;
}
```

```css
.linear-gradient {
  background: linear-gradient(
    to right,
    red,
    orange,
    yellow,
    green,
    blue,
    indigo,
    violet
  );
}
```

{{EmbedLiveSample('Linear_gradient_example', 240, 120)}}

### Beispiel für radialen Gradient

Ein radialer Gradient.

```html hidden
<div class="radial-gradient">Radial gradient</div>
```

```css hidden
div {
  width: 240px;
  height: 80px;
}
```

```css
.radial-gradient {
  background: radial-gradient(red, yellow, rgb(30 144 255));
}
```

{{EmbedLiveSample('Radial_gradient_example', 240, 120)}}

### Beispiel für kegelförmigen Gradient

Ein Beispiel für einen kegelförmigen Gradient.

```html hidden
<div class="conic-gradient">Conic gradient</div>
```

```css hidden
div {
  width: 200px;
  height: 200px;
}
```

```css
.conic-gradient {
  background: conic-gradient(pink, coral, lime);
}
```

{{EmbedLiveSample('Conic_gradient_example', 240, 240)}}

### Beispiele für wiederholende Gradienten

Beispiele für wiederholende lineare und radiale Gradienten.

```html hidden
<div class="linear-repeat"></div>
<span>Repeating linear gradient</span>
<hr />
<div class="radial-repeat"></div>
<span>Repeating radial gradient</span>
<hr />
<div class="conic-repeat"></div>
<span>Repeating conic gradient</span>
```

```css hidden
div {
  display: inline-block;
  width: 240px;
  height: 80px;
}

span {
  font-weight: bold;
  vertical-align: top;
}
```

```css
.linear-repeat {
  background: repeating-linear-gradient(
    to top left,
    pink,
    pink 5px,
    white 5px,
    white 10px
  );
}

.radial-repeat {
  background: repeating-radial-gradient(
    lime,
    lime 15px,
    white 15px,
    white 30px
  );
}

.conic-repeat {
  background: repeating-conic-gradient(lime, pink 30deg);
}
```

{{EmbedLiveSample('Repeating_gradient_examples', 240, 300)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Verwendung von CSS-Gradienten](/de/docs/Web/CSS/CSS_images/Using_CSS_gradients)
- Gradientenfunktionen: {{cssxref("gradient/linear-gradient", "linear-gradient()")}}, {{cssxref("gradient/repeating-linear-gradient", "repeating-linear-gradient()")}}, {{cssxref("gradient/radial-gradient", "radial-gradient()")}}, {{cssxref("gradient/repeating-radial-gradient", "repeating-radial-gradient()")}}, {{cssxref("gradient/conic-gradient", "conic-gradient()")}}, {{cssxref("gradient/repeating-conic-gradient", "repeating-conic-gradient()")}}
- [CSS-Grunddaten-Typen](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_data_types)
- Modul der [CSS-Werte und -Einheiten](/de/docs/Web/CSS/CSS_Values_and_Units)
- [Lernen: Werte und Einheiten](/de/docs/Learn_web_development/Core/Styling_basics/Values_and_units)
