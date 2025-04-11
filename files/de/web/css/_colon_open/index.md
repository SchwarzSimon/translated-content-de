---
title: :open
slug: Web/CSS/:open
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{CSSRef}}

Die **`:open`** [CSS](/de/docs/Web/CSS) [Pseudoklasse](/de/docs/Web/CSS/Pseudo-classes) repräsentiert ein Element, das offene und geschlossene Zustände hat, nur wenn es sich derzeit im offenen Zustand befindet.

## Syntax

```css
:open {
  /* ... */
}
```

## Beschreibung

Die Pseudoklasse `:open` wählt jedes Element aus, das sich aktuell im offenen Zustand befindet. Dazu gehören folgende Elemente:

- {{htmlelement("details")}} und {{htmlelement("dialog")}} Elemente, die im offenen Zustand sind, das heißt, sie haben das Attribut `open` gesetzt.
- {{htmlelement("input")}} Elemente, die eine Auswahloberfläche anzeigen, sodass der Benutzer einen Wert auswählen kann (zum Beispiel [`<input type="color">`](/de/docs/Web/HTML/Reference/Elements/input/color)), wenn die Auswahloberfläche angezeigt wird.
- {{htmlelement("select")}} Elemente, die eine Dropdown-Auswahl für den Benutzer anzeigen, um einen Wert auszuwählen, wenn die Auswahloberfläche angezeigt wird. Beachten Sie, dass beim Implementieren von [anpassbaren Auswahl-Elementen](/de/docs/Learn_web_development/Extensions/Forms/Customizable_select) die Auswahloberfläche selbst mit dem {{cssxref("::picker()", "::picker(select)")}} Pseudoelement ausgewählt werden kann.

Beachten Sie, dass die offenen und geschlossenen Zustände semantische Zustände sind und nicht notwendigerweise mit der Sichtbarkeit des betreffenden Elements korrelieren. Zum Beispiel ist ein `<details>` Element, das erweitert ist, um seinen Inhalt anzuzeigen, offen und wird durch den `details:open` Selektor ausgewählt, selbst wenn es mit einem {{cssxref("visibility")}} Wert von `hidden` ausgeblendet ist.

[Popover](/de/docs/Web/API/Popover_API) Elemente (das heißt, Elemente mit dem Attribut [`popover`](/de/docs/Web/HTML/Reference/Global_attributes/popover) auf ihnen) haben unterschiedliche semantische Zustände, die Popovers repräsentieren, die angezeigt oder verborgen sind, und die neben offenen und geschlossenen Zuständen koexistieren können. Um ein Popover-Element im angezeigten Zustand anzuvisieren, verwenden Sie die {{cssxref(":popover-open")}} Pseudoklasse.

## Beispiele

### Grundlegende Verwendung von `:open`

Dieses Beispiel demonstriert einige der HTML-Elemente, die einen offenen Zustand haben.

#### CSS

```css
details:open > summary {
  background-color: pink;
}

:is(select, input):open {
  background-color: pink;
}
```

```css hidden
@supports not selector(:open) {
  body::before {
    content: "Your browser doesn't support :open selector.";
    background-color: wheat;
    display: block;
    width: 100%;
    text-align: center;
  }

  body > * {
    display: none;
  }
}
```

#### HTML

```html
<details>
  <summary>Details</summary>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. In pulvinar dapibus
  lacus, sit amet finibus lectus mollis eu. Nullam quis orci dictum, porta lacus
  et, cursus nunc. Aenean pulvinar imperdiet neque fermentum facilisis. Nulla
  facilisi. Curabitur vitae sapien ut nunc pulvinar semper vitae vitae nisi.
</details>
<hr />

<label for="pet-select">Choose a pet:</label>
<select id="pet-select">
  <option value="dog">Dog</option>
  <option value="cat">Cat</option>
  <option value="hamster">Hamster</option>
</select>
<hr />

<label for="start">Start date:</label>
<input type="date" id="start" />
```

#### Ergebnis

{{EmbedLiveSample("Basic `:open` usage", 300, 200)}}

### Benutzerdefiniertes `<select>` Styling mit `:open`

