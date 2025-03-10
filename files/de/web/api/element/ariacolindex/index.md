---
title: "Element: ariaColIndex-Eigenschaft"
short-title: ariaColIndex
slug: Web/API/Element/ariaColIndex
l10n:
  sourceCommit: f65f7f6e4fda2cb1bd0e7db17777e2cb20be7d27
---

{{APIRef("DOM")}}

Die **`ariaColIndex`**-Eigenschaft der [`Element`](/de/docs/Web/API/Element)-Schnittstelle spiegelt den Wert des [`aria-colindex`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-colindex)-Attributs wider, das den Spaltenindex oder die Position eines Elements in Bezug auf die Gesamtanzahl der Spalten innerhalb einer Tabelle, eines Rasters oder eines Baumrasters definiert.

## Wert

Ein String, der eine ganze Zahl enthält.

## Beispiele

In diesem Beispiel wird das `aria-colindex`-Attribut des Elements mit der ID `role-heading` auf "1" gesetzt. Mit `ariaColIndex` aktualisieren wir den Wert auf "2".

```html
<table
  id="semantic-table"
  role="table"
  aria-label="Semantic Elements"
  aria-describedby="semantic_elements_table_desc"
  aria-rowcount="100">
  <caption id="semantic_elements_table_desc">
    Semantic Elements to use instead of ARIA's roles
  </caption>
  <thead role="rowgroup">
    <tr role="row">
      <th
        role="columnheader"
        id="role-heading"
        aria-sort="none"
        aria-rowindex="1"
        aria-colindex="1">
        ARIA Role
      </th>
      <th
        role="columnheader"
        id="element-heading"
        aria-sort="none"
        aria-rowindex="1">
        Semantic Element
      </th>
    </tr>
  </thead>
  <tbody role="rowgroup">
    <tr role="row">
      <td role="cell" aria-rowindex="11">header</td>
      <td role="cell" aria-rowindex="11">h1</td>
    </tr>
    <tr role="row">
      <td role="cell" aria-rowindex="16">header</td>
      <td role="cell" aria-rowindex="16">h6</td>
    </tr>
    <tr role="row">
      <td role="cell" aria-rowindex="18">rowgroup</td>
      <td role="cell" aria-rowindex="18">thead</td>
    </tr>
    <tr role="row">
      <td role="cell" aria-rowindex="24">term</td>
      <td role="cell" aria-rowindex="24">dt</td>
    </tr>
  </tbody>
</table>
```

```js
let el = document.getElementById("role-heading");
console.log(el.ariaColIndex); // 1
el.ariaColIndex = "2";
console.log(el.ariaColIndex); // 2
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [ARIA: table-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/table_role)
