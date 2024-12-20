---
title: <input type="color">
slug: Web/HTML/Element/input/color
l10n:
  sourceCommit: 5b20f5f4265f988f80f513db0e4b35c7e0cd70dc
---

{{HTMLSidebar}}

{{HTMLElement("input")}}-Elemente vom Typ **`color`** bieten ein Benutzeroberflächenelement, das es einem Benutzer ermöglicht, eine Farbe entweder über eine visuelle Farbauswahloberfläche festzulegen oder die Farbe in ein Textfeld im `#rrggbb`-Hexadezimalformat einzugeben.

Es sind nur grundlegende Hexadezimalfarben (ohne Alphakanal) erlaubt, obwohl CSS-Farben mehr Formate bietet, z. B. Farbnamen, funktionale Notationen und ein Hexadezimalformat mit einem Alphakanal.

Die Darstellung des Elements kann sich erheblich von einem Browser und/oder einer Plattform zur anderen unterscheiden – es könnte sich um ein einfaches Texteingabefeld handeln, das automatisch validiert wird, um sicherzustellen, dass die Farbinformationen im richtigen Format eingegeben werden, um einen plattformüblichen Farbwähler oder eine Art benutzerdefiniertes Farbauswahlfenster.

{{EmbedInteractiveExample("pages/tabbed/input-color.html", "tabbed-standard")}}

## Wert

