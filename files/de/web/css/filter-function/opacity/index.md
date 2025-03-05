---
title: opacity()
slug: Web/CSS/filter-function/opacity
l10n:
  sourceCommit: 9ca1b6d1fe5e69fc288ad18c6986b581afafc0a4
---

{{CSSRef}}

Die **`opacity()`** [CSS](/de/docs/Web/CSS) [Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) wendet Transparenz auf die Proben im Eingabebild an. Das Ergebnis ist eine {{cssxref("&lt;filter-function&gt;")}}.

{{EmbedInteractiveExample("pages/css/function-opacity.html")}}

> [!NOTE]
> Diese Funktion ähnelt der etablierteren {{Cssxref("opacity")}}-Eigenschaft. Der Unterschied besteht darin, dass einige Browser bei Filtern Hardwarebeschleunigung für bessere Leistung bieten.

## Syntax

```css
opacity(amount)
```

### Parameter

- `amount` {{Optional_Inline}}
  - : Die Menge der Umwandlung, angegeben als {{cssxref("&lt;number&gt;")}} oder {{cssxref("&lt;percentage&gt;")}}. Ein Wert von `0%` ist vollständig transparent, während ein Wert von `100%` das Eingabebild unverändert lässt. Werte zwischen `0%` und `100%` sind lineare Multiplikatoren auf den Effekt. Der Anfangswert für die {{Glossary("interpolation", "Interpolation")}} ist `1`. Der Standardwert ist `1`.

## Formale Syntax

{{CSSSyntax}}

## Beispiele

### Beispiele für korrekte Werte für opacity()

```css
opacity(0%)   /* Completely transparent */
opacity(50%)  /* 50% transparent */

opacity()     /* No effect */
opacity(1)
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- Die anderen {{cssxref("&lt;filter-function&gt;")}}-Funktionen, die in den Werten der Eigenschaften {{cssxref("filter")}} und {{cssxref("backdrop-filter")}} verwendet werden können, umfassen:
  - {{cssxref("filter-function/blur", "blur()")}}
  - {{cssxref("filter-function/brightness", "brightness()")}}
  - {{cssxref("filter-function/contrast", "contrast()")}}
  - {{cssxref("filter-function/drop-shadow", "drop-shadow()")}}
  - {{cssxref("filter-function/grayscale", "grayscale()")}}
  - {{cssxref("filter-function/hue-rotate", "hue-rotate()")}}
  - {{cssxref("filter-function/invert", "invert()")}}
  - {{cssxref("filter-function/saturate", "saturate()")}}
  - {{cssxref("filter-function/sepia", "sepia()")}}
- Die CSS {{cssxref("opacity")}}-Eigenschaft
