---
title: "EventTarget: Methode addEventListener()"
short-title: addEventListener()
slug: Web/API/EventTarget/addEventListener
l10n:
  sourceCommit: 8f4599ce0c63ac1c260933b1458e4da33ce972d5
---

{{APIRef("DOM")}}{{AvailableInWorkers}}

Die **`addEventListener()`**-Methode des [`EventTarget`](/de/docs/Web/API/EventTarget)-Interfaces
richtet eine Funktion ein, die immer dann aufgerufen wird, wenn das angegebene Ereignis an das Ziel übermittelt wird.

Gängige Ziele sind [`Element`](/de/docs/Web/API/Element) oder dessen Kinder, [`Document`](/de/docs/Web/API/Document) und [`Window`](/de/docs/Web/API/Window),
aber das Ziel kann jedes Objekt sein, das Ereignisse unterstützt (wie z.B. [`IDBRequest`](/de/docs/Web/API/IDBRequest)).

> [!NOTE]
> Die `addEventListener()`-Methode ist die _empfohlene_ Art, einen Ereignislistener zu registrieren. Die Vorteile sind folgende:
>
> - Sie ermöglicht die Hinzufügung mehrerer Handler für ein Ereignis. Dies ist besonders nützlich für Bibliotheken, JavaScript-Module oder jede andere Art von Code, der gut mit anderen Bibliotheken oder Erweiterungen funktionieren muss.
> - Im Gegensatz zur Verwendung einer `onXYZ`-Eigenschaft bietet sie eine feinere Kontrolle über die Phase, in der der Listener aktiviert wird (Erfassung vs. Blasen).
> - Sie funktioniert mit jedem Ereignisziel, nicht nur mit HTML- oder SVG-Elementen.

Die Methode `addEventListener()` funktioniert, indem sie eine Funktion oder ein Objekt, das eine `handleEvent()`-Funktion implementiert, der Liste der Ereignislistener für den angegebenen Ereignistyp hinzufügt,
auf dem [`EventTarget`](/de/docs/Web/API/EventTarget), auf dem sie aufgerufen wird. Wenn die Funktion oder das Objekt bereits in der Liste der Ereignislistener für dieses Ziel enthalten ist, wird sie nicht ein zweites Mal hinzugefügt.

