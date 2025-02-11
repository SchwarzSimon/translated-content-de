---
title: place-content
slug: Web/CSS/place-content
l10n:
  sourceCommit: f3d3298130d8e22fb89ba123a0648ad3cb7b3655
---

{{CSSRef}}

Die **`place-content`**-[CSS](/de/docs/Web/CSS)-[Kurzschrift-Eigenschaft](/de/docs/Web/CSS/Shorthand_properties) ermöglicht es Ihnen, Inhalte sowohl in Block- als auch in Inline-Richtung gleichzeitig auszurichten (d.h. die Eigenschaften {{CSSxRef("align-content")}} und {{CSSxRef("justify-content")}}) in einem relevanten Layout-System wie [Grid](/de/docs/Web/CSS/CSS_grid_layout) oder [Flexbox](/de/docs/Web/CSS/CSS_flexible_box_layout).

{{EmbedInteractiveExample("pages/css/place-content.html")}}

## Zugehörige Eigenschaften

Diese Eigenschaft ist eine Kurzschreibweise für die folgenden CSS-Eigenschaften:

- [`align-content`](/de/docs/Web/CSS/align-content)
- [`justify-content`](/de/docs/Web/CSS/justify-content)

## Syntax

```css
/* Positional alignment */
/* align-content does not take left and right values */
place-content: center start;
place-content: start center;
place-content: end left;
place-content: flex-start center;
place-content: flex-end center;

/* Baseline alignment */
/* justify-content does not take baseline values */
place-content: baseline center;
place-content: first baseline space-evenly;
place-content: last baseline right;

/* Distributed alignment */
place-content: space-between space-evenly;
place-content: space-around space-evenly;
place-content: space-evenly stretch;
place-content: stretch space-evenly;

/* Global values */
place-content: inherit;
place-content: initial;
place-content: revert;
place-content: revert-layer;
place-content: unset;
```

Der erste Wert ist der Wert der Eigenschaft {{CSSxRef("align-content")}}, der zweite der von {{CSSxRef("justify-content")}}.

> [!NOTE]
> Wenn der zweite Wert nicht vorhanden ist, wird der erste Wert für beide verwendet, vorausgesetzt, er ist ein gültiger Wert für beide. Wenn er für eine der beiden Eigenschaften ungültig ist, wird der gesamte Wert ungültig sein.

### Werte

- `start`
  - : Die Elemente werden eng aneinander an der Startkante des Ausrichtungscontainers in der entsprechenden Achse ausgerichtet.
- `end`
  - : Die Elemente werden eng aneinander an der Endkante des Ausrichtungscontainers in der entsprechenden Achse ausgerichtet.
- `flex-start`
  - : Die Elemente werden eng aneinander an der Kante des Ausrichtungscontainers je nach Hauptanfangs- oder Queranfangsseite des Flex-Containers ausgerichtet.
    Dies gilt nur für Elemente in einem Flex-Layout. Für Elemente, die keine Kinder eines Flex-Containers sind, wird dieser Wert wie `start` behandelt.
- `flex-end`
  - : Die Elemente werden eng aneinander an der Kante des Ausrichtungscontainers je nach Hauptend- oder Querendseite des Flex-Containers ausgerichtet.
    Dies gilt nur für Elemente in einem Flex-Layout. Für Elemente, die keine Kinder eines Flex-Containers sind, wird dieser Wert wie `end` behandelt.
- `center`
  - : Die Elemente werden eng aneinander in der Mitte des Ausrichtungscontainers ausgerichtet.
- `left`
  - : Die Elemente werden eng aneinander an der linken Kante des Ausrichtungscontainers ausgerichtet. Wenn die Achse der Eigenschaft nicht parallel zur Inline-Achse ist, verhält sich dieser Wert wie `start`.
- `right`
  - : Die Elemente werden eng aneinander an der rechten Kante des Ausrichtungscontainers in der entsprechenden Achse ausgerichtet. Wenn die Achse der Eigenschaft nicht parallel zur Inline-Achse ist, verhält sich dieser Wert wie `start`.
- `space-between`
  - : Die Elemente werden gleichmäßig innerhalb des Ausrichtungscontainers verteilt. Der Abstand zwischen jedem Paar benachbarter Elemente ist gleich. Das erste Element liegt bündig mit der Hauptanfangskante, und das letzte Element liegt bündig mit der Hauptendkante.
- `baseline`, `first baseline`, `last baseline`
  - : Gibt die Teilnahme an der ersten oder letzten Basislinienausrichtung an: richtet die Ausrichtungsbasislinie des ersten oder letzten Basisliniensatzes der Box mit der entsprechenden Basislinie im gemeinsamen ersten oder letzten Basisliniensatz aller Boxen in ihrer Basislinien-Sharing-Gruppe aus.
    Die Ersatz-Ausrichtung für `first baseline` ist `start`, die für `last baseline` ist `end`.
- `space-around`
  - : Die Elemente werden gleichmäßig innerhalb des Ausrichtungscontainers verteilt. Der Abstand zwischen jedem Paar benachbarter Elemente ist gleich. Der Leerraum vor dem ersten und nach dem letzten Element ist halb so groß wie der Abstand zwischen jedem Paar benachbarter Elemente.
- `space-evenly`
  - : Die Elemente werden gleichmäßig innerhalb des Ausrichtungscontainers verteilt. Der Abstand zwischen jedem Paar benachbarter Elemente, der Hauptanfangskante und dem ersten Element sowie der Hauptendkante und dem letzten Element ist genau gleich.
