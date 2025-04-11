---
title: KeyboardEvent
slug: Web/API/KeyboardEvent
l10n:
  sourceCommit: f61d0fd1f98f5c6bd8e8db987641e4a6e6155a0b
---

{{APIRef("UI Events")}}

**`KeyboardEvent`**-Objekte beschreiben eine Benutzerinteraktion mit der Tastatur; jedes Ereignis beschreibt eine einzelne Interaktion zwischen dem Benutzer und einer Taste (oder einer Kombination einer Taste mit Modifikatortasten) auf der Tastatur. Der Ereignistyp ([`keydown`](/de/docs/Web/API/Element/keydown_event), [`keypress`](/de/docs/Web/API/Element/keypress_event) oder [`keyup`](/de/docs/Web/API/Element/keyup_event)) identifiziert, welche Art von Tastaturaktivität stattgefunden hat.

> **Note:** `KeyboardEvent`-Ereignisse zeigen nur an, welche Interaktion der Benutzer auf niedriger Ebene mit einer Taste auf der Tastatur hatte, ohne dieser Interaktion eine kontextuelle Bedeutung zu verleihen. Wenn Sie die Texteingabe behandeln müssen, verwenden Sie stattdessen das [`input`](/de/docs/Web/API/Element/input_event)-Ereignis. Tastaturereignisse werden möglicherweise nicht ausgelöst, wenn der Benutzer alternative Mittel zur Texteingabe verwendet, wie z. B. ein Handschrifterkennungssystem auf einem Tablet oder Grafiktablett.

{{InheritanceDiagram}}

## Konstruktor

- [`KeyboardEvent()`](/de/docs/Web/API/KeyboardEvent/KeyboardEvent)
  - : Erstellt ein neues `KeyboardEvent`-Objekt.

## Konstanten

Das `KeyboardEvent`-Interface definiert die folgenden Konstanten.

### Tastaturlokationen

Die folgenden Konstanten identifizieren, von welchem Teil der Tastatur das Tastenereignis ausgeht. Sie werden als `KeyboardEvent.DOM_KEY_LOCATION_STANDARD` usw. aufgerufen.

<table class="standard-table">
  <caption>
    Identifikatoren für Tastaturlokationen
  </caption>
  <thead>
    <tr>
      <th scope="col">Konstante</th>
      <th scope="col">Wert</th>
      <th scope="col">Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>DOM_KEY_LOCATION_STANDARD</code></td>
      <td>0x00</td>
      <td>
        <p>Die durch das Ereignis beschriebene Taste wird nicht als in einem bestimmten Bereich der Tastatur befindlich identifiziert; sie befindet sich nicht auf dem numerischen Tastenfeld (es sei denn, es handelt sich um die NumLock-Taste), und bei Tasten, die auf der linken und rechten Seite der Tastatur doppelt vorhanden sind, ist die Taste aus welchem Grund auch immer keiner bestimmten Position zugeordnet.</p>
        <p>Beispiele umfassen alphanumerische Tasten auf der standardmäßigen PC-Tastatur mit 101 Tasten (US-Layout), die NumLock-Taste und die Leertaste.</p>
      </td>
    </tr>
    <tr>
      <td><code>DOM_KEY_LOCATION_LEFT</code></td>
      <td>0x01</td>
      <td>
        <p>Die Taste befindet sich in diesem Fall auf der linken Seite der Tastatur und kann an mehreren Positionen vorhanden sein.</p>
        <p>Beispiele sind die linke Steuerungstaste, die linke Befehlstaste auf einer Macintosh-Tastatur oder die linke Umschalttaste.</p>
      </td>
    </tr>
    <tr>
      <td><code>DOM_KEY_LOCATION_RIGHT</code></td>
      <td>0x02</td>
      <td>
        <p>Die Taste befindet sich in diesem Fall auf der rechten Seite der Tastatur und kann an mehreren Positionen vorhanden sein.</p>
        <p>Beispiele sind die rechte Umschalttaste und die rechte Alt-Taste (Option auf einer Mac-Tastatur).</p>
      </td>
    </tr>
    <tr>
      <td><code>DOM_KEY_LOCATION_NUMPAD</code></td>
      <td>0x03</td>
      <td>
        <p>Die Taste befindet sich auf dem numerischen Tastenfeld oder ist eine virtuelle Taste, die mit dem numerischen Tastenfeld verbunden ist, wenn es mehrere mögliche Ursprungsorte für die Taste gibt. Die NumLock-Taste fällt nicht in diese Gruppe und wird immer mit dem Standort <code>DOM_KEY_LOCATION_STANDARD</code> codiert.</p>
        <p>Beispiele sind die Ziffern auf dem numerischen Tastenfeld, die Eingabetaste des Tastenfelds und der Dezimalpunkt auf dem Tastenfeld.</p>
      </td>
    </tr>
  </tbody>