In diesem Beispiel geben wir einem simplen {{htmlelement("select")}} Element ein individuelles Styling. Die `:open` Pseudoklasse wird verwendet, um eine Styling-Verbesserung für ihren offenen Zustand anzuwenden — wenn das Dropdown-Menü angezeigt wird.

#### HTML

An unserem Fruchtauswahl-Element ist nichts Besonderes.

```html
<label>
  Choose your favorite fruit:
  <select name="fruit">
    <option>apple</option>
    <option>banana</option>
    <option>boysenberry</option>
    <option>cranberry</option>
    <option>fig</option>
    <option>grapefruit</option>
    <option>lemon</option>
    <option>orange</option>
    <option>papaya</option>
    <option>pomegranate</option>
    <option>tomato</option>
  </select>
</label>
```

> [!NOTE]
> Wir verwenden kein mehrzeiliges `<select>` (das heißt, eines mit dem Attribut [`multiple`](/de/docs/Web/HTML/Reference/Attributes/multiple) gesetzt) — diese neigen dazu, als eine scrollbare Liste anstelle eines Dropdown-Menüs dargestellt zu werden, daher haben sie keinen offenen Zustand.

#### CSS

Im CSS setzen wir einen {{cssxref("appearance")}} Wert von `none` auf unser `<select>` Element, um das standardmäßige OS-Styling von der Auswahlliste zu entfernen, und bieten einige grundlegende eigene Stile. Besonders bemerkenswert ist, dass wir ein {{Glossary("SVG", "SVG")}} Hintergrundbild eines Pfeils nach unten auf der rechten Seite setzen — Benutzer erkennen `<select>` Elemente häufig am Pfeil nach unten, daher ist es eine gute Idee, ihn zu inkludieren.

Wir setzen dann etwas {{cssxref("padding")}} auf das umgebende {{htmlelement("label")}} Element, sowie einen transparenten Rand, um das Layout konsistent zu halten, wenn wir später einen farbigen Rand hinzufügen.

```css
select {
  appearance: none;
  width: 100%;
  display: block;
  font-family: inherit;
  font-size: 100%;
  padding: 5px;
  border: 1px solid black;
  background-color: white;
  background: url("data:image/svg+xml,%3Csvg width='20' height='20' viewbox='0 0 20 20' xmlns='http://www.w3.org/2000/svg'%3E%3Cpolygon points='5,5 15,5 10,15'/%3E%3C/svg%3E")
    no-repeat right 3px center / 1em 1em;
}

label {
  font-family: sans-serif;
  max-width: 20em;
  display: block;
  padding: 20px;
  border: 2px solid transparent;
}
```

Wenn das `<select>` geöffnet ist, verwenden wir die `:open` Pseudoklasse, um eine andere Hintergrundfarbe zu setzen und das Hintergrundbild in einen Pfeil nach oben zu ändern. Wir setzen auch eine andere Hintergrundfarbe und einen Rand auf das umschließende `<label>` Element unter Verwendung einer Kombination der `:open` und {{cssxref(":has()")}} Pseudoklassen, um einen übergeordneten Selektor zu erstellen. Wir sagen buchstäblich "wähle das `<label>`, aber nur wenn sein Nachkomme `<select>` geöffnet ist."

```css
select:open {
  background-color: #f8f2dc;
  background-image: url("data:image/svg+xml,%3Csvg width='20' height='20' viewbox='0 0 20 20' xmlns='http://www.w3.org/2000/svg'%3E%3Cpolygon points='5,15 10,5 15,15'/%3E%3C/svg%3E");
}

label:has(select:open) {
  background-color: #81adc8;
  border-color: #cd4631;
}
```

#### Ergebnis

Das Ergebnis ist wie folgt. Versuchen Sie, die `<select>` Dropdown-Liste zu öffnen, um den Effekt auf das Styling zu sehen:

{{ EmbedLiveSample("Custom `<select>` styling with `:open`", "100%", "100") }}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{htmlelement("details")}}, {{htmlelement("dialog")}}, {{htmlelement("select")}}, und {{htmlelement("input")}} Elemente
- {{cssxref(":popover-open")}} Pseudoklasse
- {{Cssxref(":modal")}}
