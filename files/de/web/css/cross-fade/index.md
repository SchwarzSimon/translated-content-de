---
title: cross-fade()
slug: Web/CSS/cross-fade
l10n:
  sourceCommit: b17ca921175c0a92d21c6c4effbc7fa3dc348a8e
---

{{CSSRef}}

Die **`cross-fade()`** [CSS](/de/docs/Web/CSS) [Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) kann verwendet werden, um zwei oder mehr Bilder bei einer definierten Transparenz zu mischen. Sie kann für viele grundlegende Bildmanipulationen genutzt werden, wie zum Beispiel um ein Bild mit einer Volltonfarbe zu überlagern oder einen bestimmten Bereich der Seite hervorzuheben, indem ein Bild mit einem radialen Verlauf kombiniert wird.

## Syntax

> [!WARNING]
> Die Spezifikation und die aktuellen Implementierungen haben unterschiedliche Syntaxen.
> Die Spezifikationssyntax wird zuerst erklärt.

### Spezifikationssyntax

Die Funktion `cross-fade()` nimmt eine Liste von Bildern, bei der ein Prozentsatz definiert, wie viel von jedem Bild in Bezug auf die Deckkraft erhalten bleibt, wenn es mit den anderen Bildern gemischt wird. Der Prozentwert muss ohne Anführungszeichen kodiert werden, muss das `'%'`-Symbol enthalten und sein Wert muss zwischen 0% und 100% liegen.

Die Funktion kann in CSS überall dort verwendet werden, wo ein gewöhnlicher Bildverweis verwendet werden kann.

#### Cross-fade-Prozentsätze

Betrachten Sie den Prozentsatz als einen Deckkraftwert für jedes Bild. Das bedeutet, ein Wert von 0% macht das Bild vollständig transparent, während ein Wert von 100% das Bild vollständig deckend macht.

```css
cross-fade(url(white.png) 0%, url(black.png) 100%); /* fully black */
cross-fade(url(white.png) 25%, url(black.png) 75%); /* 25% white, 75% black */
cross-fade(url(white.png) 50%, url(black.png) 50%); /* 50% white, 50% black */
cross-fade(url(white.png) 75%, url(black.png) 25%); /* 75% white, 25% black */
cross-fade(url(white.png) 100%, url(black.png) 0%); /* fully white */
cross-fade(url(green.png) 75%, url(red.png) 75%); /* both green and red at 75% */
```

Wenn einige Prozentsätze weggelassen werden, werden alle angegebenen Prozentsätze summiert und von `100%` subtrahiert. Wenn das Ergebnis größer als 0% ist, wird das Ergebnis gleichmäßig zwischen allen Bildern mit ausgelassenen Prozentsätzen aufgeteilt.

Im einfachsten Fall werden zwei Bilder ineinander übergeblendet. Um dies zu tun, braucht nur eines der Bilder einen Prozentsatz, das andere wird entsprechend verblendet. Zum Beispiel ergibt ein Wert von 0% definiert für das erste Bild nur das zweite Bild, während 100% nur das erste ergibt. Ein Wert von 25% zeigt das erste Bild zu 25% und das zweite zu 75%. Der 75%-Wert ist das Inverse, zeigt das erste Bild zu 75% und das zweite zu 25%.

Das Obige könnte auch so geschrieben werden:

```css
cross-fade(url(white.png) 0%, url(black.png)); /* fully black */
cross-fade(url(white.png) 25%, url(black.png)); /* 25% white, 75% black */
cross-fade(url(white.png), url(black.png)); /* 50% white, 50% black */
cross-fade(url(white.png) 75%, url(black.png)); /* 75% white, 25% black */
cross-fade(url(white.png) 100%, url(black.png)); /* fully white */
cross-fade(url(green.png) 75%, url(red.png) 75%); /* both green and red at 75% */
```

Wenn keine Prozentsätze angegeben sind, sind beide Bilder zu 50% deckend, wobei eine cross-fade-Darstellung als gleichmäßige Verschmelzung beider Bilder erfolgt. Das 50%/50%-Beispiel, das oben zu sehen ist, brauchte keine angegebenen Prozentsätze, da wenn ein Prozentwert weggelassen wird, die enthaltenen Prozentsätze zusammengezählt und von 100% subtrahiert werden. Das Ergebnis, wenn es größer als 0 ist, wird dann gleichmäßig zwischen allen Bildern mit ausgelassenen Prozentsätzen aufgeteilt.

Im letzten Beispiel ist die Summe der beiden Prozentsätze nicht 100%, und daher enthalten beide Bilder ihre jeweiligen Deckkräfte.

