---
title: :indeterminate
slug: Web/CSS/:indeterminate
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{CSSRef}}

Die **`:indeterminate`** [CSS](/de/docs/Web/CSS) [Pseudoklasse](/de/docs/Web/CSS/Pseudo-classes) repräsentiert jedes Formularelement, dessen Zustand unbestimmt ist, wie beispielsweise Kontrollkästchen, die mit JavaScript auf einen [`indeterminate`](/de/docs/Web/API/HTMLInputElement/indeterminate)-Zustand gesetzt wurden, Optionsfelder, die Mitglieder einer Gruppe sind, in der alle Optionsfelder nicht ausgewählt sind, und {{HTMLElement("progress")}}-Elemente ohne `value`-Attribut.

```css
/* Selects any <input> whose state is indeterminate */
input:indeterminate {
  background: lime;
}
```

Elemente, die durch diesen Selektor angesprochen werden, sind:

- [`<input type="checkbox">`](/de/docs/Web/HTML/Reference/Elements/input/checkbox) Elemente, deren [`indeterminate`](/de/docs/Web/API/HTMLInputElement/indeterminate)-Eigenschaft auf `true` gesetzt ist
- [`<input type="radio">`](/de/docs/Web/HTML/Reference/Elements/input/radio) Elemente, wenn alle Optionsfelder mit demselben `name`-Wert im Formular nicht ausgewählt sind
- {{HTMLElement("progress")}}-Elemente in einem unbestimmten Zustand

## Syntax

```plain
:indeterminate
```

## Beispiele

### Kontrollkästchen & Optionsfeld

Dieses Beispiel wendet spezielle Stile auf die Labels an, die mit unbestimmten Formularfeldern verbunden sind.

#### HTML

```html
<fieldset>
  <legend>Checkbox</legend>
  <div>
    <input type="checkbox" id="checkbox" />
    <label for="checkbox">This checkbox label starts out lime.</label>
  </div>
</fieldset>

<fieldset>
  <legend>Radio</legend>
  <div>
    <input type="radio" id="radio1" name="radioButton" value="val1" />
    <label for="radio1">First radio label starts out lime.</label>
  </div>
  <div>
    <input type="radio" id="radio2" name="radioButton" value="val2" />
    <label for="radio2">Second radio label also starts out lime.</label>
  </div>
</fieldset>
```

#### CSS

```css
input:indeterminate + label {
  background: lime;
}
```

```css hidden
fieldset {
  padding: 1em 0.75em;
}

fieldset:first-of-type {
  margin-bottom: 1.5rem;
}

fieldset:not(:first-of-type) > div:not(:last-child) {
  margin-bottom: 0.5rem;
}
```

#### JavaScript

```js
const inputs = document.getElementsByTagName("input");

for (let i = 0; i < inputs.length; i++) {
  inputs[i].indeterminate = true;
}
```

#### Ergebnis

{{EmbedLiveSample('Checkbox_radio_button', 'auto', 230)}}

### Fortschrittsbalken

#### HTML

```html
<progress></progress>
```

#### CSS

```css
progress {
  margin: 4px;
}

progress:indeterminate {
  width: 80vw;
  height: 20px;
}
```

#### Ergebnis

{{EmbedLiveSample('Progress_bar', 'auto', 30)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Webformulare — Arbeiten mit Benutzerdaten](/de/docs/Learn_web_development/Extensions/Forms)
- [Styling von Webformularen](/de/docs/Learn_web_development/Extensions/Forms/Styling_web_forms)
- Die [`<input type="checkbox">`](/de/docs/Web/HTML/Reference/Elements/input/checkbox)-Eigenschaft [`indeterminate`](/de/docs/Web/API/HTMLInputElement/indeterminate)
- {{HTMLElement("input")}} und die [`HTMLInputElement`](/de/docs/Web/API/HTMLInputElement)-Schnittstelle, die es implementiert.
- Der {{cssxref(":checked")}} CSS-Selektor ermöglicht es, Kontrollkästchen je nachdem, ob sie ausgewählt sind oder nicht, zu stylen.
