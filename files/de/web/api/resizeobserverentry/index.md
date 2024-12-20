---
title: ResizeObserverEntry
slug: Web/API/ResizeObserverEntry
l10n:
  sourceCommit: 5b20f5f4265f988f80f513db0e4b35c7e0cd70dc
---

{{APIRef("Resize Observer API")}}

Das **`ResizeObserverEntry`**-Interface repräsentiert das Objekt, das der Callback-Funktion des Konstruktors von [`ResizeObserver()`](/de/docs/Web/API/ResizeObserver/ResizeObserver) übergeben wird. Es ermöglicht Ihnen, auf die neuen Abmessungen des beobachteten [`Element`](/de/docs/Web/API/Element) oder [`SVGElement`](/de/docs/Web/API/SVGElement) zuzugreifen.

## Instanz-Eigenschaften

- [`ResizeObserverEntry.borderBoxSize`](/de/docs/Web/API/ResizeObserverEntry/borderBoxSize) {{ReadOnlyInline}}
  - : Ein Array von Objekten, das die neue Größe des Border-Box des beobachteten Elements enthält, wenn der Callback ausgeführt wird.
- [`ResizeObserverEntry.contentBoxSize`](/de/docs/Web/API/ResizeObserverEntry/contentBoxSize) {{ReadOnlyInline}}
  - : Ein Array von Objekten, das die neue Größe des Content-Box des beobachteten Elements enthält, wenn der Callback ausgeführt wird.
- [`ResizeObserverEntry.devicePixelContentBoxSize`](/de/docs/Web/API/ResizeObserverEntry/devicePixelContentBoxSize) {{ReadOnlyInline}}
  - : Ein Array von Objekten, das die neue Größe des Content-Box in Geräte-Pixeln des beobachteten Elements enthält, wenn der Callback ausgeführt wird.
- [`ResizeObserverEntry.contentRect`](/de/docs/Web/API/ResizeObserverEntry/contentRect) {{ReadOnlyInline}}
  - : Ein [`DOMRectReadOnly`](/de/docs/Web/API/DOMRectReadOnly)-Objekt, das die neue Größe des beobachteten Elements enthält, wenn der Callback ausgeführt wird. Beachten Sie, dass dies jetzt eine veraltete Eigenschaft ist, die aus Gründen der Rückwärtskompatibilität in der Spezifikation beibehalten wird.
- [`ResizeObserverEntry.target`](/de/docs/Web/API/ResizeObserverEntry/target) {{ReadOnlyInline}}
  - : Eine Referenz auf das beobachtete [`Element`](/de/docs/Web/API/Element) oder [`SVGElement`](/de/docs/Web/API/SVGElement).

> [!NOTE]
> Die Content-Box ist der Bereich, in dem Inhalte platziert werden können, also die Border-Box abzüglich des Paddings und der Breite des Rahmens. Die Border-Box umfasst den Inhalt, das Padding und den Rahmen. Siehe [Das Box-Modell](/de/docs/Learn_web_development/Core/Styling_basics/Box_model) für eine weitere Erklärung.

## Instanz-Methoden

Keine.

## Beispiele

Der folgende Ausschnitt stammt aus dem [resize-observer-text.html](https://mdn.github.io/dom-examples/resize-observer/resize-observer-text.html) ([siehe Quelle](https://github.com/mdn/dom-examples/blob/main/resize-observer/resize-observer-text.html)) Beispiel.

Beachten Sie, dass der Code drei verschiedene Kompatibilitätsfälle abdeckt:

- Einige alte Browser unterstützen möglicherweise `contentRect`, aber nicht `contentBoxSize`.
- Alte Versionen von Firefox unterstützen `contentBoxSize`, haben es jedoch fälschlicherweise als einzelnes Objekt anstelle eines Arrays implementiert.
- Moderne Browser unterstützen `contentBoxSize` als ein Array von Objekten, um die Meldung von Box-Größen für fragmentierte Elemente zu ermöglichen (zum Beispiel in einem Mehrspaltenszenario).

```js
const resizeObserver = new ResizeObserver((entries) => {
  for (let entry of entries) {
    if (entry.contentBoxSize) {
      // The standard makes contentBoxSize an array...
      if (entry.contentBoxSize[0]) {
        h1Elem.style.fontSize =
          Math.max(1.5, entry.contentBoxSize[0].inlineSize / 200) + "rem";
        pElem.style.fontSize =
          Math.max(1, entry.contentBoxSize[0].inlineSize / 600) + "rem";
      } else {
        // ...but old versions of Firefox treat it as a single item
        h1Elem.style.fontSize =
          Math.max(1.5, entry.contentBoxSize.inlineSize / 200) + "rem";
        pElem.style.fontSize =
          Math.max(1, entry.contentBoxSize.inlineSize / 600) + "rem";
      }
    } else {
      h1Elem.style.fontSize =
        Math.max(1.5, entry.contentRect.width / 200) + "rem";
      pElem.style.fontSize = Math.max(1, entry.contentRect.width / 600) + "rem";
    }
  }
  console.log("Size changed");
});

resizeObserver.observe(divElem);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
