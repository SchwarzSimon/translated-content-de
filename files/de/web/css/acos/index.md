---
title: acos()
slug: Web/CSS/acos
l10n:
  sourceCommit: 891bc513a3349040a16c4896197d6a3a910ca42b
---

{{CSSRef}}

Die **`acos()`** [CSS](/de/docs/Web/CSS) [Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) ist eine trigonometrische Funktion, die den Arkuskosinus einer Zahl zwischen `-1` und `1` zurückgibt. Die Funktion enthält eine einzige Berechnung, die die Anzahl der Bogenmaß-Einheiten zurückgibt, die ein {{cssxref("&lt;angle&gt;")}} zwischen `0deg` und `180deg` darstellt.

## Syntax

```css
/* Single <number> values */
transform: rotate(acos(-0.2));
transform: rotate(acos(2 * 0.125));

/* Other values */
transform: rotate(acos(pi / 5));
transform: rotate(acos(e / 3));
```

### Parameter

Die `acos(number)` Funktion akzeptiert nur einen Wert als Parameter.

- `number`
  - : Eine Berechnung, die zu einer {{cssxref("&lt;number&gt;")}} zwischen `-1` und `1` führt.

### Rückgabewert

Der Arkuskosinus einer `number` wird immer ein {{cssxref("&lt;angle&gt;")}} zwischen `0deg` und `180deg` zurückgeben.

- Wenn `number` kleiner als `-1` oder größer als `1` ist, ist das Ergebnis `NaN`.
- Wenn `number` genau `1` ist, ist das Ergebnis `0`.

## Formale Syntax

{{CSSSyntax}}

## Beispiele

### Elemente rotieren

Die `acos()` Funktion kann verwendet werden, um Elemente zu {{cssxref("transform-function/rotate", "rotieren")}}, da sie ein {{cssxref("&lt;angle&gt;")}} zurückgibt.

#### HTML

```html
<div class="box box-1"></div>
<div class="box box-2"></div>
<div class="box box-3"></div>
<div class="box box-4"></div>
<div class="box box-5"></div>
```

#### CSS

```css hidden
body {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 50px;
}
```

```css
div.box {
  width: 100px;
  height: 100px;
  background: linear-gradient(orange, red);
}
div.box-1 {
  transform: rotate(acos(1));
}
div.box-2 {
  transform: rotate(acos(0.5));
}
div.box-3 {
  transform: rotate(acos(0));
}
div.box-4 {
  transform: rotate(acos(-0.5));
}
div.box-5 {
  transform: rotate(acos(-1));
}
```

#### Ergebnis

{{EmbedLiveSample('Rotate elements', '100%', '200px')}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{CSSxRef("sin")}}
- {{CSSxRef("cos")}}
- {{CSSxRef("tan")}}
- {{CSSxRef("asin")}}
- {{CSSxRef("atan")}}
- {{CSSxRef("atan2")}}
