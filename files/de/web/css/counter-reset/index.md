---
title: counter-reset
slug: Web/CSS/counter-reset
l10n:
  sourceCommit: 429d45679a29f386af0ddfcf2a64498843c3e1e5
---

{{CSSRef}}

Die **`counter-reset`** [CSS](/de/docs/Web/CSS) Eigenschaft erstellt benannte [CSS-Zähler](/de/docs/Web/CSS/CSS_counter_styles/Using_CSS_counters) und initialisiert diese auf einen bestimmten Wert. Sie unterstützt das Erstellen von Zählern, die von eins bis zur Anzahl der Elemente hochzählen, sowie von solchen, die von der Anzahl der Elemente bis eins herunterzählen.

{{InteractiveExample("CSS Demo: counter-reset")}}

```css interactive-example-choice
counter-reset: none;
```

```css interactive-example-choice
counter-reset: chapter-count 0;
```

```css interactive-example-choice
counter-reset: chapter-count;
```

```css interactive-example-choice
counter-reset: chapter-count 5;
```

```css interactive-example-choice
counter-reset: chapter-count -5;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="transition-all" id="chapters">
    <h1>Alice's Adventures in Wonderland</h1>
    <h2>Down the Rabbit-Hole</h2>
    <h2 id="example-element">The Pool of Tears</h2>
    <h2>A Caucus-Race and a Long Tale</h2>
    <h2>The Rabbit Sends in a Little Bill</h2>
  </div>
</section>
```

```css interactive-example
#default-example {
  text-align: left;
  counter-reset: chapter-count;
}

#example-element {
  background-color: lightblue;
  color: black;
}

h2 {
  counter-increment: chapter-count;
  font-size: 1em;
}

h2::before {
  content: "Chapter " counters(chapter-count, ".") ": ";
}
```

## Syntax

```css
/* Create a counter with initial default value 0 */
counter-reset: my-counter;

/* Create a counter and initialize as "-3" */
counter-reset: my-counter -3;

/* Create a reversed counter with initial default value */
counter-reset: reversed(my-counter);

/* Create a reversed counter and initialize as "-1" */
counter-reset: reversed(my-counter) -1;

/* Create reversed and regular counters at the same time */
counter-reset: reversed(pages) 10 items 1 reversed(sections) 4;

/* Remove all counter-reset declarations in less specific rules */
counter-reset: none;

/* Global values */
counter-reset: inherit;
counter-reset: initial;
counter-reset: revert;
counter-reset: revert-layer;
counter-reset: unset;
```

### Werte

Die `counter-reset` Eigenschaft akzeptiert eine Liste von einem oder mehreren durch Leerzeichen getrennten Zählernamen oder das Schlüsselwort `none`. Für Zählernamen verwenden reguläre Zähler das Format `<counter-name>`, und umgekehrte Zähler verwenden `reversed(<counter-name>)`, wobei `<counter-name>` ein {{cssxref("custom-ident", "&lt;custom-ident&gt;")}} oder `list-item` für den eingebauten {{HTMLElement("ol")}} Zähler ist. Optional kann jedem Zählername ein `<integer>` folgen, um seinen Anfangswert festzulegen.

- {{cssxref("custom-ident", "&lt;custom-ident&gt;")}}
  - : Gibt den Zählernamen an, der mit dem Format {{cssxref("custom-ident", "&lt;custom-ident&gt;")}} erstellt und initialisiert wird. Die funktionale Notation `reversed()` kann verwendet werden, um den Zähler als umgekehrt zu markieren.
- {{cssxref("&lt;integer&gt;")}}
  - : Der Anfangswert, der auf den neu erstellten Zähler gesetzt wird. Standardmäßig `0`, falls nicht angegeben.
- `none`
  - : Gibt an, dass keine Zählerinitialisierung stattfinden soll. Dieser Wert ist nützlich, um `counter-reset` Werte in weniger spezifischen Regeln zu überschreiben.

## Beschreibung

Die `counter-reset` Eigenschaft kann sowohl reguläre als auch, in unterstützenden Browsern, umgekehrte Zähler erstellen. Sie können mehrere reguläre und umgekehrte Zähler erstellen, jeweils getrennt durch ein Leerzeichen. Zähler können ein eigenständiger Name oder ein durch Leerzeichen getrenntes Name-Wert-Paar sein.

