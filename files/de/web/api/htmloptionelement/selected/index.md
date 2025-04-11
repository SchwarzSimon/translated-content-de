---
title: "HTMLOptionElement: selected-Eigenschaft"
short-title: selected
slug: Web/API/HTMLOptionElement/selected
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{ APIRef("HTML DOM") }}

Die **`selected`**-Eigenschaft des [`HTMLOptionElement`](/de/docs/Web/API/HTMLOptionElement)-Interfaces gibt die aktuelle Ausgewähltkeit des Elements an; das heißt, ob das {{HTMLElement("option")}} ausgewählt ist oder nicht.

Das Vorhandensein des HTML-Attributs [`selected`](/de/docs/Web/HTML/Reference/Elements/option#selected) zeigt an, dass die Option standardmäßig ausgewählt ist. Es zeigt nicht an, ob diese Option derzeit ausgewählt ist: Wenn sich der Status der Option ändert, spiegelt das `selected`-Inhaltsattribut die Änderung nicht wider; nur die `selected` IDL-Eigenschaft des `HTMLOptionElement` wird aktualisiert. Das `selected`-Attribut wird durch die [`defaultSelected`](/de/docs/Web/API/HTMLOptionElement/defaultSelected)-Eigenschaft widergespiegelt.

## Wert

Ein Boolean.

## Beispiele

```js
const optionElement = document.getElementById("water");
console.log(optionElement.selected);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{HTMLElement("option")}}
- {{HTMLElement("select")}}
- [`HTMLOptionElement.defaultSelected`](/de/docs/Web/API/HTMLOptionElement/defaultSelected)
- [`HTMLOptionElement.index`](/de/docs/Web/API/HTMLOptionElement/index)
- [`HTMLOptionsCollection`](/de/docs/Web/API/HTMLOptionsCollection)
- [`HTMLSelectElement.selectedIndex`](/de/docs/Web/API/HTMLSelectElement/selectedIndex)
