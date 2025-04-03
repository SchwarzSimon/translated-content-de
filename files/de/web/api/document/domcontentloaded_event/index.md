---
title: "Dokument: DOMContentLoaded-Ereignis"
short-title: DOMContentLoaded
slug: Web/API/Document/DOMContentLoaded_event
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{APIRef}}

Das **`DOMContentLoaded`**-Ereignis wird ausgelöst, wenn das HTML-Dokument vollständig geparst wurde und alle verzögerten Skripte ([`<script defer src="…">`](/de/docs/Web/HTML/Element/script#defer) und [`<script type="module">`](/de/docs/Web/HTML/Element/script#module)) heruntergeladen und ausgeführt wurden. Es wartet nicht darauf, dass andere Elemente wie Bilder, Unterrahmen und asynchrone Skripte fertig geladen sind.

`DOMContentLoaded` wartet nicht auf das Laden von Stylesheets, jedoch warten verzögerte Skripte _auf_ Stylesheets, und das `DOMContentLoaded`-Ereignis wird nach verzögerten Skripten in die Warteschlange gestellt. Auch Skripte, die weder verzögert noch asynchron sind (z.B. `<script>`), warten darauf, dass bereits geparste Stylesheets geladen werden.

Ein anderes Ereignis, [`load`](/de/docs/Web/API/Window/load_event), sollte nur verwendet werden, um eine vollständig geladene Seite zu erkennen. Es ist ein häufiger Fehler, `load` zu verwenden, wo `DOMContentLoaded` angemessener wäre.

Dieses Ereignis ist nicht abbrechbar.

## Syntax

Verwenden Sie den Ereignisnamen in Methoden wie [`addEventListener()`](/de/docs/Web/API/EventTarget/addEventListener) oder setzen Sie eine Event-Handler-Eigenschaft.

```js
addEventListener("DOMContentLoaded", (event) => {});
```

## Ereignistyp

Ein generisches [`Event`](/de/docs/Web/API/Event).

## Beispiele

### Grundlegende Verwendung

```js
document.addEventListener("DOMContentLoaded", (event) => {
  console.log("DOM fully loaded and parsed");
});
```

### Verzögerung von DOMContentLoaded

```html
<script>
  document.addEventListener("DOMContentLoaded", (event) => {
    console.log("DOM fully loaded and parsed");
  });

  for (let i = 0; i < 1_000_000_000; i++);
  // This synchronous script is going to delay parsing of the DOM,
  // so the DOMContentLoaded event is going to launch later.
</script>
```

### Überprüfung ob die Ladephase bereits abgeschlossen ist

`DOMContentLoaded` kann ausgelöst werden, bevor Ihr Skript die Chance hat, ausgeführt zu werden. Es ist daher ratsam, dies zu überprüfen, bevor Sie einen Listener hinzufügen.

```js
function doSomething() {
  console.info("DOM loaded");
}

if (document.readyState === "loading") {
  // Loading hasn't finished yet
  document.addEventListener("DOMContentLoaded", doSomething);
} else {
  // `DOMContentLoaded` has already fired
  doSomething();
}
```

> [!NOTE]
> Hier gibt es keine Race-Bedingung – es ist nicht möglich, dass das Dokument zwischen der `if`-Überprüfung und dem `addEventListener()`-Aufruf geladen wird. JavaScript hat Semantiken zur Fertigstellung, was bedeutet, dass, wenn sich das Dokument in einem bestimmten Tick der Ereignisschleife im Ladevorgang befindet, es erst im nächsten Zyklus geladen werden kann, zu welchem Zeitpunkt der `doSomething`-Handler bereits angefügt ist und ausgeführt wird.

### Live-Beispiel

#### HTML

```html
<div class="controls">
  <button id="reload" type="button">Reload</button>
</div>

<div class="event-log">
  <label for="eventLog">Event log:</label>
  <textarea
    readonly
    class="event-log-contents"
    rows="8"
    cols="30"
    id="eventLog"></textarea>
</div>
```

```css hidden
body {
  display: grid;
  grid-template-areas: "control log";
}

.controls {
  grid-area: control;
  display: flex;
  align-items: center;
  justify-content: center;
}

.event-log {
  grid-area: log;
}

.event-log-contents {
  resize: none;
}

label,
button {
  display: block;
}

#reload {
  height: 2rem;
}
```

#### JavaScript

```js
const log = document.querySelector(".event-log-contents");
const reload = document.querySelector("#reload");

reload.addEventListener("click", () => {
  log.textContent = "";
  setTimeout(() => {
    window.location.reload(true);
  }, 200);
});

window.addEventListener("load", (event) => {
  log.textContent += "load\n";
});

document.addEventListener("readystatechange", (event) => {
  log.textContent += `readystate: ${document.readyState}\n`;
});

document.addEventListener("DOMContentLoaded", (event) => {
  log.textContent += "DOMContentLoaded\n";
});
```

#### Ergebnis

{{ EmbedLiveSample('Live_example', '100%', '160px') }}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- Verwandte Ereignisse: [`load`](/de/docs/Web/API/Window/load_event), [`readystatechange`](/de/docs/Web/API/Document/readystatechange_event), [`beforeunload`](/de/docs/Web/API/Window/beforeunload_event), [`unload`](/de/docs/Web/API/Window/unload_event)
