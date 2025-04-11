---
title: "HTMLImageElement: Image() Konstruktor"
short-title: Image()
slug: Web/API/HTMLImageElement/Image
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{APIRef("HTML DOM")}}

Der **`Image()`**
Konstruktor erstellt eine neue Instanz von [`HTMLImageElement`](/de/docs/Web/API/HTMLImageElement). Er ist funktional
äquivalent zu [`document.createElement('img')`](/de/docs/Web/API/Document/createElement).

> [!NOTE]
> Diese Funktion sollte nicht mit der CSS-Funktion [`image()`](/de/docs/Web/CSS/image/image) verwechselt werden.

## Syntax

```js-nolint
new Image()
new Image(width)
new Image(width, height)
```

### Parameter

- `width` {{optional_inline}}
  - : Die Breite des Bildes (d.h. der Wert für das [`width`](/de/docs/Web/HTML/Reference/Elements/img#width)
    Attribut).
- `height` {{optional_inline}}
  - : Die Höhe des Bildes (d.h. der Wert für das [`height`](/de/docs/Web/HTML/Reference/Elements/img#height)
    Attribut).

## Anwendungshinweis

Das gesamte Bitmap wird geladen, unabhängig von den im Konstruktor angegebenen Größen. Die
im Konstruktor angegebene Größe spiegelt sich in den Eigenschaften
[`HTMLImageElement.width`](/de/docs/Web/API/HTMLImageElement/width) und [`HTMLImageElement.height`](/de/docs/Web/API/HTMLImageElement/height) der
resultierenden Instanz wider. Die intrinsische Breite und Höhe des Bildes in CSS-Pixeln werden
durch die Eigenschaften [`HTMLImageElement.naturalWidth`](/de/docs/Web/API/HTMLImageElement/naturalWidth) und
[`HTMLImageElement.naturalHeight`](/de/docs/Web/API/HTMLImageElement/naturalHeight) widergespiegelt. Wenn im
Konstruktor keine Größe angegeben wird, haben beide Eigenschaftspaare dieselben Werte.

## Beispiele

```js
const myImage = new Image(100, 200);
myImage.src = "picture.jpg";
document.body.appendChild(myImage);
```

Dies wäre gleichbedeutend mit der Definition des folgenden HTML-Tags innerhalb des
{{HTMLElement("body")}}:

```html
<img width="100" height="200" src="picture.jpg" />
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
