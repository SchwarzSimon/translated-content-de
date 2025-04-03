---
title: "StylePropertyMap: set()-Methode"
short-title: set()
slug: Web/API/StylePropertyMap/set
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{APIRef("CSS Typed Object Model API")}}

Die **`set()`**-Methode des [`StylePropertyMap`](/de/docs/Web/API/StylePropertyMap)-Interfaces ändert die CSS-Deklaration mit der angegebenen Eigenschaft.

## Syntax

```js-nolint
set(property, value)
```

### Parameter

- `property`
  - : Ein Bezeichner, der das stilistische Merkmal angibt (z.B. Schriftart, Breite, Hintergrundfarbe), das geändert werden soll.
- `value`
  - : Der Wert, den die angegebene Eigenschaft haben soll.

### Rückgabewert

Kein ({{jsxref("undefined")}}).

## Beispiele

Dieses Beispiel setzt die {{cssxref('padding-top')}}-Eigenschaft mit dem angegebenen Wert innerhalb des [style-Attributs](/de/docs/Web/HTML/Global_attributes/style) des Elements.

```js
// get the button element
const buttonEl = document.querySelector("button");

// set padding-top on button style attribute
buttonEl.attributeStyleMap.set("padding-top", CSS.px(10));
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