- `stretch`
  - : Wenn die kombinierte Größe der Elemente kleiner ist als die Größe des Ausrichtungscontainers, wird die Größe von `auto`-Größe-Elementen gleichmäßig (nicht proportional) erhöht, unter Beachtung der durch {{CSSxRef("max-height")}}/{{CSSxRef("max-width")}} (oder gleichwertige Funktionalität) auferlegten Einschränkungen, sodass die kombinierte Größe den Ausrichtungscontainer genau ausfüllt.
- `safe`
  - : Wird zusammen mit einem Ausrichtungs-Schlüsselwort verwendet. Wenn das gewählte Schlüsselwort dazu führt, dass das Element den Ausrichtungscontainer überläuft und Datenverlust verursacht, wird das Element stattdessen so ausgerichtet, als wäre der Ausrichtungsmodus `start`.
- `unsafe`
  - : Wird zusammen mit einem Ausrichtungs-Schlüsselwort verwendet. Unabhängig von den relativen Größen des Elements und des Ausrichtungscontainers und unabhängig davon, ob ein Überlauf, der Datenverlust verursacht, auftreten könnte, wird der angegebene Ausrichtungswert eingehalten.

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### Platzierung von Inhalten in einem Flex-Container

#### HTML

```html
<div id="container">
  <div class="small">Lorem</div>
  <div class="small">Lorem<br />ipsum</div>
  <div class="large">Lorem</div>
  <div class="large">Lorem<br />ipsum</div>
  <div class="large"></div>
  <div class="large"></div>
</div>
```

```html hidden
<code>writing-mode:</code
><select id="writingMode">
  <option value="horizontal-tb" selected>horizontal-tb</option>
  <option value="vertical-rl">vertical-rl</option>
  <option value="vertical-lr">vertical-lr</option>
  <option value="sideways-rl">sideways-rl</option>
  <option value="sideways-lr">sideways-lr</option></select
><code>;</code><br />

<code>direction:</code
><select id="direction">
  <option value="ltr" selected>ltr</option>
  <option value="rtl">rtl</option></select
><code>;</code><br />

<code>place-content:</code
><select id="alignContentAlignment">
  <option value="normal">normal</option>
  <option value="first baseline">first baseline</option>
  <option value="last baseline">last baseline</option>
  <option value="baseline">baseline</option>
  <option value="space-between">space-between</option>
  <option value="space-around">space-around</option>
  <option value="space-evenly" selected>space-evenly</option>
  <option value="stretch">stretch</option>
  <option value="center">center</option>
  <option value="start">start</option>
  <option value="end">end</option>
  <option value="flex-start">flex-start</option>
  <option value="flex-end">flex-end</option>
  <option value="safe">safe</option>
  <option value="unsafe">unsafe</option>
</select>
<select id="justifyContentAlignment">
  <option value="normal">normal</option>
  <option value="space-between">space-between</option>
  <option value="space-around">space-around</option>
  <option value="space-evenly">space-evenly</option>
  <option value="stretch">stretch</option>
  <option value="center" selected>center</option>
  <option value="start">start</option>
  <option value="end">end</option>
  <option value="flex-start">flex-start</option>
  <option value="flex-end">flex-end</option>
  <option value="left">left</option>
  <option value="right">right</option>
  <option value="safe">safe</option>
  <option value="unsafe">unsafe</option></select
><code>;</code>
```

```js hidden
function update() {
  document.getElementById("container").style.placeContent =
    `${document.getElementById("alignContentAlignment").value} ` +
    `${document.getElementById("justifyContentAlignment").value}`;
}

const alignContentAlignment = document.getElementById("alignContentAlignment");
alignContentAlignment.addEventListener("change", update);

const justifyContentAlignment = document.getElementById(
  "justifyContentAlignment",
);
justifyContentAlignment.addEventListener("change", update);

const writingM = document.getElementById("writingMode");
writingM.addEventListener("change", (evt) => {
  document.getElementById("container").style.writingMode = evt.target.value;
});

const direction = document.getElementById("direction");
direction.addEventListener("change", (evt) => {
  document.getElementById("container").style.direction = evt.target.value;
});
```

#### CSS

```css
#container {
  display: flex;
  height: 240px;
  width: 240px;
  flex-wrap: wrap;
  background-color: #8c8c8c;
  writing-mode: horizontal-tb; /* Can be changed in the live sample */
  direction: ltr; /* Can be changed in the live sample */
  place-content: flex-end center; /* Can be changed in the live sample */
}

div > div {
  border: 2px solid #8c8c8c;
  width: 50px;
  background-color: #a0c8ff;
}

.small {
  font-size: 12px;
  height: 40px;
}

.large {
  font-size: 14px;
  height: 50px;
}
```

#### Ergebnis

{{EmbedLiveSample("Placing_content_in_a_flex_container", "370", "300")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{cssxref("align-content")}}
- {{cssxref("justify-content")}}
- [Grundlagen von Flexbox](/de/docs/Web/CSS/CSS_flexible_box_layout/Basic_concepts_of_flexbox)
- [Ausrichtung von Elementen in einem Flex-Container](/de/docs/Web/CSS/CSS_flexible_box_layout/Aligning_items_in_a_flex_container)
- [Box-Ausrichtung in Grid-Layouts](/de/docs/Web/CSS/CSS_box_alignment/Box_alignment_in_grid_layout)
- [CSS Box-Ausrichtung](/de/docs/Web/CSS/CSS_box_alignment)-Modul
