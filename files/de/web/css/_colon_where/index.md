---
title: :where()
slug: Web/CSS/:where
l10n:
  sourceCommit: 215e1b1590b1210152e3570627933c0303171e11
---

{{CSSRef}}

Die **`:where()`** [CSS](/de/docs/Web/CSS) [Pseudoklasse](/de/docs/Web/CSS/Pseudo-classes)-Funktion nimmt eine Selektorliste als Argument und wählt jedes Element aus, das durch einen der Selektoren in dieser Liste ausgewählt werden kann.

Der Unterschied zwischen `:where()` und {{CSSxRef(":is", ":is()")}} besteht darin, dass `:where()` immer eine [Spezifität](/de/docs/Web/CSS/CSS_cascade/Specificity) von 0 hat, während `:is()` die Spezifität des spezifischsten Selektors in seinen Argumenten übernimmt.

{{InteractiveExample("CSS Demo: :where", "tabbed-shorter")}}

```css interactive-example
ol {
  list-style-type: upper-alpha;
  color: darkblue;
}

/* Not applied to ol, because of lower specificity */
:where(ol, ul, menu:unsupported) :where(ol, ul) {
  color: green;
}

:where(ol, ul) :where(ol, ul) ol {
  list-style-type: lower-greek;
  color: chocolate;
}
```

```html interactive-example
<ol>
  <li>Saturn</li>
  <li>
    <ul>
      <li>Mimas</li>
      <li>Enceladus</li>
      <li>
        <ol>
          <li>Voyager</li>
          <li>Cassini</li>
        </ol>
      </li>
      <li>Tethys</li>
    </ul>
  </li>
  <li>Uranus</li>
  <li>
    <ol>
      <li>Titania</li>
      <li>Oberon</li>
    </ol>
  </li>
</ol>
```

## Syntax

Die `:where()`-Pseudoklasse erfordert eine [Selektorliste](/de/docs/Web/CSS/CSS_selectors/Selector_structure#selector_list), eine kommagetrennte Liste von einem oder mehreren Selektoren, als Argument. Die Liste darf kein [Pseudoelement](/de/docs/Web/CSS/Pseudo-elements) enthalten, aber alle anderen einfachen, zusammengesetzten und komplexen Selektoren sind erlaubt.

```css-nolint
:where(<complex-selector-list>) {
  /* ... */
}
```

### Nachsichtiges Selektor-Parsing

Die Spezifikation definiert `:is()` und `:where()` als akzeptierend für eine [nachsichtig Selektorliste](https://drafts.csswg.org/selectors-4/#typedef-forgiving-selector-list).

In CSS wird bei der Verwendung einer Selektorliste, wenn einer der Selektoren ungültig ist, die gesamte Liste als ungültig angesehen. Bei der Verwendung von `:is()` oder `:where()` wird statt der gesamten Liste von Selektoren, wenn man einen nicht parsen kann, der falsche oder nicht unterstützte Selektor ignoriert und die anderen verwendet.

```css
:where(:valid, :unsupported) {
  /* … */
}
```

Wird auch korrekt geparst und `:valid` zugeordnet, selbst in Browsern, die `:unsupported` nicht unterstützen, wohingegen:

```css
:valid,
:unsupported {
  /* … */
}
```

In Browsern ignoriert wird, die `:unsupported` nicht unterstützen, selbst wenn sie `:valid` unterstützen.

## Beispiele

### Vergleich von :where() und :is()

Dieses Beispiel zeigt, wie `:where()` funktioniert, und veranschaulicht auch den Unterschied zwischen `:where()` und `:is()`.

Betrachten Sie folgendes HTML:

```html
<article>
  <h2>:is()-styled links</h2>
  <section class="is-styling">
    <p>
      Here is my main content. This
      <a href="https://mozilla.org">contains a link</a>.
    </p>
  </section>

  <aside class="is-styling">
    <p>
      Here is my aside content. This
      <a href="https://developer.mozilla.org">also contains a link</a>.
    </p>
  </aside>

  <footer class="is-styling">
    <p>
      This is my footer, also containing
      <a href="https://github.com/mdn">a link</a>.
    </p>
  </footer>
</article>

<article>
  <h2>:where()-styled links</h2>
  <section class="where-styling">
    <p>
      Here is my main content. This
      <a href="https://mozilla.org">contains a link</a>.
    </p>
  </section>

  <aside class="where-styling">
    <p>
      Here is my aside content. This
      <a href="https://developer.mozilla.org">also contains a link</a>.
    </p>
  </aside>

  <footer class="where-styling">
    <p>
      This is my footer, also containing
      <a href="https://github.com/mdn">a link</a>.
    </p>
  </footer>
</article>
```

In diesem etwas konstruierten Beispiel haben wir zwei Artikel, die jeweils einen Abschnitt, eine Randnotiz und ein Footer enthalten. Sie unterscheiden sich durch die Klassen, die verwendet werden, um die Kindelemente zu kennzeichnen.

Um die Auswahl der Links zu gruppieren und dabei die `is-styling`- und `where-styling`-Stile zu unterscheiden, könnten wir `:is()` oder `:where()` auf folgende Weise verwenden:

```css
html {
  font-family: sans-serif;
  font-size: 150%;
}

:is(section.is-styling, aside.is-styling, footer.is-styling) a {
  color: red;
}

:where(section.where-styling, aside.where-styling, footer.where-styling) a {
  color: orange;
}
```

Aber was ist, wenn wir später die Farbe der Links in den Footern mit einem zusammengesetzten Selektor aus niederspezifischen Typselektoren überschreiben möchten?

```css
footer a {
  color: blue;
}
```

Dies wird bei den roten Links nicht funktionieren, da die Selektoren innerhalb von `:is()` zur Spezifität des gesamten Selektors beitragen, und Klassenselektoren eine höhere Spezifität als Elementselektoren haben.

Jedoch haben Selektoren innerhalb von `:where()` die Spezifität 0, sodass der orangene Footer-Link von unserem typbasierten zusammengesetzten Selektor überschrieben wird.

> [!NOTE]
> Sie können dieses Beispiel auch auf GitHub finden; siehe [is-where](https://mdn.github.io/css-examples/is-where/).

{{EmbedLiveSample('Examples', '100%', 600)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{CSSxRef(":is", ":is()")}}
- [Selektorliste](/de/docs/Web/CSS/Selector_list)
- [Webkomponenten](/de/docs/Web/API/Web_components)