> [!WARNING]
> Es gibt [einen Unterschied zwischen den Eigenschaften `counter-reset` und `counter-set`](/de/docs/Web/CSS/CSS_counter_styles/Using_CSS_counters#difference_between_counter-set_and_counter-reset). Nachdem ein Zähler mit `counter-reset` erstellt wurde, können Sie seinen Wert mit der Eigenschaft {{cssxref("counter-set")}} anpassen. Dies ist kontraintuitiv, denn trotz seines Namens wird die `counter-reset` Eigenschaft zum Erstellen und Initialisieren von Zählern verwendet, während die `counter-set` Eigenschaft zum Zurücksetzen des Wertes eines vorhandenen Zählers genutzt wird.

Das Setzen von `counter-increment: none` auf einen Selektor mit höherer Spezifität überschreibt die Erstellung des benannten Zählers auf Selektoren mit geringerer Spezifität.

### Standardanfangswerte

Die standardmäßigen Anfangswerte sowohl der regulären als auch der umgekehrten Zähler erleichtern die Implementierung der beiden häufigsten Nummerierungsmuster: Hochzählen von eins zur Anzahl der Elemente und Herunterzählen von der Anzahl der Elemente bis eins. Durch Einbeziehen eines Zählwerts für einen benannten Zähler kann Ihr Zähler ab einem ganzzahligen Wert hoch- oder herunterzählen.

Reguläre Zähler haben einen Standardwert von `0`, wenn kein Reset-Wert angegeben wird. Standardmäßig erhöhen sich reguläre Zähler um eins, was mit der {{cssxref("counter-increment")}} Eigenschaft angepasst werden kann.

```css
h1 {
  /* Create the counters "chapter" and "page" and set to initial default value.
     Create the counter "section" and set to "4". */
  counter-reset: chapter section 4 page;
}
```

### Umgekehrte Zähler

Wenn umgekehrte Zähler ohne Wert erstellt werden, startet der Zähler mit dem Wert, der der Anzahl der Elemente im Satz entspricht, und zählt so herunter, dass das letzte Element im Satz `1` ist. Standardmäßig verringern sich umgekehrte Zähler um eins; dies kann ebenfalls mit der `counter-increment` Eigenschaft geändert werden.

```css
h1 {
  /* Create reversed counters "chapter" and "section".
      Set "chapter" as the number of elements and "section" as "10".
      Create the counter "pages" with the initial default value. */
  counter-reset: reversed(chapter) reversed(section) 10 pages;
}
```

### Eingebauter `list-item` Zähler

Geordnete Listen ({{HTMLElement("ol")}}) haben eingebaute `list-item` Zähler, die ihre Nummerierung steuern. Diese Zähler erhöhen oder verringern sich automatisch um eins mit jedem Listenelement. Die `counter-reset` Eigenschaft kann verwendet werden, um die `list-item` Zähler zurückzusetzen. Wie bei anderen Zählern können Sie den Standardinkrementwert für `list-item` Zähler durch die {{cssxref("counter-increment")}} Eigenschaft überschreiben.

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### Überschreiben des `list-item` Zählers

In diesem Beispiel wird die `counter-reset` Eigenschaft verwendet, um einen Startwert für einen impliziten `list-item` Zähler festzulegen.

#### HTML

```html
<ol>
  <li>First</li>
  <li>Second</li>
  <li>Third</li>
  <li>Fourth</li>
  <li>Fifth</li>
</ol>
```

#### CSS

Mit `counter-reset` setzen wir den impliziten `list-item` Zähler auf einen anderen Startwert als den Standardwert `1`:

```css
ol {
  counter-reset: list-item 3;
}
```

#### Ergebnis

{{EmbedLiveSample("Overriding the list-item counter", 140, 300)}}

Mit `counter-reset` beginnen wir den impliziten `list-item` Zähler bei `3` für jedes `ol` zu zählen. Dann würde das erste Element mit 4 nummeriert, das zweite mit 5 und so weiter, ähnlich dem Effekt, den man in HTML mit [`<ol start="4">`](/de/docs/Web/HTML/Element/ol#start) erzielte.

### Verwendung eines umgekehrten Zählers

Im folgenden Beispiel haben wir einen umgekehrten Zähler namens 'priority' deklariert. Der Zähler wird verwendet, um fünf Aufgaben zu nummerieren.

```html
<ul class="stack">
  <li>Task A</li>
  <li>Task B</li>
  <li>Task C</li>
  <li>Task D</li>
  <li>Task E</li>
</ul>
```

```css hidden
@supports not (counter-reset: reversed(priority)) {
  .stack {
    display: none;
  }
  body::after {
    content: "Your browser doesn't support the reversed counters yet.";
  }
}
```

```css
li::before {
  content: counter(priority) ". ";
  counter-increment: priority -1;
}

.stack {
  counter-reset: reversed(priority);
  list-style: none;
}
```

{{EmbedLiveSample("Using a reverse counter", 140, 150)}}

In der Ausgabe sind die Elemente in umgekehrter Reihenfolge von 5 bis 1 nummeriert. Beachten Sie, dass wir im Code den Anfangswert des Zählers nicht angegeben haben. Der Browser berechnet den Anfangswert zur Layoutzeit automatisch unter Verwendung des Zählerinkrementwerts.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Verwendung von CSS-Zählern](/de/docs/Web/CSS/CSS_counter_styles/Using_CSS_counters) Leitfaden
- {{cssxref("counter-increment")}} Eigenschaft
- {{cssxref("counter-set")}} Eigenschaft
- {{cssxref("@counter-style")}} Regel
- {{cssxref("counter", "counter()")}} und {{cssxref("counters", "counters()")}} Funktionen
- {{cssxref("content")}} Eigenschaft
- {{cssxref("::marker")}} Pseudo-Klasse
- [CSS-Listen und -Zähler](/de/docs/Web/CSS/CSS_lists) Modul
- [CSS Zählerstile](/de/docs/Web/CSS/CSS_counter_styles) Modul