</table>

## Instanz-Eigenschaften

_Dieses Interface erbt auch Eigenschaften seiner Eltern, [`UIEvent`](/de/docs/Web/API/UIEvent) und [`Event`](/de/docs/Web/API/Event)._

- [`KeyboardEvent.altKey`](/de/docs/Web/API/KeyboardEvent/altKey) {{ReadOnlyInline}}

  - : Gibt einen booleschen Wert zurück, der `true` ist, wenn die <kbd>Alt</kbd> (<kbd>Option</kbd> oder <kbd>⌥</kbd> auf macOS) Taste aktiv war, als das Tastenereignis generiert wurde.

- [`KeyboardEvent.code`](/de/docs/Web/API/KeyboardEvent/code) {{ReadOnlyInline}}

  - : Gibt einen String mit dem Code-Wert der physischen Taste zurück, die durch das Ereignis dargestellt wird.

    > [!WARNING]
    > Dies ignoriert das Tastaturlayout des Benutzers, sodass, wenn der Benutzer die Taste an der Position "Y" in einem QWERTY-Tastaturlayout drückt (in der Nähe der Mitte der Zeile über der Basiszeile), dies immer "KeyY" zurückgibt, selbst wenn der Benutzer eine QWERTZ-Tastatur hat (was bedeuten würde, dass der Benutzer ein "Z" erwartet und alle anderen Eigenschaften ein "Z" anzeigen würden) oder ein Dvorak-Tastaturlayout (wo der Benutzer ein "F" erwarten würde). Wenn Sie dem Benutzer die korrekten Tastendrücke anzeigen möchten, können Sie [`Keyboard.getLayoutMap()`](/de/docs/Web/API/Keyboard/getLayoutMap) verwenden.

- [`KeyboardEvent.ctrlKey`](/de/docs/Web/API/KeyboardEvent/ctrlKey) {{ReadOnlyInline}}

  - : Gibt einen booleschen Wert zurück, der `true` ist, wenn die <kbd>Strg</kbd>-Taste aktiv war, als das Tastenereignis generiert wurde.

- [`KeyboardEvent.isComposing`](/de/docs/Web/API/KeyboardEvent/isComposing) {{ReadOnlyInline}}
  - : Gibt einen booleschen Wert zurück, der `true` ist, wenn das Ereignis zwischen `compositionstart` und `compositionend` ausgelöst wird.
- [`KeyboardEvent.key`](/de/docs/Web/API/KeyboardEvent/key) {{ReadOnlyInline}}
  - : Gibt einen String zurück, der den Tastenwert der Taste repräsentiert, die durch das Ereignis dargestellt wird.
