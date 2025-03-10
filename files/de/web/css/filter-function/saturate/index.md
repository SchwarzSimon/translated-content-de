---
title: saturate()
slug: Web/CSS/filter-function/saturate
l10n:
  sourceCommit: 429d45679a29f386af0ddfcf2a64498843c3e1e5
---

{{CSSRef}}

Die **`saturate()`** [CSS](/de/docs/Web/CSS) [Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) super-saturiert oder entsättigt das Eingabebild. Ihr Ergebnis ist eine {{cssxref("&lt;filter-function&gt;")}}.

> **Note:** `saturate()` ist als Matrixoperation auf der RGB-Farbe spezifiziert. Sie konvertiert die Farbe nicht tatsächlich in das HSL-Modell, was eine nicht-lineare Operation ist. Daher kann sie die Farbton- oder Helligkeitswerte der Originalfarbe nicht beibehalten.

{{InteractiveExample("CSS Demo: saturate()")}}

```css interactive-example-choice
filter: saturate(1);
```

```css interactive-example-choice
filter: saturate(4);
```

```css interactive-example-choice
filter: saturate(50%);
```

```css interactive-example-choice
filter: saturate(0);
```

```html interactive-example
<section id="default-example">
  <img
    class="transition-all"
    id="example-element"
    src="/shared-assets/images/examples/firefox-logo.svg"
    width="200" />
</section>
```

## Syntax

```css
saturate(amount)
```

### Parameter

- `amount` {{Optional_Inline}}
  - : Die Menge der Umwandlung, angegeben als {{cssxref("&lt;number&gt;")}} oder {{cssxref("&lt;percentage&gt;")}}. Ein Wert unter `100%` entsättigt das Bild, während ein Wert über `100%` es super-saturiert. Ein Wert von `0%` ist komplett entsättigt, während ein Wert von `100%` die Eingabe unverändert lässt. Der initiale Wert für {{Glossary("interpolation", "Interpolierung")}} ist `1`. Der Standardwert ist `1`.

## Formale Syntax

{{CSSSyntax}}

## Beispiele

### Beispiele für korrekte Werte für saturate()

```css
saturate(0)     /* Completely unsaturated */
saturate(.4)    /* 40% saturated */
saturate()      /* No effect */
saturate(100%)  /* No effect */
saturate(200%)  /* Double saturation */
```

### saturate() bewahrt Farbton oder Helligkeit nicht

Das folgende Diagramm vergleicht zwei Farbspektren mit `hsl(0 50% 50%)` als Mittelpunkt: das erste Spektrum wird unter Verwendung von `saturate()` erstellt und das zweite benutzt tatsächliche HSL-Farbwerte. Beachten Sie, wie das `saturate()`-Spektrum Unterschiede im Farbton und in der Helligkeit zu den beiden Enden hin zeigt.

```html
<div>
  <p>Using <code>saturate()</code></p>
  <div id="saturate"></div>
</div>
<div>
  <p>Using <code>hsl()</code></p>
  <div id="hsl"></div>
</div>
```

```css hidden
#saturate,
#hsl {
  display: flex;
  margin: 1em 0;
}

#saturate div,
#hsl div {
  width: 2px;
  height: 100px;
}
```

```js
const saturate = document.getElementById("saturate");
const hsl = document.getElementById("hsl");

for (let i = 0; i <= 200; i++) {
  const div1 = document.createElement("div");
  div1.style.backgroundColor = `hsl(0 ${i / 2}% 50%)`;
  hsl.appendChild(div1);

  const div2 = document.createElement("div");
  div2.style.backgroundColor = "hsl(0 50% 50%)";
  div2.style.filter = `saturate(${i}%)`;
  saturate.appendChild(div2);
}
```

{{EmbedLiveSample('saturate_does_not_preserve_hue_or_lightness','100%','350')}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

Die anderen {{cssxref("&lt;filter-function&gt;")}} Funktionen, die in den Werten der {{cssxref("filter")}} und {{cssxref("backdrop-filter")}} Eigenschaften verwendet werden können, umfassen:

- {{cssxref("filter-function/blur", "blur()")}}
- {{cssxref("filter-function/brightness", "brightness()")}}
- {{cssxref("filter-function/contrast", "contrast()")}}
- {{cssxref("filter-function/drop-shadow", "drop-shadow()")}}
- {{cssxref("filter-function/grayscale", "grayscale()")}}
- {{cssxref("filter-function/hue-rotate", "hue-rotate()")}}
- {{cssxref("filter-function/invert", "invert()")}}
- {{cssxref("filter-function/opacity", "opacity()")}}
- {{cssxref("filter-function/sepia", "sepia()")}}
