---
title: "Window: devicePixelRatio-Eigenschaft"
short-title: devicePixelRatio
slug: Web/API/Window/devicePixelRatio
l10n:
  sourceCommit: 874ad29df9150037acb8a4a3e7550a302c90a080
---

{{APIRef}}

Die **`devicePixelRatio`**-Eigenschaft des [`Window`](/de/docs/Web/API/Window)-Interfaces gibt das Verhältnis der Auflösung in _physischen Pixeln_ zur Auflösung in _CSS-Pixeln_ für das aktuelle Anzeigegerät zurück.

Dieser Wert kann auch als Verhältnis der Pixelgrößen interpretiert werden: die Größe eines _CSS-Pixels_ zur Größe eines _physischen Pixels_. Einfacher ausgedrückt teilt dies dem Browser mit, wie viele tatsächliche Bildschirm-Pixel verwendet werden sollten, um einen einzelnen CSS-Pixel zu zeichnen.

Das Zoomen der Seite beeinflusst den Wert von `devicePixelRatio`. Wenn eine Seite vergrößert wird, erhöht sich die Größe eines CSS-Pixels, und somit steigt der `devicePixelRatio`-Wert. Das Pinch-Zoomen beeinflusst `devicePixelRatio` nicht, da dadurch die Seite vergrößert wird, ohne die Größe eines CSS-Pixels zu ändern.

Dies ist nützlich, wenn es um den Unterschied zwischen dem Rendering auf einem Standarddisplay und einem HiDPI- oder Retina-Display geht, die mehr Bildschirm-Pixel verwenden, um die gleichen Objekte zu zeichnen, was zu einem schärferen Bild führt.

Sie können [`window.matchMedia()`](/de/docs/Web/API/Window/matchMedia) verwenden, um zu prüfen, ob sich der Wert von `devicePixelRatio` ändert (was beispielsweise passieren kann, wenn der Benutzer das Fenster auf ein Display mit einer anderen Pixeldichte zieht). Siehe [das untenstehende Beispiel](#überwachung_von_bildschirmauflösung_oder_zoom-level-änderungen).

## Wert

Ein Gleitkommawert mit doppelter Genauigkeit, der das Verhältnis der Auflösung des Displays in physischen Pixeln zur Auflösung in CSS-Pixeln anzeigt. Ein Wert von 1 zeigt ein klassisches 96 DPI-Display an, während ein Wert von 2 für HiDPI/Retina-Displays erwartet wird.

Andere Werte können bei ungewöhnlich niedrig auflösenden Displays oder öfter, wenn ein Bildschirm eine höhere Pixeldichte als das Doppelte der Standardauflösung von 96 DPI hat, zurückgegeben werden. Moderne mobile Geräte - die eine hohe Anzeigeauflösung bei kleinen physischen Größen bieten - führen häufig zu einem `devicePixelRatio`-Wert größer als 2.

## Beispiele

### Korrektur der Auflösung in einem `<canvas>`

Ein {{htmlelement("canvas")}} kann auf Retina-Bildschirmen zu unscharf erscheinen. Verwenden Sie `window.devicePixelRatio`, um zu bestimmen, wie viel extra Pixeldichte hinzugefügt werden sollte, um ein schärferes Bild zu ermöglichen.

#### HTML

```html
<canvas id="canvas"></canvas>
```

#### JavaScript

```js
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

// Set display size (css pixels).
const size = 200;
canvas.style.width = `${size}px`;
canvas.style.height = `${size}px`;

// Set actual size in memory (scaled to account for extra pixel density).
const scale = window.devicePixelRatio; // Change to 1 on retina screens to see blurry canvas.
canvas.width = Math.floor(size * scale);
canvas.height = Math.floor(size * scale);

// Normalize coordinate system to use CSS pixels.
ctx.scale(scale, scale);

ctx.fillStyle = "#bada55";
ctx.fillRect(10, 10, 300, 300);
ctx.fillStyle = "#ffffff";
ctx.font = "18px Arial";
ctx.textAlign = "center";
ctx.textBaseline = "middle";

const x = size / 2;
const y = size / 2;

const textString = "I love MDN";
ctx.fillText(textString, x, y);
```

![Vergleich nebeneinander der Wirkung unterschiedlicher devicePixelRatio-Werte auf ein Bild, das auf einem Retina-Display angezeigt wird.](devicepixelratio_diff.png)

### Überwachung von Bildschirmauflösung oder Zoom-Level-Änderungen

In diesem Beispiel richten wir eine Media Query ein und überwachen sie, um zu sehen, wann sich die Geräteauflösung ändert und protokollieren die neue Auflösung.

#### HTML

```html
<div id="container">
  <p>
    This example demonstrates the effect of zooming the page in and out (or
    moving it to a screen with a different scaling factor) on the value of the
    <code>devicePixelRatio</code> property.
  </p>
  <p>Try it and watch what happens!</p>
</div>
<div id="output"></div>
```

#### CSS

```css
body {
  font:
    22px arial,
    sans-serif;
}

#container {
  border: 2px solid #22d;
  margin: 1rem auto;
  padding: 1rem;
  background-color: #a9f;
}
```

#### JavaScript

Der String `mqString` wird auf eine Media Query gesetzt, die überprüft, ob die aktuelle Anzeigegeräteauflösung einer spezifischen Anzahl von Gerätepunkten pro `px` entspricht.

Die Variable `media` ist ein [`MediaQueryList`](/de/docs/Web/API/MediaQueryList)-Objekt, das mit dem Media Query-String initialisiert wird. Wenn das Ergebnis der Ausführung von `mqString` gegen das Dokument sich ändert, löst das `change`-Ereignis des `media`-Objekts aus und der Code protokolliert die neue Auflösung.

Beachten Sie, dass jedes Mal, wenn sich die Auflösung ändert, das Beispiel eine neue Media Query, basierend auf der neuen Auflösung, und eine neue `MediaQueryList`-Instanz erstellen muss.

```js
let remove = null;
const output = document.querySelector("#output");

const updatePixelRatio = () => {
  if (remove != null) {
    remove();
  }
  const mqString = `(resolution: ${window.devicePixelRatio}dppx)`;
  const media = matchMedia(mqString);
  media.addEventListener("change", updatePixelRatio);
  remove = () => {
    media.removeEventListener("change", updatePixelRatio);
  };

  output.textContent = `devicePixelRatio: ${window.devicePixelRatio}`;
};

updatePixelRatio();
```

#### Ergebnis

Um das Beispiel zu testen, versuchen Sie, die Seite ein- und auszuzoomen und beachten Sie den Unterschied im protokollierten Wert von `devicePixelRatio`.

{{EmbedLiveSample("Monitoring_screen_resolution_or_zoom_level_changes", "100%", 300)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Media queries](/de/docs/Web/CSS/CSS_media_queries)
- [Verwendung von Media Queries](/de/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- [CSS `resolution`-Media Query](/de/docs/Web/CSS/@media/resolution)
- Die {{cssxref("image-resolution")}}-Eigenschaft
