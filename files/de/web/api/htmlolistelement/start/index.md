---
title: "HTMLOListElement: start-Eigenschaft"
short-title: start
slug: Web/API/HTMLOListElement/start
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{ApiRef("HTML DOM")}}

Die **`start`**-Eigenschaft der [`HTMLOListElement`](/de/docs/Web/API/HTMLOListElement)-Schnittstelle gibt den Startwert der nummerierten Liste an, mit einem Standardwert von 1.

Sie spiegelt das [`start`](/de/docs/Web/HTML/Reference/Elements/ol#start)-Attribut des {{HTMLElement("ol")}}-Elements wider.

> [!NOTE]
> Der Wert der `start`-Eigenschaft ist unabhängig von der [`HTMLOListElement.type`](/de/docs/Web/API/HTMLOListElement/type)-Eigenschaft; er ist immer numerisch, auch wenn der Typ Buchstaben oder römische Ziffern ist.

## Wert

Ein `long`-Wert.

## Beispiele

### HTML

```html
<ol id="order-list">
  <li>Fee</li>
  <li>Fi</li>
  <li>Fo</li>
  <li>Fum</li>
</ol>
```

### JavaScript

```js
const olElement = document.querySelector("#order-list");
console.log(olElement.start); // Output: "1"
olElement.start = "11";
console.log(olElement.start); // Output: "11"
```

### Ergebnis

{{EmbedLiveSample("Examples", 400, 100)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