> [!NOTE]
> Wenn eine bestimmte anonyme Funktion in der Liste der Ereignislistener registriert ist, und später im Code eine identische anonyme Funktion in einem `addEventListener`-Aufruf angegeben wird, wird die zweite Funktion _auch_ zur Liste der Ereignislistener für dieses Ziel hinzugefügt.
>
> Tatsächlich sind anonyme Funktionen nicht identisch, auch wenn sie mit demselben unveränderten Quellcode wiederholt definiert werden, **sogar in einer Schleife**.
>
> Das wiederholte Definieren derselben namenlosen Funktion in solchen Fällen kann problematisch sein. (Siehe [Speicherprobleme](#speicherprobleme) unten.)

Wenn ein Ereignislistener während der Verarbeitung des Ereignisses zu einem [`EventTarget`](/de/docs/Web/API/EventTarget) aus einem anderen Listener hinzugefügt wird, wird dieses Ereignis den neuen Listener nicht auslösen. Der neue Listener kann jedoch während einer späteren Phase des Ereignisflusses ausgelöst werden, z.B. während der Blasenphase.

## Syntax

```js-nolint
addEventListener(type, listener)
addEventListener(type, listener, options)
addEventListener(type, listener, useCapture)
```

### Parameter

- `type`
  - : Ein groß-/kleinschreibungsempfindlicher String, der den [Ereignistyp](/de/docs/Web/Events) darstellt, auf den gehört werden soll.
- `listener`
  - : Das Objekt, das eine Benachrichtigung (ein Objekt, das die [`Event`](/de/docs/Web/API/Event)-Schnittstelle implementiert) erhält, wenn ein Ereignis des angegebenen Typs auftritt. Dies kann `null`, ein Objekt mit einer `handleEvent()`-Methode oder eine JavaScript-[Funktion](/de/docs/Web/JavaScript/Guide/Functions) sein. Siehe [Der Ereignislistener-Callback](#der_ereignislistener-callback) für Details zum Callback selbst.
- `options` {{optional_inline}}

  - : Ein Objekt, das Merkmale des Ereignislisteners angibt. Die verfügbaren Optionen sind:

    - `capture` {{optional_inline}}
      - : Ein boolescher Wert, der angibt, dass Ereignisse dieses Typs an den registrierten `listener` gesendet werden, bevor sie an ein `EventTarget` darunter im DOM-Baum gesendet werden. Wenn nicht angegeben, ist der Standardwert `false`.
    - `once` {{optional_inline}}
      - : Ein boolescher Wert, der angibt, dass der `listener` höchstens einmal nach dem Hinzufügen aufgerufen werden soll. Wenn `true`, würde der `listener` automatisch entfernt werden, wenn er aufgerufen wird. Wenn nicht angegeben, ist der Standardwert `false`.
    - `passive` {{optional_inline}}

      - : Ein boolescher Wert, der angibt, dass die Funktion, die von `listener` angegeben wird, niemals [`preventDefault()`](/de/docs/Web/API/Event/preventDefault) aufruft. Wenn ein passiver Listener `preventDefault()` aufruft, passiert nichts und es kann eine Konsolenwarnung generiert werden.

        Wenn diese Option nicht angegeben ist, ist der Standardwert `false` - außer in Browsern außer Safari, wo sie für [`wheel`](/de/docs/Web/API/Element/wheel_event), [`mousewheel`](/de/docs/Web/API/Element/mousewheel_event), [`touchstart`](/de/docs/Web/API/Element/touchstart_event) und [`touchmove`](/de/docs/Web/API/Element/touchmove_event)-Ereignisse auf `true` gesetzt ist. Siehe [Verwendung passiver Listener](#verwendung_passiver_listener), um mehr zu erfahren.

    - `signal` {{optional_inline}}
      - : Ein [`AbortSignal`](/de/docs/Web/API/AbortSignal). Der Listener wird entfernt, wenn die [`abort()`](/de/docs/Web/API/AbortController/abort)-Methode des [`AbortController`](/de/docs/Web/API/AbortController), dem das `AbortSignal` gehört, aufgerufen wird. Wenn nicht angegeben, ist kein `AbortSignal` mit dem Listener verbunden.

- `useCapture` {{optional_inline}}

  - : Ein boolescher Wert, der angibt, ob Ereignisse dieses Typs an den registrierten `listener` _vor_ dem Versenden an ein `EventTarget` darunter im DOM-Baum gesendet werden. Ereignisse, die den Baum hinaufblubbern, lösen keinen Listener aus, der zur Verwendung der Erfassung bestimmt ist. Ereignisblasen und Erfassung sind zwei Möglichkeiten der Ereignisweiterleitung, die in einem Element auftreten, das in einem anderen Element verschachtelt ist, wenn beide Elemente einen Handler für dieses Ereignis registriert haben. Die Ereignisweiterleitungsmodus bestimmt die Reihenfolge, in der Elemente das Ereignis erhalten. Siehe [DOM Level 3 Events](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow) und [JavaScript-Ereignisreihenfolge](https://www.quirksmode.org/js/events_order.html#link4) für eine detaillierte Erklärung. Wenn nicht angegeben, ist `useCapture` standardmäßig `false`.

    > [!NOTE]
    > Für Ereignislistener, die am Ereignisziel angebracht sind, befindet sich das Ereignis in der Zielphase, statt in den Erfassungs- und Blasenphasen.
    > Ereignislistener in der _Erfassungsphase_ werden vor Ereignislistenern in der Ziel- und Blasenphase aufgerufen.

- `wantsUntrusted` {{optional_inline}} {{non-standard_inline}}
  - : Ein Firefox (Gecko)-spezifischer Parameter. Wenn `true`, empfängt der Listener synthetische Ereignisse, die von Webinhalten gesendet werden (der Standardwert ist `false` für Browser-{{Glossary("chrome", "chrome")}} und `true` für reguläre Webseiten). Dieser Parameter ist nützlich für Code in Add-Ons sowie den Browser selbst.

### Rückgabewert

Keiner ({{jsxref("undefined")}}).

## Anwendungshinweise

### Der Ereignislistener-Callback

Der Ereignislistener kann entweder als Callback-Funktion oder
als Objekt, dessen `handleEvent()`-Methode als Callback-Funktion dient, angegeben werden.

Die Callback-Funktion selbst hat dieselben Parameter und denselben Rückgabewert wie die `handleEvent()`-Methode; das heißt, der Callback akzeptiert einen einzigen Parameter: ein
Objekt basierend auf [`Event`](/de/docs/Web/API/Event), das das aufgetretene Ereignis beschreibt, und gibt nichts zurück.

Zum Beispiel könnte ein Ereignishandler-Callback, der sowohl
[`fullscreenchange`](/de/docs/Web/API/Element/fullscreenchange_event) als auch
[`fullscreenerror`](/de/docs/Web/API/Element/fullscreenerror_event) verarbeiten kann, so aussehen:

```js
function handleEvent(event) {
  if (event.type === "fullscreenchange") {
    /* handle a full screen toggle */
  } else {
    /* handle a full screen toggle error */
  }
}
```

### Der Wert von "this" im Handler

Es ist oft wünschenswert, auf das Element zu verweisen, auf dem der Ereignishändler ausgelöst wurde,
z. B. bei Verwendung eines generischen Handlers für eine Gruppe ähnlicher Elemente.

Wenn Sie eine Handler-Funktion mithilfe von `addEventListener()` an ein Element binden,
wird der Wert von {{jsxref("Operators/this","this")}} innerhalb des Handlers eine Referenz auf
das Element sein. Es wird derselbe Wert wie die Eigenschaft `currentTarget`
des Ereignisarguments sein, das an den Handler übergeben wird.

```js
my_element.addEventListener("click", function (e) {
  console.log(this.className); // logs the className of my_element
  console.log(e.currentTarget === this); // logs `true`
});
```

Zur Erinnerung: [Pfeilfunktionen haben keinen eigenen `this`-Kontext](/de/docs/Web/JavaScript/Reference/Functions/Arrow_functions#cannot_be_used_as_methods).

```js
my_element.addEventListener("click", (e) => {
  console.log(this.className); // WARNING: `this` is not `my_element`
  console.log(e.currentTarget === this); // logs `false`
});
```

Wenn ein Ereignishandler (z. B. [`onclick`](/de/docs/Web/API/Element/click_event)) in der HTML-Quelle für ein Element angegeben ist, wird der JavaScript-Code im Attributwert effektiv in eine Handler-Funktion eingeschlossen, die den Wert von `this` auf eine Weise bindet, die mit `addEventListener()` konsistent ist; ein Vorkommen von `this` im Code stellt eine Referenz auf das Element dar.

```html
<table id="my_table" onclick="console.log(this.id);">
  <!-- `this` refers to the table; logs 'my_table' -->
  …
</table>
```

Beachten Sie, dass der Wert von `this` innerhalb einer Funktion, die von
dem im Attributwert enthaltenen Code _aufgerufen_ wird, sich gemäß den [Standardregeln](/de/docs/Web/JavaScript/Reference/Operators/this) verhält. Dies wird im folgenden Beispiel gezeigt:

```html
<script>
  function logID() {
    console.log(this.id);
  }
</script>
<table id="my_table" onclick="logID();">
  <!-- when called, `this` will refer to the global object -->
  …
</table>
```

Der Wert von `this` innerhalb von `logID()` ist eine Referenz auf das globale
Objekt [`Window`](/de/docs/Web/API/Window) (oder `undefined` im Fall von [strict mode](/de/docs/Web/JavaScript/Reference/Strict_mode).

#### Festlegen von "this" mit bind()

Mit der Methode {{jsxref("Function.prototype.bind()")}} können Sie einen festen
`this`-Kontext für alle nachfolgenden Aufrufe festlegen — wodurch Probleme umgangen werden, bei denen unklar ist, was `this` sein wird, je nach
dem Kontext, aus dem Ihre Funktion aufgerufen wurde. Beachten Sie jedoch, dass Sie eine
Referenz zum Listener behalten müssen, damit Sie ihn später entfernen können.

Dies ist ein Beispiel mit und ohne `bind()`:

```js
class Something {
  name = "Something Good";
  constructor(element) {
    // bind causes a fixed `this` context to be assigned to `onclick2`
    this.onclick2 = this.onclick2.bind(this);
    element.addEventListener("click", this.onclick1, false);
    element.addEventListener("click", this.onclick2, false); // Trick
  }
  onclick1(event) {
    console.log(this.name); // undefined, as `this` is the element
  }
  onclick2(event) {
    console.log(this.name); // 'Something Good', as `this` is bound to the Something instance
  }
}

const s = new Something(document.body);
```

Eine andere Lösung besteht darin, eine spezielle Funktion namens `handleEvent()` zu verwenden, um
alle Ereignisse zu erfassen:

```js
class Something {
  name = "Something Good";
  constructor(element) {
    // Note that the listeners in this case are `this`, not this.handleEvent
    element.addEventListener("click", this, false);
    element.addEventListener("dblclick", this, false);
  }
  handleEvent(event) {
    console.log(this.name); // 'Something Good', as this is bound to newly created object
    switch (event.type) {
      case "click":
        // some code here…
        break;
      case "dblclick":
        // some code here…
        break;
    }
  }
}

const s = new Something(document.body);
```

Eine weitere Möglichkeit, die Referenz auf `this` zu handhaben, besteht darin, eine Pfeilfunktion zu verwenden, die keinen eigenen `this`-Kontext erstellt.

```js
class SomeClass {
  name = "Something Good";

  register() {
    window.addEventListener("keydown", (e) => {
      this.someMethod(e);
    });
  }

  someMethod(e) {
    console.log(this.name);
    switch (e.code) {
      case "ArrowUp":
        // some code here…
        break;
      case "ArrowDown":
        // some code here…
        break;
    }
  }
}

const myObject = new SomeClass();
myObject.register();
```

### Daten in einen und aus einem Ereignislistener einfügen und extrahieren

Ereignislistener nehmen nur ein Argument an,
ein [`Event`](/de/docs/Web/API/Event) oder eine Unterklasse von `Event`,
das automatisch an den Listener übergeben wird, und der Rückgabewert wird ignoriert.
Daher müssen Sie, um Daten in einen Ereignislistener zu setzen und daraus zu extrahieren, statt die Daten durch Parameter und Rückgabewerte zu übergeben, [closures](/de/docs/Web/JavaScript/Closures) verwenden.

Die Funktionen, die als Ereignislistener übergeben werden, haben Zugang zu allen Variablen, die in den äußeren Bereichen deklariert sind, die die Funktion enthalten.

```js
const myButton = document.getElementById("my-button-id");
let someString = "Data";

myButton.addEventListener("click", () => {
  console.log(someString);
  // 'Data' on first click,
  // 'Data Again' on second click

  someString = "Data Again";
});

console.log(someString); // Expected Value: 'Data' (will never output 'Data Again')
```

Lesen Sie den [Funktionsleitfaden](/de/docs/Web/JavaScript/Guide/Functions#function_scope) für mehr Informationen über Funktionsbereiche.

### Speicherprobleme

```js
const elts = document.getElementsByTagName("*");

// Case 1
for (const elt of elts) {
  elt.addEventListener(
    "click",
    (e) => {
      // Do something
    },
    false,
  );
}

// Case 2
function processEvent(e) {
  // Do something
}

for (const elt of elts) {
  elt.addEventListener("click", processEvent, false);
}
```

Im ersten Fall oben wird mit jeder
Iteration der Schleife eine neue (anonyme) Handler-Funktion erstellt. Im zweiten Fall wird dieselbe vorher deklarierte Funktion als
Ereignishandler verwendet, was zu einem geringeren Speicherverbrauch führt, da nur eine
Handler-Funktion erstellt wird. Außerdem ist es im ersten Fall nicht möglich,
[`removeEventListener()`](/de/docs/Web/API/EventTarget/removeEventListener) aufzurufen, da keine
Referenz auf die anonyme Funktion behalten wird (oder hier nicht auf eine der mehreren
anonymen Funktionen, die die Schleife erstellen könnte). Im zweiten Fall kann
`myElement.removeEventListener("click", processEvent, false)`
ausgeführt werden, weil `processEvent` die Funktionsreferenz ist.

Tatsächlich ist das Problem bezüglich des Speicherverbrauchs nicht
das Fehlen einer Funktionsreferenz, sondern das Fehlen einer _statischen_ Funktionsreferenz.

### Verwendung passiver Listener

Wenn ein Ereignis eine Standardaktion hat — zum Beispiel, ein [`wheel`](/de/docs/Web/API/Element/wheel_event)-Ereignis, das standardmäßig den Container scrollt — kann der Browser in der Regel nicht mit der Ausführung der Standardaktion beginnen, bis der Ereignislistener abgeschlossen ist, da er im Voraus nicht weiß, ob der Ereignislistener die Standardaktion durch Aufruf von [`Event.preventDefault()`](/de/docs/Web/API/Event/preventDefault) abbrechen könnte. Wenn der Ereignislistener zu lange braucht, um auszuführen, kann dies zu einer spürbaren Verzögerung führen, auch bekannt als {{Glossary("jank", "Jank")}}, bevor die Standardaktion ausgeführt werden kann.

Durch das Setzen der `passive`-Option auf `true` erklärt ein Ereignislistener, dass er die Standardaktion nicht abbrechen wird, so dass der Browser die Standardaktion sofort beginnen kann, ohne darauf zu warten, dass der Listener fertig ist. Wenn der Listener dann [`Event.preventDefault()`](/de/docs/Web/API/Event/preventDefault) aufruft, hat dies keine Wirkung.

Die Spezifikation für `addEventListener()` definiert den Standardwert für die `passive`-Option immer als `false`. Moderne Browser haben jedoch den Standardwert der `passive`-Option auf `true` für die [`wheel`](/de/docs/Web/API/Element/wheel_event), [`mousewheel`](/de/docs/Web/API/Element/mousewheel_event), [`touchstart`](/de/docs/Web/API/Element/touchstart_event) und [`touchmove`](/de/docs/Web/API/Element/touchmove_event)-Ereignisse auf Dokumenteebene wie [`Window`](/de/docs/Web/API/Window), [`Document`](/de/docs/Web/API/Document) und [`Document.body`](/de/docs/Web/API/Document/body) geändert, um die Vorteile der Scrollperformance von passiven Listenern im Legacy-Code zu nutzen. Das verhindert, dass der Ereignislistener [das Ereignis abbricht](/de/docs/Web/API/Event/preventDefault), so dass es das Rendering der Seite nicht blockieren kann, während der Benutzer scrollt.

Aus diesem Grund müssen Sie, wenn Sie dieses Verhalten überschreiben und sicherstellen möchten, dass die `passive`-Option `false` ist, die Option explizit auf `false` setzen (anstatt sich auf den Standardwert zu verlassen).

Sie müssen sich keine Sorgen über den Wert von `passive` für das grundlegende [`scroll`](/de/docs/Web/API/Element/scroll_event)-Ereignis machen.
Da es nicht abgebrochen werden kann, können Ereignislistener das Seiten-Rendering nicht blockieren.

Siehe [Verbesserung der Scroll-Performance mit passiven Listenern](#verbesserung_der_scroll-performance_mit_passiven_listenern) für ein Beispiel, das die Wirkung passiver Listener zeigt.

## Beispiele

### Einen einfachen Listener hinzufügen

Dieses Beispiel zeigt, wie `addEventListener()` verwendet wird, um Maus
klicks auf einem Element zu beobachten.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Function to change the content of t2
function modifyText() {
  const t2 = document.getElementById("t2");
  const isNodeThree = t2.firstChild.nodeValue === "three";
  t2.firstChild.nodeValue = isNodeThree ? "two" : "three";
}

// Add event listener to table
const el = document.getElementById("outside");
el.addEventListener("click", modifyText, false);
```

In diesem Code ist `modifyText()` ein Listener für `click`-Ereignisse,
der mit `addEventListener()` registriert wurde. Ein Klick irgendwo in der Tabelle blubbert
zum Handler hoch und führt `modifyText()` aus.

#### Ergebnis

{{EmbedLiveSample('Add_a_simple_listener')}}

### Hinzufügen eines abbrechbaren Listeners

Dieses Beispiel zeigt, wie man `addEventListener()` hinzufügt, das mit einem [`AbortSignal`](/de/docs/Web/API/AbortSignal) abgebrochen werden kann.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Add an abortable event listener to table
const controller = new AbortController();
const el = document.getElementById("outside");
el.addEventListener("click", modifyText, { signal: controller.signal });

// Function to change the content of t2
function modifyText() {
  const t2 = document.getElementById("t2");
  if (t2.firstChild.nodeValue === "three") {
    t2.firstChild.nodeValue = "two";
  } else {
    t2.firstChild.nodeValue = "three";
    controller.abort(); // remove listener after value reaches "three"
  }
}
```

Im obigen Beispiel ändern wir den Code im vorherigen Beispiel so, dass wir, nachdem der Inhalt der zweiten Zeile auf "drei" geändert wurde, `abort()` vom [`AbortController`](/de/docs/Web/API/AbortController) aufrufen, den wir in den Aufruf von `addEventListener()` übergeben haben. Das führt dazu, dass der Wert dauerhaft als "drei" verbleibt, da wir keinen Code mehr haben, der auf ein Klick-Ereignis lauscht.

#### Ergebnis

{{EmbedLiveSample('Add_an_abortable_listener')}}

### Ereignis-Listener mit anonymer Funktion

Hier werfen wir einen Blick darauf, wie eine anonyme Funktion verwendet wird, um Parameter in den
Ereignislistener zu übergeben.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Function to change the content of t2
function modifyText(new_text) {
  const t2 = document.getElementById("t2");
  t2.firstChild.nodeValue = new_text;
}

// Function to add event listener to table
const el = document.getElementById("outside");
el.addEventListener(
  "click",
  function () {
    modifyText("four");
  },
  false,
);
```

Beachten Sie, dass der Listener eine anonyme Funktion ist, die Code umfasst, der wiederum in
der Lage ist, Parameter an die `modifyText()`-Funktion zu senden, die
für die tatsächliche Reaktion auf das Ereignis verantwortlich ist.

#### Ergebnis

{{EmbedLiveSample('Event_listener_with_anonymous_function')}}

### Ereignis-Listener mit einer Pfeilfunktion

Dieses Beispiel zeigt einen Ereignislistener, der mit der Pfeilfunktionsnotation implementiert ist.

#### HTML

```html
<table id="outside">
  <tr>
    <td id="t1">one</td>
  </tr>
  <tr>
    <td id="t2">two</td>
  </tr>
</table>
```

#### JavaScript

```js
// Function to change the content of t2
function modifyText(new_text) {
  const t2 = document.getElementById("t2");
  t2.firstChild.nodeValue = new_text;
}

// Add event listener to table with an arrow function
const el = document.getElementById("outside");
el.addEventListener(
  "click",
  () => {
    modifyText("four");
  },
  false,
);
```

#### Ergebnis

{{EmbedLiveSample('Event_listener_with_an_arrow_function')}}

Bitte beachten Sie, dass, obwohl anonyme und Pfeilfunktionen ähnlich sind, sie unterschiedliche
`this`-Bindungen haben. Während anonyme (und alle traditionellen JavaScript-Funktionen)
ihre eigenen `this`-Bindungen erstellen, übernehmen Pfeilfunktionen die
`this`-Bindung der enthaltenen Funktion.

Das bedeutet, dass die Variablen und Konstanten, die der enthaltenen Funktion zur Verfügung stehen,
auch dem Ereignishandler mit einer Pfeilfunktion zur Verfügung stehen.

### Beispiel zur Verwendung von Optionen

#### HTML

```html
<div class="outer">
  outer, once & none-once
  <div class="middle" target="_blank">
    middle, capture & none-capture
    <a class="inner1" href="https://www.mozilla.org" target="_blank">
      inner1, passive & preventDefault(which is not allowed)
    </a>
    <a class="inner2" href="https://developer.mozilla.org/" target="_blank">
      inner2, none-passive & preventDefault(not open new page)
    </a>
  </div>
</div>
<hr />
<button class="clear-button">Clear logs</button>
<section class="demo-logs"></section>
```

#### CSS

```css
.outer,
.middle,
.inner1,
.inner2 {
  display: block;
  width: 520px;
  padding: 15px;
  margin: 15px;
  text-decoration: none;
}
.outer {
  border: 1px solid red;
  color: red;
}
.middle {
  border: 1px solid green;
  color: green;
  width: 460px;
}
.inner1,
.inner2 {
  border: 1px solid purple;
  color: purple;
  width: 400px;
}
```

```css hidden
.demo-logs {
  width: 530px;
  height: 16rem;
  background-color: #ddd;
  overflow-x: auto;
  padding: 1rem;
}
```

#### JavaScript

```js hidden
const clearBtn = document.querySelector(".clear-button");
const demoLogs = document.querySelector(".demo-logs");

function log(msg) {
  demoLogs.innerText += `${msg}\n`;
}

clearBtn.addEventListener("click", () => {
  demoLogs.innerText = "";
});
```

```js
const outer = document.querySelector(".outer");
const middle = document.querySelector(".middle");
const inner1 = document.querySelector(".inner1");
const inner2 = document.querySelector(".inner2");

const capture = {
  capture: true,
};
const noneCapture = {
  capture: false,
};
const once = {
  once: true,
};
const noneOnce = {
  once: false,
};
const passive = {
  passive: true,
};
const nonePassive = {
  passive: false,
};

outer.addEventListener("click", onceHandler, once);
outer.addEventListener("click", noneOnceHandler, noneOnce);
middle.addEventListener("click", captureHandler, capture);
middle.addEventListener("click", noneCaptureHandler, noneCapture);
inner1.addEventListener("click", passiveHandler, passive);
inner2.addEventListener("click", nonePassiveHandler, nonePassive);

function onceHandler(event) {
  log("outer, once");
}
function noneOnceHandler(event) {
  log("outer, none-once, default\n");
}
function captureHandler(event) {
  //event.stopImmediatePropagation();
  log("middle, capture");
}
function noneCaptureHandler(event) {
  log("middle, none-capture, default");
}
function passiveHandler(event) {
  // Unable to preventDefault inside passive event listener invocation.
  event.preventDefault();
  log("inner1, passive, open new page");
}
function nonePassiveHandler(event) {
  event.preventDefault();
  //event.stopPropagation();
  log("inner2, none-passive, default, not open new page");
}
```

#### Ergebnis

Klicken Sie auf die äußeren, mittleren und inneren Container, um zu sehen, wie die Optionen funktionieren.

{{ EmbedLiveSample('Example_of_options_usage', 600, 630) }}

### Ereignis-Listener mit mehreren Optionen

Sie können mehr als eine der Optionen im `options`-Parameter festlegen. Im folgenden Beispiel setzen wir zwei Optionen:

- `passive`, um zu bestätigen, dass der Handler [`preventDefault()`](/de/docs/Web/API/Event/preventDefault) nicht aufruft
- `once`, um sicherzustellen, dass der Ereignis-Handler nur einmal aufgerufen wird.

#### HTML

```html
<button id="example-button">You have not clicked this button.</button>
<button id="reset-button">Click this button to reset the first button.</button>
```

#### JavaScript

```js
const buttonToBeClicked = document.getElementById("example-button");

const resetButton = document.getElementById("reset-button");

// the text that the button is initialized with
const initialText = buttonToBeClicked.textContent;

// the text that the button contains after being clicked
const clickedText = "You have clicked this button.";

// we hoist the event listener callback function
// to prevent having duplicate listeners attached
function eventListener() {
  buttonToBeClicked.textContent = clickedText;
}

function addListener() {
  buttonToBeClicked.addEventListener("click", eventListener, {
    passive: true,
    once: true,
  });
}

// when the reset button is clicked, the example button is reset,
// and allowed to have its state updated again
resetButton.addEventListener("click", () => {
  buttonToBeClicked.textContent = initialText;
  addListener();
});

addListener();
```

#### Ergebnis

{{EmbedLiveSample('Event_listener_with_multiple_options')}}

### Verbesserung der Scroll-Performance mit passiven Listenern

Das folgende Beispiel zeigt die Wirkung der Einstellung von `passive`. Es enthält eine {{htmlelement("div")}} mit etwas Text und ein Kontrollkästchen.

#### HTML

```html
<div id="container">
  <p>
    But down there it would be dark now, and not the lovely lighted aquarium she
    imagined it to be during the daylight hours, eddying with schools of tiny,
    delicate animals floating and dancing slowly to their own serene currents
    and creating the look of a living painting. That was wrong, in any case. The
    ocean was different from an aquarium, which was an artificial environment.
    The ocean was a world. And a world is not art. Dorothy thought about the
    living things that moved in that world: large, ruthless and hungry. Like us
    up here.
  </p>
</div>

<div>
  <input type="checkbox" id="passive" name="passive" checked />
  <label for="passive">passive</label>
</div>
```

```css hidden
#container {
  width: 150px;
  height: 200px;
  overflow: scroll;
  margin: 2rem 0;
  padding: 0.4rem;
  border: 1px solid black;
}
```

#### JavaScript

Der Code fügt einen Listener zum [`wheel`](/de/docs/Web/API/Element/wheel_event)-Ereignis des Containers hinzu, das standardmäßig den Container scrollt. Der Listener führt eine langwierige Operation aus. Zunächst wird der Listener mit der `passive`-Option hinzugefügt, und jedes Mal, wenn das Kontrollkästchen umgeschaltet wird, wird die `passive`-Option umgeschaltet.

```js
const passive = document.querySelector("#passive");
passive.addEventListener("change", (event) => {
  container.removeEventListener("wheel", wheelHandler);
  container.addEventListener("wheel", wheelHandler, {
    passive: passive.checked,
    once: true,
  });
});

const container = document.querySelector("#container");
container.addEventListener("wheel", wheelHandler, {
  passive: true,
  once: true,
});

function wheelHandler() {
  function isPrime(n) {
    for (let c = 2; c <= Math.sqrt(n); ++c) {
      if (n % c === 0) {
        return false;
      }
    }
    return true;
  }

  const quota = 1000000;
  const primes = [];
  const maximum = 1000000;

  while (primes.length < quota) {
    const candidate = Math.floor(Math.random() * (maximum + 1));
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }

  console.log(primes);
}
```

#### Ergebnis

Der Effekt ist, dass:

- Anfangs ist der Listener passiv, daher ist der Versuch, den Container mit dem Rad zu scrollen, sofort.
- Wenn Sie "passiv" deaktivieren und versuchen, den Container mit dem Rad zu scrollen, gibt es eine merkliche Verzögerung, bevor der Container scrollt, da der Browser auf das Ende des langwierigen Listeners warten muss.

{{EmbedLiveSample("Improving scroll performance using passive listeners", 100, 300)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`EventTarget.removeEventListener()`](/de/docs/Web/API/EventTarget/removeEventListener)
- [Erstellen und Auslösen benutzerdefinierter Ereignisse](/de/docs/Web/Events/Creating_and_triggering_events)
- [Weitere Details zur Verwendung von `this` in Ereignishandlern](https://www.quirksmode.org/js/this.html)
