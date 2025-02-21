---
title: pow()
slug: Web/CSS/pow
l10n:
  sourceCommit: 891bc513a3349040a16c4896197d6a3a910ca42b
---

{{CSSRef}}

Die **`pow()`** [CSS](/de/docs/Web/CSS) [Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) ist eine Exponentialfunktion, die den Wert einer Basis liefert, die auf die Potenz einer Zahl erhöht wird.

Die {{CSSxRef("exp")}} Funktion ist ein Spezialfall von `pow()`, bei dem der Wert der Basis die mathematische Konstante [e](<https://en.wikipedia.org/wiki/E_(mathematical_constant)>) ist.

## Syntax

```css
/* A <number> value */
width: calc(10px * pow(5, 2)); /* 10px * 25 = 250px */
width: calc(10px * pow(5, 3)); /* 10px * 125 = 1250px */
width: calc(10px * pow(2, 10)); /* 10px * 1024 = 10240px */
```

### Parameter

Die `pow(base, number)` Funktion akzeptiert zwei durch Kommas getrennte Werte als Parameter.

- `base`
  - : Eine Berechnung, die zu einer {{CSSxRef("&lt;number&gt;")}} aufgelöst wird und die Basis darstellt.
- `number`
  - : Eine Berechnung, die zu einer {{CSSxRef("&lt;number&gt;")}} aufgelöst wird und den Exponenten darstellt.

### Rückgabewert

Gibt eine {{CSSxRef("&lt;number&gt;")}} zurück, die base<sup>number</sup> darstellt, d.h. `base` erhöht auf die Potenz von `number`.

## Formale Syntax

{{CSSSyntax}}

## Beispiele

### Skalieren von Überschriften mit festem Verhältnis

Die `pow()` Funktion kann für Strategien wie CSS Modular Scale nützlich sein, die alle Schriftgrößen auf einer Seite durch ein festes Verhältnis zueinander in Beziehung setzen.

#### HTML

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
```

#### CSS

```css
h1 {
  font-size: calc(1rem * pow(1.5, 4));
}
h2 {
  font-size: calc(1rem * pow(1.5, 3));
}
h3 {
  font-size: calc(1rem * pow(1.5, 2));
}
h4 {
  font-size: calc(1rem * pow(1.5, 1));
}
h5 {
  font-size: calc(1rem * pow(1.5, 0));
}
h6 {
  font-size: calc(1rem * pow(1.5, -1));
}
```

#### Ergebnis

{{EmbedLiveSample('Scale headings by fixed ratio', '100%', '300px')}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{CSSxRef("sqrt")}}
- {{CSSxRef("hypot")}}
- {{CSSxRef("exp")}}
- {{CSSxRef("log")}}