Der [`value`](/de/docs/Web/HTML/Element/input#value) eines {{HTMLElement("input")}}-Elements vom Typ `color` ist immer eine Zeichenkette, die eine siebenstellige Zeichenfolge enthält, die eine RGB-Farbe im Hexadezimalformat angibt. Während Sie die Farbe entweder in Groß- oder Kleinbuchstaben eingeben können, wird sie in Kleinbuchstaben gespeichert. Der Wert liegt niemals in einer anderen Form vor und ist niemals leer.

> [!NOTE]
> Wenn Sie den Wert auf etwas setzen, das keine gültige, vollständig undurchsichtige RGB-Farbe _in Hexadezimalnotation_ ist, wird der Wert auf `#000000` gesetzt. Insbesondere können Sie nicht die standardisierten Farbnamen von CSS oder eine CSS-Funktionssyntax verwenden, um den Wert festzulegen. Dies ist sinnvoll, wenn man bedenkt, dass HTML und CSS separate Sprachen und Spezifikationen sind. Außerdem werden Farben mit einem Alphakanal nicht unterstützt; Wenn Sie eine Farbe in einer neunstelligen Hexadezimalnotation angeben (z. B. `#009900aa`), wird die Farbe ebenfalls auf `#000000` festgelegt.

## Verwendung von Farbeingaben

Eingaben vom Typ `color` sind einfach aufgrund der begrenzten Anzahl von Attributen, die sie unterstützen.

### Bereitstellen einer Standardfarbe

Sie können das obige Beispiel aktualisieren, um einen Standardwert festzulegen, sodass der Farbwähler mit der Standardfarbe vorab gefüllt ist und der Farbwähler (sofern vorhanden) auch auf diese Farbe voreingestellt wird:

```html
<input type="color" value="#ff0000" />
```

{{EmbedLiveSample("Providing_a_default_color", 700, 30)}}

Wenn Sie keinen Wert angeben, lautet der Standardwert `#000000`, was schwarz ist. Der Wert muss in siebenstelliger Hexadezimalnotation vorliegen, was bedeutet, dass das Zeichen „#“ gefolgt von jeweils zwei Ziffern, die Rot, Grün und Blau darstellen, wie folgt: `#rrggbb`. Wenn Sie Farben haben, die in einem anderen Format vorliegen (z. B. CSS-Farbnamen oder CSS-Funktionen wie `rgb()` oder `hsl()`), müssen Sie diese vor der Festlegung des `value` in Hexadezimal umwandeln.

### Verfolgen von Farbänderungen

Wie bei anderen {{HTMLElement("input")}}-Typen gibt es zwei Ereignisse, die verwendet werden können, um Änderungen des Farbwerts zu erkennen: [`input`](/de/docs/Web/API/Element/input_event) und [`change`](/de/docs/Web/API/HTMLElement/change_event). `input` wird jedes Mal beim `<input>`-Element ausgelöst, wenn sich die Farbe ändert. Das `change`-Ereignis wird ausgelöst, wenn der Benutzer den Farbwähler schließt. In beiden Fällen können Sie den neuen Wert des Elements ermitteln, indem Sie seinen [`value`](/de/docs/Web/HTML/Element/input#value) betrachten.

Hier ist ein Beispiel, das Änderungen im Laufe der Zeit beim Farbwert überwacht:

```js
colorPicker.addEventListener("input", updateFirst, false);
colorPicker.addEventListener("change", watchColorPicker, false);

function watchColorPicker(event) {
  document.querySelectorAll("p").forEach((p) => {
    p.style.color = event.target.value;
  });
}
```

### Auswahl des Wertes

Wenn ein Browser keine Farbwähler-Schnittstelle unterstützt, wird als Implementierung von Farbeingaben ein Textfeld verwendet, das den Inhalt automatisch validiert, um sicherzustellen, dass der Wert im richtigen Format vorliegt. In diesem Fall können Sie die Methode [`select()`](/de/docs/Web/API/HTMLInputElement/select) verwenden, um den derzeit im Bearbeitungsfeld befindlichen Text auszuwählen.

Wenn der Browser stattdessen einen Farbwähler verwendet, bewirkt `select()` nichts. Sie sollten sich dieses Verhaltens bewusst sein, damit Ihr Code in beiden Fällen angemessen reagieren kann.

```js
colorPicker.select();
```

## Validierung

Der Wert einer Farbeingabe wird als ungültig betrachtet, wenn der {{Glossary("user_agent", "User-Agent")}} nicht in der Lage ist, die Eingabe des Benutzers in eine siebenstellige Hexadezimalnotation in Kleinbuchstaben zu konvertieren. Wenn dies der Fall ist, wird die {{cssxref(":invalid")}} Pseudo-Klasse auf das Element angewendet.

## Beispiel

Erstellen wir ein Beispiel, das etwas mehr mit der Farbeingabe macht, indem wir die Ereignisse [`change`](/de/docs/Web/API/HTMLElement/change_event) und [`input`](/de/docs/Web/API/Element/input_event) überwachen, um die neue Farbe zu übernehmen und auf jedes {{HTMLElement("p")}}-Element im Dokument anzuwenden.

### HTML

Das HTML ist ziemlich einfach — ein paar Absätze mit beschreibendem Material und ein {{HTMLElement("input")}} vom Typ `color` mit der ID `color-picker`, mit dem wir die Textfarbe der Absätze ändern.

```html
<p>
  An example demonstrating the use of the
  <code>&lt;input type="color"&gt;</code> control.
</p>

<label for="color-picker">Color:</label>
<input type="color" value="#ff0000" id="color-picker" />

<p>
  Watch the paragraph colors change when you adjust the color picker. As you
  make changes in the color picker, the first paragraph's color changes, as a
  preview (this uses the <code>input</code> event). When you close the color
  picker, the <code>change</code> event fires, and we detect that to change
  every paragraph to the selected color.
</p>
```

### JavaScript

Zuerst gibt es ein bisschen Setup. Hier richten wir einige Variablen ein, eine Variable, die die Farbe enthält, die wir beim ersten Laden auf den Farbwähler einstellen, und einen [`load`](/de/docs/Web/API/Window/load_event)-Handler, um die Hauptarbeit zu starten, sobald die Seite vollständig geladen ist.

```js
let colorPicker;
const defaultColor = "#0000ff";

window.addEventListener("load", startup, false);
```

#### Initialisierung

Sobald die Seite geladen ist, wird unser `load`-Ereignis-Handler, `startup()`, aufgerufen:

```js
function startup() {
  colorPicker = document.querySelector("#color-picker");
  colorPicker.value = defaultColor;
  colorPicker.addEventListener("input", updateFirst, false);
  colorPicker.addEventListener("change", updateAll, false);
  colorPicker.select();
}
```

Dies holt einen Verweis auf das Farb-`<input>`-Element in einer Variablen namens `colorPicker` ab und setzt dann den Wert der Farbeingabe auf den Wert in `defaultColor`. Dann wird das [`input`](/de/docs/Web/API/Element/input_event)-Ereignis der Farbeingabe auf unseren `updateFirst()`-Funktionsaufruf eingestellt, und das [`change`](/de/docs/Web/API/HTMLElement/change_event)-Ereignis wird auf den Aufruf von `updateAll()` gesetzt. Diese sind beide unten zu sehen.

Zum Schluss rufen wir [`select()`](/de/docs/Web/API/HTMLInputElement/select) auf, um den Textinhalt der Farbeingabe auszuwählen, falls die Steuerung als Textfeld implementiert ist (dies hat keinen Effekt, wenn stattdessen eine Farbwähler-Schnittstelle zur Verfügung steht).

#### Reaktion auf Farbänderungen

Wir stellen zwei Funktionen bereit, die sich mit Farbänderungen befassen. Die `updateFirst()`-Funktion wird als Reaktion auf das `input`-Ereignis aufgerufen. Sie ändert die Farbe des ersten Absatzes im Dokument, um sie an den neuen Wert der Farbeingabe anzupassen. Da `input`-Ereignisse jedes Mal ausgelöst werden, wenn eine Anpassung am Wert vorgenommen wird (z. B. wenn die Helligkeit der Farbe erhöht wird), passieren diese wiederholt, wenn der Farbwähler verwendet wird.

```js
function updateFirst(event) {
  const p = document.querySelector("p");
  if (p) {
    p.style.color = event.target.value;
  }
}
```

Wenn der Farbwähler geschlossen wird, was darauf hinweist, dass sich der Wert nicht mehr ändern wird (es sei denn, der Benutzer öffnet den Farbwähler erneut), wird ein `change`-Ereignis an das Element gesendet. Wir behandeln dieses Ereignis mit der `updateAll()`-Funktion und verwenden [`Event.target.value`](/de/docs/Web/HTML/Element/input#value), um die endgültig ausgewählte Farbe zu erhalten:

```js
function updateAll(event) {
  document.querySelectorAll("p").forEach((p) => {
    p.style.color = event.target.value;
  });
}
```

Dies setzt die Farbe jedes `{{HTMLElement("p")}}`-Blocks so, dass sein {{cssxref("color")}}-Attribut mit dem aktuellen Wert der Farbeingabe übereinstimmt, auf die mit [`event.target`](/de/docs/Web/API/Event/target) verwiesen wird.

### Ergebnis

Das endgültige Ergebnis sieht wie folgt aus:

{{EmbedLiveSample("Example", 700, 200)}}

## Technische Zusammenfassung

<table class="properties">
  <tbody>
    <tr>
      <td><strong><a href="#Wert">Wert</a></strong></td>
      <td>
        Eine siebenstellige Zeichenfolge, die ein
        {{cssxref("&lt;color&gt;")}} in Kleinbuchstaben-Hexadezimalnotation angibt
      </td>
    </tr>
    <tr>
      <td><strong>Ereignisse</strong></td>
      <td>
        [`change`](/de/docs/Web/API/HTMLElement/change_event) und
        [`input`](/de/docs/Web/API/Element/input_event)
      </td>
    </tr>
    <tr>
      <td><strong>Unterstützte gemeinsame Attribute</strong></td>
      <td>
        <a href="/de/docs/Web/HTML/Element/input#autocomplete"><code>autocomplete</code></a> und
        <a href="/de/docs/Web/HTML/Element/input#list"><code>list</code></a>
      </td>
    </tr>
    <tr>
      <td><strong>IDL-Attribute</strong></td>
      <td><code>list</code> und <code>value</code></td>
    </tr>
    <tr>
      <td><strong>DOM-Schnittstelle</strong></td>
      <td><p>[`HTMLInputElement`](/de/docs/Web/API/HTMLInputElement)</p></td>
    </tr>
    <tr>
      <td><strong>Methoden</strong></td>
      <td>
        [`select()`](/de/docs/Web/API/HTMLInputElement/select)
      </td>
    </tr>
    <tr>
      <td><strong>Implizierte ARIA-Rolle</strong></td>
      <td><a href="https://www.w3.org/TR/html-aria/#dfn-no-corresponding-role">keine entsprechende Rolle</a></td>
    </tr>
  </tbody>
</table>

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
