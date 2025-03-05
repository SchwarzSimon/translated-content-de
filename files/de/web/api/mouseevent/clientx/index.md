---
title: "MouseEvent: clientX-Eigenschaft"
short-title: clientX
slug: Web/API/MouseEvent/clientX
l10n:
  sourceCommit: d13c1276b80bbfc940a1091b62f333fe9edc78a2
---

{{APIRef("UI Events")}}

Die schreibgeschützte Eigenschaft **`clientX`** des [`MouseEvent`](/de/docs/Web/API/MouseEvent)-Interfaces liefert die horizontale Koordinate innerhalb des {{Glossary("viewport", "Viewports")}} der Anwendung, an der das Ereignis aufgetreten ist (im Gegensatz zur Koordinate innerhalb der Seite).

Wenn Sie beispielsweise auf den linken Rand des Viewports klicken, führt dies immer zu einem Mausereignis mit einem `clientX`-Wert von `0`, unabhängig davon, ob die Seite horizontal gescrollt ist.

## Wert

Ein `double`-Gleitkommawert in Pixel.

## Beispiele

Dieses Beispiel zeigt Ihre Mauskoordinaten an, wann immer Sie das [`mousemove`](/de/docs/Web/API/Element/mousemove_event)-Ereignis auslösen.

### HTML

```html
<p>Move your mouse to see its position.</p>
<p id="screen-log"></p>
```

### JavaScript

```js
let screenLog = document.querySelector("#screen-log");
document.addEventListener("mousemove", logKey);

function logKey(e) {
  screenLog.innerText = `
    Screen X/Y: ${e.screenX}, ${e.screenY}
    Client X/Y: ${e.clientX}, ${e.clientY}`;
}
```

### Ergebnis

{{EmbedLiveSample("Examples")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`MouseEvent`](/de/docs/Web/API/MouseEvent)
- [`clientY`](/de/docs/Web/API/MouseEvent/clientY)
- [`screenX`](/de/docs/Web/API/MouseEvent/screenX) / [`screenY`](/de/docs/Web/API/MouseEvent/screenY)
- [Koordinatensysteme](/de/docs/Web/CSS/CSSOM_view/Coordinate_systems)
