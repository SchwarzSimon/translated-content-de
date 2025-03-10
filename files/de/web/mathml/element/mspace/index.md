---
title: <mspace>
slug: Web/MathML/Element/mspace
l10n:
  sourceCommit: f65f7f6e4fda2cb1bd0e7db17777e2cb20be7d27
---

{{MathMLRef}}

Das **`<mspace>`** [MathML](/de/docs/Web/MathML) Element wird verwendet, um einen Leerraum anzuzeigen, dessen Größe durch seine Attribute festgelegt wird.

## Attribute

Die Attribute dieses Elements umfassen die [globalen MathML-Attribute](/de/docs/Web/MathML/Global_attributes) sowie die folgenden Attribute:

- `depth`
  - : Ein {{cssxref("length-percentage")}}, das die gewünschte Tiefe (unterhalb der Grundlinie) des Raums angibt.
- `height`
  - : Ein {{cssxref("length-percentage")}}, das die gewünschte Höhe (oberhalb der Grundlinie) des Raums angibt.
- `width`
  - : Ein {{cssxref("length-percentage")}}, das die gewünschte Breite des Raums angibt.

> [!NOTE]
> Für die Attribute `depth`, `height`, `width` könnten einige Browser auch [veraltete MathML-Längen](/de/docs/Web/MathML/Values#legacy_mathml_lengths) akzeptieren.

## Beispiele

```html
<math display="block">
  <mn>1</mn>
  <mspace
    depth="40px"
    height="20px"
    width="100px"
    style="background: lightblue" />
  <mn>2</mn>
</math>
```

{{EmbedLiveSample('Examples')}}

## Technische Zusammenfassung

<table class="properties">
  <tr>
    <th scope="row">
      <a href="/de/docs/Web/Accessibility/ARIA/Reference/Roles">Implizite ARIA-Rolle</a>
    </th>
    <td>
      Keine
    </td>
  </tr>
</table>

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{ MathMLElement("mpadded") }}
- {{ MathMLElement("mphantom") }}
