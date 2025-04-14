---
title: "Element: ariaColSpan-Eigenschaft"
short-title: ariaColSpan
slug: Web/API/Element/ariaColSpan
l10n:
  sourceCommit: 874ad29df9150037acb8a4a3e7550a302c90a080
---

{{APIRef("DOM")}}

Die **`ariaColSpan`**-Eigenschaft des [`Element`](/de/docs/Web/API/Element)-Interfaces spiegelt den Wert des [`aria-colspan`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-colspan)-Attributs wider, welches die Anzahl der Spalten definiert, die von einer Zelle oder Gridcell innerhalb einer Tabelle, eines Grids oder Treegrids überspannt werden.

## Wert

Ein String, der eine Ganzzahl enthält.

## Beispiele

In diesem Beispiel wird das `aria-colspan`-Attribut des Elements mit der ID `spanning-heading` auf "2" gesetzt. Mit `ariaColSpan` aktualisieren wir den Wert auf "3".

```html
<table>
  <tr>
    <th>Heading 1</th>
    <th>Heading 2</th>
    <th>Heading 3</th>
  </tr>
  <tr>
    <td colspan="2" aria-colspan="2" id="spanning-column">Spanning</td>
    <td>One</td>
  </tr>
</table>
```

```js
let el = document.getElementById("spanning-column");
console.log(el.ariaColSpan);
el.ariaColSpan = "3";
console.log(el.ariaColSpan);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [ARIA: table role](/de/docs/Web/Accessibility/ARIA/Reference/Roles/table_role)
