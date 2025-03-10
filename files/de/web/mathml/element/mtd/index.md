---
title: <mtd>
slug: Web/MathML/Element/mtd
l10n:
  sourceCommit: f65f7f6e4fda2cb1bd0e7db17777e2cb20be7d27
---

{{MathMLRef}}

Das **`<mtd>`** [MathML](/de/docs/Web/MathML)-Element repräsentiert eine Zelle in einer Tabelle oder einer Matrix. Es darf nur in einem {{ MathMLElement("mtr") }}-Element vorkommen. Dieses Element ist dem {{ HTMLElement("td") }}-Element von [HTML](/de/docs/Web/HTML) ähnlich.

## Attribute

Die Attribute dieses Elements umfassen die [globalen MathML-Attribute](/de/docs/Web/MathML/Global_attributes) sowie die folgenden Attribute:

- `columnspan`
  - : Ein nicht-negativer ganzzahliger Wert, der angibt, über wie viele Spalten sich die Zelle erstreckt.
- `rowspan`
  - : Ein nicht-negativer ganzzahliger Wert, der angibt, über wie viele Zeilen sich die Zelle erstreckt.

Einige Browser unterstützen möglicherweise auch die folgenden Attribute:

- `columnalign` {{Non-standard_Inline}}
  - : Gibt die horizontale Ausrichtung dieser Zelle an und überschreibt die von {{ MathMLElement("mtable") }} oder {{ MathMLElement("mtr") }} festgelegten Werte.
    Mögliche Werte sind: `left`, `center` und `right`.
- `rowalign` {{Non-standard_Inline}}
  - : Gibt die vertikale Ausrichtung dieser Zelle an und überschreibt die von {{ MathMLElement("mtable") }} oder {{ MathMLElement("mtr") }} festgelegten Werte.
    Mögliche Werte sind: `axis`, `baseline`, `bottom`, `center` und `top`.

## Beispiele

### Matrix mit mtable, mrow, mtr und mtd

```html
<math display="block">
  <mfrac>
    <mi>A</mi>
    <mn>2</mn>
  </mfrac>
  <mo>=</mo>
  <mrow>
    <mo>(</mo>
    <mtable>
      <mtr>
        <mtd><mn>1</mn></mtd>
        <mtd><mn>2</mn></mtd>
        <mtd><mn>3</mn></mtd>
      </mtr>
      <mtr>
        <mtd><mn>4</mn></mtd>
        <mtd><mn>5</mn></mtd>
        <mtd><mn>6</mn></mtd>
      </mtr>
      <mtr>
        <mtd><mn>7</mn></mtd>
        <mtd><mn>8</mn></mtd>
        <mtd><mn>9</mn></mtd>
      </mtr>
    </mtable>
    <mo>)</mo>
  </mrow>
</math>
```

{{EmbedLiveSample('Alignment with row number')}}

## Technische Zusammenfassung

<table class="properties">
  <tr>
    <th scope="row">
      <a href="/de/docs/Web/Accessibility/ARIA/Reference/Roles">Implizierte ARIA-Rolle</a>
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

- {{ MathMLElement("mtable") }}
- {{ MathMLElement("mtr") }}
