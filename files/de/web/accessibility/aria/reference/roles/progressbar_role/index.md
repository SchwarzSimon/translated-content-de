---
title: "ARIA: Progressbar-Rolle"
slug: Web/Accessibility/ARIA/Reference/Roles/progressbar_role
l10n:
  sourceCommit: ec98716dfe71c78db3f82ee3b1b9e7f68997fa19
---

Die `progressbar`-Rolle definiert ein Element, das den Fortschrittsstatus für Aufgaben anzeigt, die längere Zeit in Anspruch nehmen.

## Beschreibung

Das `progressbar`-Bereichs-Widget zeigt an, dass eine Anforderung eingegangen ist und die Anwendung Fortschritte bei der Ausführung der angeforderten Aktion macht.

Autoren **können** `aria-valuemin` und `aria-valuemax` festlegen, um die minimalen und maximalen Werte des Fortschrittsindikators anzuzeigen. Andernfalls folgen ihre impliziten Werte den gleichen Regeln wie HTMLs [`<input type="range">`](/de/docs/Web/HTML/Element/input/range):

- Wenn [`aria-valuemin`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuemin) fehlt oder keine Zahl ist, wird es standardmäßig auf `0` (null) gesetzt.
- Wenn [`aria-valuemax`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuemax) fehlt oder keine Zahl ist, wird es standardmäßig auf `100` gesetzt.
- Die Eigenschaften `aria-valuemin` und `aria-valuemax` müssen nur für die `progressbar`-Rolle festgelegt werden, wenn das Minimum der Fortschrittsanzeige nicht `0` oder der Höchstwert nicht `100` ist.
- Der schreibgeschützte Wert [`aria-valuenow`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuenow) sollte bereitgestellt und aktualisiert werden, es sei denn, der Wert ist `indeterminate` (unbestimmt); in diesem Fall sollte das Attribut nicht enthalten sein. Wenn festgelegt, stellen Sie sicher, dass der `aria-valuenow`-Wert zwischen den minimalen und maximalen Werten liegt.

Wenn die `progressbar`-Rolle auf ein HTML {{HTMLElement('progress')}}-Element angewendet wird, kann der zugängliche Name von dem zugehörigen {{HTMLElement('label')}} stammen. Andernfalls verwenden Sie [`aria-labelledby`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby), wenn ein sichtbares Label vorhanden ist, oder [`aria-label`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-label), wenn kein sichtbares Label vorhanden ist.

### Alle Nachkommen sind präsentational

Es gibt einige Arten von Benutzeroberflächenkomponenten, die, wenn sie in einer Plattform-Zugänglichkeits-API dargestellt werden, nur Text enthalten können. Zugänglichkeits-APIs haben keine Möglichkeit, semantische Elemente in einem `progressbar` zu repräsentieren. Um mit dieser Einschränkung umzugehen, wenden Browser automatisch die Rolle [`presentation`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/presentation_role) auf alle Nachkommenelemente eines jeden `progressbar`-Elements an, da es sich um eine Rolle handelt, die semantische Kinder nicht unterstützt.

Zum Beispiel, betrachten Sie das folgende `progressbar`-Element, das eine Überschrift enthält.

```html
<div role="progressbar"><h3>Title of my progressbar</h3></div>
```

Da Nachkommen von `progressbar` präsentational sind, ist der folgende Code gleichwertig:

```html
<div role="progressbar">
  <h3 role="presentation">Title of my progressbar</h3>
</div>
```

Aus Sicht eines Benutzers von unterstützenden Technologien existiert die Überschrift nicht, da die vorherigen Code-Snippets im {{Glossary("Accessibility_tree", "Zugänglichkeitsbaum")}} gleichwertig mit dem folgenden sind:

```html
<div role="progressbar">Title of my progressbar</div>
```

### Zugeordnete WAI-ARIA-Rollen, Zustände und Eigenschaften

