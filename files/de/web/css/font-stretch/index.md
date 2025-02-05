---
title: font-stretch
slug: Web/CSS/font-stretch
l10n:
  sourceCommit: 64d85b74ce1cce6a24ae8979da4f3f4a01a47229
---

{{CSSRef}}

> [!NOTE]
> Die Eigenschaft `font-stretch` [wurde nun in den Spezifikationen in `font-width` umbenannt](https://drafts.csswg.org/css-fonts/#font-stretch-desc). Der Name `font-stretch` wurde als Alias für die Eigenschaft `font-width` beibehalten.
> Der neue Name `font-width` wird von keinem Browser bisher unterstützt.

Die **`font-stretch`** [CSS](/de/docs/Web/CSS) Eigenschaft wählt eine normale, komprimierte oder erweiterte Schriftart aus einer Schriftfamilie aus.

{{EmbedInteractiveExample("pages/css/font-stretch.html")}}

## Syntax

```css
/* <font-stretch-css3> keyword values */
font-stretch: normal;
font-stretch: ultra-condensed;
font-stretch: extra-condensed;
font-stretch: condensed;
font-stretch: semi-condensed;
font-stretch: semi-expanded;
font-stretch: expanded;
font-stretch: extra-expanded;
font-stretch: ultra-expanded;

/* Percentage values */
font-stretch: 50%;
font-stretch: 100%;
font-stretch: 200%;

/* Global values */
font-stretch: inherit;
font-stretch: initial;
font-stretch: revert;
font-stretch: revert-layer;
font-stretch: unset;
```

Diese Eigenschaft kann als einzelner `<font-stretch-css3>` Schlüsselwortwert oder als einzelner {{cssxref("&lt;percentage&gt;")}} Wert angegeben werden.

### Werte

- `normal`
  - : Gibt eine normale Schriftart an.
- `semi-condensed`, `condensed`, `extra-condensed`, `ultra-condensed`
  - : Gibt eine komprimiertere Schriftart als normal an, wobei `ultra-condensed` die kompakteste ist.
- `semi-expanded`, `expanded`, `extra-expanded`, `ultra-expanded`
  - : Gibt eine erweiterte Schriftart als normal an, wobei `ultra-expanded` die breiteste ist.
- `<percentage>`

  - : Ein {{cssxref("&lt;percentage&gt;")}} Wert zwischen 50% und 200% (einschließlich). Negative Werte sind für diese Eigenschaft nicht erlaubt.

### Zuordnung von Schlüsselwörtern zu numerischen Werten

Die folgende Tabelle zeigt die Zuordnung zwischen den `<font-stretch-css3>` Schlüsselwortwerten und numerischen Prozentsätzen:

| Schlüsselwort     | Prozentsatz |
| ----------------- | ----------- |
| `ultra-condensed` | 50%         |
| `extra-condensed` | 62,5%       |
| `condensed`       | 75%         |
| `semi-condensed`  | 87,5%       |
| `normal`          | 100%        |
| `semi-expanded`   | 112,5%      |
| `expanded`        | 125%        |
| `extra-expanded`  | 150%        |
| `ultra-expanded`  | 200%        |

## Beschreibung

Einige Schriftfamilien bieten zusätzliche Schriftvarianten, bei denen die Zeichen schmaler sind als die normale Variante (_condensed_ Varianten) oder breiter als die normale Variante (_expanded_ Varianten).

Sie können `font-stretch` verwenden, um eine komprimierte oder erweiterte Variante aus solchen Schriftarten auszuwählen. Wenn die verwendete Schriftart keine komprimierten oder erweiterten Varianten bietet, hat diese Eigenschaft keine Wirkung.

### Auswahl des Schriftschnitts

Die für einen gegebenen Wert von `font-stretch` ausgewählte Variante hängt von den unterstützten Varianten der betreffenden Schriftart ab. Wenn die Schriftart keine Variante bietet, die genau dem angegebenen Wert entspricht, dann führen Werte unter 100% zu einer schmaleren Variante, und Werte größer oder gleich 100% zu einer breiteren Variante.

Die folgende Tabelle zeigt die Wirkung verschiedener prozentualer Werte von `font-stretch` auf zwei verschiedene Schriftarten:

```css hidden
@font-face {
  font-family: "Inconsolata";
  src: url("https://fonts.gstatic.com/s/inconsolata/v31/QlddNThLqRwH-OJ1UHjlKENVzlm-WkL3GZQmAwPyya15.woff2")
    format("woff2");
  font-stretch: 50% 200%;
}

@font-face {
  font-family: "Anek Malayalam";
  src: url("https://fonts.gstatic.com/s/anekmalayalam/v4/6qLUKZActRTs_mZAJUZWWkhke0nYa-f6__Azq3-gP1W7db9_.woff2")
    format("woff2");
  font-stretch: 75% 125%;
}

td {
  border: solid;
  border-width: 1px;
}

#inconsolata td {
  font:
    90px Inconsolata,
    sans-serif;
}
#anek-malayalam td {
  font: 90px "Anek Malayalam";
}
#inconsolata td:nth-child(2),
#anek-malayalam td:nth-child(2) {
  font-stretch: 50%;
}
#inconsolata td:nth-child(3),
#anek-malayalam td:nth-child(3) {
  font-stretch: 62.5%;
}
#inconsolata td:nth-child(4),
#anek-malayalam td:nth-child(4) {
  font-stretch: 75%;
}
#inconsolata td:nth-child(5),
#anek-malayalam td:nth-child(5) {
  font-stretch: 87.5%;
}
#inconsolata td:nth-child(6),
#anek-malayalam td:nth-child(6) {
  font-stretch: 100%;
}
#inconsolata td:nth-child(7),
#anek-malayalam td:nth-child(7) {
  font-stretch: 112.5%;
}
#inconsolata td:nth-child(8),
#anek-malayalam td:nth-child(8) {
  font-stretch: 125%;
}
#inconsolata td:nth-child(9),
#anek-malayalam td:nth-child(9) {
  font-stretch: 150%;
}
#inconsolata td:nth-child(10),
#anek-malayalam td:nth-child(10) {
  font-stretch: 200%;
}
```

```html hidden
<table class="standard-table">
  <thead>
    <tr>
      <th scope="row"></th>
      <th scope="col">50%</th>
      <th scope="col">62.5%</th>
      <th scope="col">75%</th>
      <th scope="col">87.5%</th>
      <th scope="col">100%</th>
      <th scope="col">112.5%</th>
      <th scope="col">125%</th>
      <th scope="col">150%</th>
      <th scope="col">200%</th>
    </tr>
  </thead>
  <tbody>
    <tr id="inconsolata">
      <th scope="row">Inconsolata</th>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
    </tr>
    <tr id="anek-malayalam">
      <th scope="row">Anek Malayalam</th>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
```

{{EmbedLiveSample('Font_face_selection', "100%", "300px")}}

- [Anek Malayalam](https://fonts.google.com/specimen/Anek+Malayalam) ist eine variable Google-Schriftart, die Breiten von 75% bis 125% unterstützt. Werte unterhalb und oberhalb dieses Bereichs wählen die am besten passende Schriftart aus.
- [Inconsolata](https://fonts.google.com/specimen/Inconsolata) ist eine variable Schriftart, die einen kontinuierlichen Bereich von Breiten zwischen 50% und 200% bietet. <!-- Hinweis, dynamisch bezogenes woff2 von Google-Schriftarten durch Abfrage: https://fonts.googleapis.com/css2?family=Inconsolata:wdth@50..200 -->

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax("font-width")}}

## Beispiele

### Einstellen von Schriftdehnungsprozentsätzen

```html
<p class="condensed">an elephantine lizard</p>
<p class="normal">an elephantine lizard</p>
<p class="expanded">an elephantine lizard</p>
```

```css
@font-face {
  src: url("https://mdn.github.io/shared-assets/fonts/LeagueMono-VF.ttf");
  font-family: "LeagueMonoVariable";
  font-style: normal;
  font-stretch: 1% 500%; /* Required by Chrome */
}

p {
  font:
    1.5rem "LeagueMonoVariable",
    sans-serif;
}

.condensed {
  font-stretch: 50%;
}

.normal {
  font-stretch: 100%;
}

.expanded {
  font-stretch: 200%;
}
```

{{EmbedLiveSample("Setting font stretch percentages", "100%", 200)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{cssxref("font-style")}}
- {{cssxref("font-weight")}}
- SVG {{SVGAttr("font-stretch")}} Attribut
- [Lernen: Fundamentales Text- und Schriftstyling](/de/docs/Learn_web_development/Core/Text_styling/Fundamentals)
- [CSS Schriftarten](/de/docs/Web/CSS/CSS_fonts) Modul