- [`KeyboardEvent.location`](/de/docs/Web/API/KeyboardEvent/location) {{ReadOnlyInline}}
  - : Gibt eine Nummer zurück, die die Position der Taste auf der Tastatur oder einem anderen Eingabegerät darstellt. Eine Liste der Konstanten, die die Orte identifizieren, wird oben unter [Tastaturlokationen](#tastaturlokationen) angezeigt.
- [`KeyboardEvent.metaKey`](/de/docs/Web/API/KeyboardEvent/metaKey) {{ReadOnlyInline}}

  - : Gibt einen booleschen Wert zurück, der `true` ist, wenn die <kbd>Meta</kbd>-Taste (auf Mac-Tastaturen die <kbd>⌘ Command</kbd>-Taste; auf Windows-Tastaturen die Windows-Taste (<kbd>⊞</kbd>)) aktiv war, als das Tastenereignis generiert wurde.

- [`KeyboardEvent.repeat`](/de/docs/Web/API/KeyboardEvent/repeat) {{ReadOnlyInline}}
  - : Gibt einen booleschen Wert zurück, der `true` ist, wenn die Taste so lange gedrückt gehalten wird, dass sie automatisch wiederholt wird.
- [`KeyboardEvent.shiftKey`](/de/docs/Web/API/KeyboardEvent/shiftKey) {{ReadOnlyInline}}

  - : Gibt einen booleschen Wert zurück, der `true` ist, wenn die <kbd>Umschalt</kbd>-Taste aktiv war, als das Tastenereignis generiert wurde.

### Veraltete Eigenschaften

- [`KeyboardEvent.charCode`](/de/docs/Web/API/KeyboardEvent/charCode) {{Deprecated_inline}} {{ReadOnlyInline}}

  - : Gibt eine Nummer zurück, die die Unicode-Referenznummer der Taste darstellt; diese Eigenschaft wird nur vom `keypress`-Ereignis verwendet. Für Tasten, deren `char`-Eigenschaft mehrere Zeichen enthält, ist dies der Unicode-Wert des ersten Zeichens in dieser Eigenschaft. In Firefox 26 wird dies für druckbare Zeichen zurückgegeben.

- [`KeyboardEvent.keyCode`](/de/docs/Web/API/KeyboardEvent/keyCode) {{deprecated_inline}} {{ReadOnlyInline}}

  - : Gibt eine Nummer zurück, die einen system- und implementationsabhängigen numerischen Code darstellt, der den nicht modifizierten Wert der gedrückten Taste identifiziert.

- [`KeyboardEvent.keyIdentifier`](/de/docs/Web/API/KeyboardEvent/keyIdentifier) {{Non-standard_inline}} {{deprecated_inline}} {{ReadOnlyInline}}
  - : Diese Eigenschaft ist nicht standardisiert und wurde zugunsten von [`KeyboardEvent.key`](/de/docs/Web/API/KeyboardEvent/key) abgelehnt. Es war Teil einer alten Version von DOM Level 3 Events.

## Instanzmethoden

_Dieses Interface erbt auch Methoden seiner Eltern, [`UIEvent`](/de/docs/Web/API/UIEvent) und [`Event`](/de/docs/Web/API/Event)._

- [`KeyboardEvent.getModifierState()`](/de/docs/Web/API/KeyboardEvent/getModifierState)

  - : Gibt einen booleschen Wert zurück, der angibt, ob eine Modifikatortaste wie <kbd>Alt</kbd>, <kbd>Umschalt</kbd>, <kbd>Strg</kbd> oder <kbd>Meta</kbd> gedrückt war, als das Ereignis erstellt wurde.

### Veraltete Methoden

- [`KeyboardEvent.initKeyboardEvent()`](/de/docs/Web/API/KeyboardEvent/initKeyboardEvent) {{deprecated_inline}}
  - : Initialisiert ein `KeyboardEvent`-Objekt. Diese Methode ist jetzt veraltet. Sie sollten stattdessen den [`KeyboardEvent()`](/de/docs/Web/API/KeyboardEvent/KeyboardEvent)-Konstruktor verwenden.

## Ereignisse

Die folgenden Ereignisse basieren auf dem `KeyboardEvent`-Typ. In der Liste unten verlinkt jedes Ereignis auf die Dokumentation für den `Element`-Handler des Ereignisses, der allgemein auf alle Empfänger, einschließlich [`Element`](/de/docs/Web/API/Element), [`Document`](/de/docs/Web/API/Document) und [`Window`](/de/docs/Web/API/Window) zutrifft.

- [`keydown`](/de/docs/Web/API/Element/keydown_event)
  - : Eine Taste wurde gedrückt.
- [`keyup`](/de/docs/Web/API/Element/keyup_event)
  - : Eine Taste wurde losgelassen.

### Veraltete Ereignisse

- [`keypress`](/de/docs/Web/API/Element/keypress_event) {{deprecated_inline}}
  - : Eine Taste, die normalerweise einen Zeichenwert erzeugt, wurde gedrückt. Dieses Ereignis war stark geräteabhängig und ist veraltet. Sie sollten es nicht verwenden.

## Verwendungshinweise

Es gibt drei Arten von Tastaturereignissen: [`keydown`](/de/docs/Web/API/Element/keydown_event), [`keypress`](/de/docs/Web/API/Element/keypress_event) und [`keyup`](/de/docs/Web/API/Element/keyup_event). Für die meisten Tasten sendet Gecko eine Sequenz von Tastenereignissen wie folgt:

1. Wenn die Taste zum ersten Mal gedrückt wird, wird das `keydown`-Ereignis gesendet.
2. Wenn die Taste keine Modifikatortaste ist, wird das `keypress`-Ereignis gesendet.
3. Wenn der Benutzer die Taste loslässt, wird das `keyup`-Ereignis gesendet.

### Sonderfälle

Einige Tasten schalten den Status einer Anzeigelampe um; dazu gehören Tasten wie Caps Lock, Num Lock und Scroll Lock. Unter Windows und Linux lösen diese Tasten nur die Ereignisse `keydown` und `keyup` aus.

> [!NOTE]
> Unter Linux löste Firefox 12 und früher auch das `keypress`-Ereignis für diese Tasten aus.

Jedoch verursacht eine Einschränkung des macOS-Ereignismodells, dass Caps Lock nur das `keydown`-Ereignis ausgelöst wird. Num Lock wurde auf einigen älteren Laptop-Modellen (2007 und älter) unterstützt, aber seitdem unterstützt macOS Num Lock nicht einmal auf externen Tastaturen. Auf älteren MacBooks mit einer Num Lock-Taste erzeugt diese Taste keine Tastenereignisse. Gecko unterstützt die Scroll Lock-Taste, wenn eine externe Tastatur mit einer F14-Taste angeschlossen ist. In bestimmten älteren Versionen von Firefox hat diese Taste ein `keypress`-Ereignis erzeugt; dieses inkonsistente Verhalten war [Firefox Bug 602812](https://bugzil.la/602812).

### Auto-Repeat-Verarbeitung

Wenn eine Taste gedrückt und gehalten wird, beginnt sie, sich automatisch zu wiederholen. Dies führt dazu, dass eine Sequenz von Ereignissen ähnlich der folgenden ausgelöst wird:

1. `keydown`
2. `keypress`
3. `keydown`
4. `keypress`
5. <\<wiederholt sich, bis der Benutzer die Taste loslässt>>
6. `keyup`

Dies ist, was die DOM Level 3-Spezifikation besagt, dass passieren sollte. Es gibt jedoch einige Einschränkungen, wie unten beschrieben.

#### Auto-Repeat in einigen GTK-Umgebungen wie Ubuntu 9.4

In einigen GTK-basierten Umgebungen löst Auto-Repeat automatisch ein natives Key-up-Ereignis während der Auto-Repeat aus, und es gibt keine Möglichkeit für Gecko, den Unterschied zwischen einer wiederholten Serie von Tastendrücken und einer Auto-Repeat zu erkennen. Auf diesen Plattformen wird eine Auto-Repeat-Taste dann die folgende Ereignissequenz generieren:

1. `keydown`
2. `keypress`
3. `keyup`
4. `keydown`
5. `keypress`
6. `keyup`
7. <\<wiederholt sich, bis der Benutzer die Taste loslässt>>
8. `keyup`

In diesen Umgebungen gibt es leider keine Möglichkeit für Webinhalte, den Unterschied zwischen sich automatisch wiederholenden Tasten und Tasten, die einfach wiederholt gedrückt werden, zu erkennen.

## Beispiel

```js
document.addEventListener(
  "keydown",
  (event) => {
    const keyName = event.key;

    if (keyName === "Control") {
      // do not alert when only Control key is pressed.
      return;
    }

    if (event.ctrlKey) {
      // Even though event.key is not 'Control' (e.g., 'a' is pressed),
      // event.ctrlKey may be true if Ctrl key is pressed at the same time.
      alert(`Combination of ctrlKey + ${keyName}`);
    } else {
      alert(`Key pressed ${keyName}`);
    }
  },
  false,
);

document.addEventListener(
  "keyup",
  (event) => {
    const keyName = event.key;

    // As the user releases the Ctrl key, the key is no longer active,
    // so event.ctrlKey is false.
    if (keyName === "Control") {
      alert("Control key was released");
    }
  },
  false,
);
```

## Spezifikationen

{{Specifications}}

Die `KeyboardEvent`-Interface-Spezifikation durchlief zahlreiche Entwurfsfassungen, zunächst unter DOM Events Level 2, wo sie aufgegeben wurde, da kein Konsens erzielt wurde, dann unter DOM Events Level 3. Dies führte zur Implementierung nicht standardisierter Initialisierungsmethoden, der frühen DOM Events Level 2-Version `KeyboardEvent.initKeyEvent()` durch Gecko-Browser und der frühen DOM Events Level 3-Version [`KeyboardEvent.initKeyboardEvent()`](/de/docs/Web/API/KeyboardEvent/initKeyboardEvent) durch andere. Beide wurden durch die moderne Nutzung eines Konstruktors ersetzt: [`KeyboardEvent()`](/de/docs/Web/API/KeyboardEvent/KeyboardEvent).

## Browser-Kompatibilität

{{Compat}}

### Kompatibilitätshinweise

- Ab Firefox 65 wird das `keypress`-Ereignis nicht mehr für [nicht druckbare Tasten](/de/docs/Web/API/KeyboardEvent/keyCode#non-printable_keys_function_keys) ([Firefox Bug 968056](https://bugzil.la/968056)) ausgelöst, mit Ausnahme der <kbd>Eingabetaste</kbd> und der Tastenkombinationen <kbd>Umschalt</kbd> + <kbd>Eingabetaste</kbd> und <kbd>Strg</kbd> + <kbd>Eingabetaste</kbd> (diese wurden aus Gründen der plattformübergreifenden Kompatibilität beibehalten).

## Siehe auch

- [`KeyboardEvent.code`](/de/docs/Web/API/KeyboardEvent/code).
- [`KeyboardEvent.key`](/de/docs/Web/API/KeyboardEvent/key).
- [`KeyboardEvent.getModifierState()`](/de/docs/Web/API/KeyboardEvent/getModifierState)