Wenn keine Prozentsätze angegeben sind und drei Bilder eingeschlossen sind, wird jedes Bild zu 33,33% deckend sein. Die beiden folgenden Zeilen sind (fast) identisch:

```css
cross-fade(url(red.png), url(yellow.png), url(blue.png)); /* all three will be 33.3333% opaque */
cross-fade(url(red.png) 33.33%, url(yellow.png) 33.33%, url(blue.png) 33.33%);
```

### Ältere implementierte Syntax

```css
cross-fade( <image>, <image>, <percentage> )
```

Die Spezifikation für die `cross-fade()`-Funktion erlaubt mehrere Bilder, und für jedes Bild können unabhängig von den anderen Werten Transparenzwerte festgelegt werden. Dies war nicht immer der Fall. Die ursprüngliche Syntax, die in einigen Browsern implementiert wurde, erlaubte nur zwei Bilder, wobei die Summe der Transparenz dieser beiden Bilder genau 100% betragen musste. Die ursprüngliche Syntax wird in Safari unterstützt und mit dem Präfix `-webkit-` in Chrome, Opera und anderen auf Blink basierenden Browsern unterstützt.

```css
cross-fade(url(white.png), url(black.png), 0%);   /* fully black */
cross-fade(url(white.png), url(black.png), 25%);  /* 25% white, 75% black */
cross-fade(url(white.png), url(black.png), 50%);  /* 50% white, 50% black */
cross-fade(url(white.png), url(black.png), 75%);  /* 75% white, 25% black */
cross-fade(url(white.png), url(black.png), 100%); /* fully white */
```

In der implementierten Syntax werden die zwei durch Komma getrennten Bilder zuerst deklariert, gefolgt von einem Komma und einem erforderlichen Prozentwert. Das Weglassen des Kommas oder Prozentsatzes macht den Wert ungültig. Der Prozentsatz ist die Deckkraft des zuerst deklarierten Bildes. Der enthaltene Prozentsatz wird von 100% subtrahiert, wobei die Differenz die Deckkraft des zweiten Bildes darstellt.

Das Grün/Rot-Beispiel (mit den Prozentsätzen 150%) und das Gelb/Rot/Blau-Beispiel (mit drei Bildern) aus dem Abschnitt der Spezifikationssyntax sind in dieser Implementierung nicht möglich.

## Barrierefreiheit

Browser bieten keine speziellen Informationen zu Hintergrundbildern für unterstützende Technologien. Dies ist in erster Linie für Screenreader wichtig, da ein Screenreader dessen Vorhandensein nicht ankündigt und daher dem Benutzer nichts vermittelt. Wenn das Bild Informationen enthält, die für das Verständnis des Gesamtzwecks der Seite entscheidend sind, ist es besser, es semantisch im Dokument zu beschreiben. Beim Verwenden von Hintergrundbildern sollten Sie darauf achten, dass der Farbkontrast groß genug ist, damit jeder Text sowohl über das Bild als auch bei fehlenden Bildern lesbar ist.

- [MDN Understanding WCAG, Leitfaden 1.1 Erklärungen](/de/docs/Web/Accessibility/Guides/Understanding_WCAG/Perceivable#guideline_1.1_—_providing_text_alternatives_for_non-text_content)
- [Understanding Success Criterion 1.1.1 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)

## Formale Syntax

{{csssyntax}}

## Beispiele

### Ältere Syntax für cross-fade

#### HTML

```html
<div class="crossfade"></div>
```

#### CSS

```css
.crossfade {
  width: 300px;
  height: 300px;
  background-image: -webkit-cross-fade(url("br.png"), url("tr.png"), 75%);
  background-image: cross-fade(url("br.png"), url("tr.png"), 75%);
}
```

#### Ergebnis

{{EmbedLiveSample("Older_syntax_for_cross-fade", "330", "330")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{cssxref("image")}}
- {{cssxref("url_value", "&lt;url&gt;")}}
- {{cssxref("image/image", "image()")}}
- {{cssxref("image/image-set", "image-set()")}}
- {{cssxref("element")}}
- [Using CSS gradients](/de/docs/Web/CSS/CSS_images/Using_CSS_gradients)
- Verlauf-Funktionen: {{cssxref("gradient/linear-gradient", "linear-gradient()")}}, {{cssxref("gradient/radial-gradient", "radial-gradient()")}}, {{cssxref("gradient/repeating-linear-gradient", "repeating-linear-gradient()")}}, {{cssxref("gradient/repeating-radial-gradient", "repeating-radial-gradient()")}}, {{cssxref("gradient/conic-gradient", "conic-gradient()")}}, {{cssxref("gradient/repeating-conic-gradient", "repeating-conic-gradient()")}}