- [`aria-valuenow`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuenow)
  - : Nur vorhanden und erforderlich, wenn der Wert nicht unbestimmt ist. Setzen Sie einen Dezimalwert zwischen `0` oder `aria-valuemin`, wenn vorhanden, und `aria-valuemax`, der den aktuellen Wert der Fortschrittsanzeige angibt.
- [`aria-valuetext`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuetext)
  - : Unterstützende Technologien präsentieren den Wert von `aria-valuenow` oft als Prozentsatz. Wenn dies nicht korrekt wäre, verwenden Sie diese Eigenschaft, um den Wert der Fortschrittsanzeige verständlich zu machen.
- [`aria-valuemin`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuemin)
  - : Setzen Sie einen Dezimalwert darstellend den minimalen Wert, der kleiner ist als `aria-valuemax`. Wenn nicht vorhanden, ist der Standardwert `0`.
- [`aria-valuemax`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-valuemax)
  - : Setzen Sie einen Dezimalwert darstellend den maximalen Wert, der größer ist als `aria-valuemin`. Wenn nicht vorhanden, ist der Standardwert `100`.
- [`aria-label`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-label) oder [`aria-labelledby`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby)
  - : Definiert den Zeichenfolgenwert oder identifiziert das Element (oder die Elemente), die das progressbar-Element mit einem zugänglichen Namen kennzeichnen. Ein zugänglicher Name ist erforderlich.

Es wird empfohlen, native {{HTMLElement("progress")}}- oder [`<input type="range">`](/de/docs/Web/HTML/Element/input/range)-Elemente anstelle der `progressbar`-Rolle zu verwenden. Benutzeragenten bieten ein stilisiertes Widget für das {{HTMLElement("progress")}}-Element basierend auf dem aktuellen `value`, wie es sich auf `0`, den minimalen Wert, und den `max`-Wert bezieht. Bei der Verwendung nicht-semantischer Elemente müssen alle Funktionen des nativen semantischen Elements mit ARIA-Attributen, JavaScript und CSS neu erstellt werden.

## Beispiele

Im folgenden Beispiel verwendet die Fortschrittsanzeige die Standardwerte 0 und 100 für `aria-valuemin` und `aria-valuemax`:

```html
<div>
  <span id="loadinglabel">Loading:</span>
  <span role="progressbar" aria-labelledby="loadinglabel" aria-valuenow="23">
    <svg width="100" height="10">
      <rect height="10" width="100" stroke="black" fill="black" />
      <rect height="10" width="23" fill="white" />
    </svg>
  </span>
</div>
```

Unter Verwendung semantischen HTMLs könnte dies wie folgt geschrieben werden:

```html
<label for="loadinglabel">Loading:</label>
<progress id="loadinglabel" max="100" value="23"></progress>
```

## Beste Praktiken

Wenn die Fortschrittsanzeige den Ladefortschritt eines bestimmten Bereichs einer Seite beschreibt, fügen Sie das Attribut [`aria-describedby`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-describedby) hinzu, um den Status der Fortschrittsanzeige zu referenzieren, und setzen Sie das Attribut [`aria-busy`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-busy) auf `true` für den Bereich, bis das Laden abgeschlossen ist.

### Bevorzugen Sie HTML

Es wird empfohlen, native {{HTMLElement("progress")}}- oder [`<input type="range">`](/de/docs/Web/HTML/Element/input/range)-Elemente anstelle der `progressbar`-Rolle zu verwenden.

## Spezifikationen

{{Specifications}}

## Siehe auch

- HTML-{{HTMLElement('progress')}}-Element
- Andere Bereichs-Widgets umfassen:
  - [`meter`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/meter_role)
  - [`scrollbar`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/scrollbar_role)
  - [`separator`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/separator_role) (wenn fokussierbar)
  - [`slider`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/slider_role)
  - [`spinbutton`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/spinbutton_role)
