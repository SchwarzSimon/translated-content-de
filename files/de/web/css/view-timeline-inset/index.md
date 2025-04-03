---
title: view-timeline-inset
slug: Web/CSS/view-timeline-inset
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{CSSRef}}{{SeeCompatTable}}

Die **`view-timeline-inset`**-Eigenschaft [CSS](/de/docs/Web/CSS) wird verwendet, um einen oder zwei Werte anzugeben, die eine Anpassung der Position des Scrollbereichs (weitere Informationen finden Sie im {{Glossary("Scroll_container", "Scroll container")}}) darstellen, in dem das Subjektelement einer _benannten View-Progress-Zeitachsenanimation_ als sichtbar angesehen wird. Anders ausgedrückt, ermöglicht dies, Start- und/oder End-Inset- (oder Outset-) Werte festzulegen, die die Position der Zeitachse versetzen.

Dies kann mit oder anstelle von {{cssxref("animation-range")}} und deren Langform-Eigenschaften kombiniert werden, mit denen der Anwendungsbereich einer Animation entlang ihrer Zeitachse festgelegt werden kann.
Weitere Details finden Sie unter [CSS-Scroll-gesteuerte Animationen](/de/docs/Web/CSS/CSS_scroll-driven_animations).

## Syntax

```css
/* Single value */
view-timeline-inset: auto;
view-timeline-inset: 200px;
view-timeline-inset: 20%;

/* Two values */
view-timeline-inset: 20% auto;
view-timeline-inset: auto 200px;
view-timeline-inset: 20% 200px;
```

### Werte

Erlaubte Werte für `view-timeline-inset` sind:

- `auto`
  - : Wenn festgelegt, wird das entsprechende {{cssxref("scroll-padding")}} (oder äquivalenter Langformwert) für diese Kante des Scrollbereichs verwendet. Ist dies nicht festgelegt (oder auf `auto` gesetzt), beträgt der Wert in der Regel 0, obwohl einige Benutzeragenten Heuristiken verwenden können, um gegebenenfalls einen anderen Standardwert zu bestimmen.
- {{cssxref("length-percentage")}}
  - : Jeder gültige `<length-percentage>`-Wert wird als Inset/Outset-Wert akzeptiert.
    - Wenn der Wert positiv ist, wird die Position des Start-/Endpunkts der Animation innerhalb des Scrollbereichs um die angegebene Länge oder Prozentsatz verschoben.
    - Wenn der Wert negativ ist, wird die Position des Start-/Endpunkts der Animation außerhalb des Scrollbereichs um die angegebene Länge oder Prozentsatz verschoben, d.h. sie beginnt zu animieren, bevor sie im Scrollbereich erscheint, oder endet, nachdem sie den Scrollbereich verlassen hat.

Wenn zwei Werte angegeben werden, stellt der erste Wert das Start-Inset/Outset auf der relevanten Achse dar (wo die Animation beginnt), und der zweite Wert stellt das End-Inset/Outset dar (wo die Animation endet). Wenn nur ein Wert angegeben wird, werden das Start- und End-Inset/Outset beide auf denselben Wert gesetzt.

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### Erstellen einer benannten View-Progress-Zeitachse mit Inset

Eine View-Progress-Zeitachse namens `--subjectReveal` wird mithilfe der `view-timeline`-Eigenschaft auf einem Subjektelement mit einer `class` von `animation` definiert.
Diese wird dann als Zeitachse für das gleiche Element mit `animation-timeline: --subjectReveal;` festgelegt. Das Ergebnis ist, dass das Subjektelement animiert wird, wenn es nach oben durch das Dokument bewegt wird, während es gescrollt wird.

Eine `view-timeline-inset`-Deklaration wird ebenfalls festgelegt, um die Animation später als erwartet zu beginnen und früher zu beenden.

#### HTML

Das HTML für das Beispiel wird unten gezeigt.

```html
<div class="content">
  <h1>Content</h1>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
    tempor incididunt ut labore et dolore magna aliqua. Risus quis varius quam
    quisque id. Et ligula ullamcorper malesuada proin libero nunc consequat
    interdum varius. Elit ullamcorper dignissim cras tincidunt lobortis feugiat
    vivamus at augue.
  </p>

  <p>
    Dolor sed viverra ipsum nunc aliquet. Sed sed risus pretium quam vulputate
    dignissim. Tortor aliquam nulla facilisi cras. A erat nam at lectus urna
    duis convallis convallis. Nibh ipsum consequat nisl vel pretium lectus.
    Sagittis aliquam malesuada bibendum arcu vitae elementum. Malesuada bibendum
    arcu vitae elementum curabitur vitae nunc sed velit.
  </p>

  <div class="subject animation"></div>

  <p>
    Adipiscing enim eu turpis egestas pretium aenean pharetra magna ac. Arcu
    cursus vitae congue mauris rhoncus aenean vel. Sit amet cursus sit amet
    dictum. Augue neque gravida in fermentum et. Gravida rutrum quisque non
    tellus orci ac auctor augue mauris. Risus quis varius quam quisque id diam
    vel quam elementum. Nibh praesent tristique magna sit amet purus gravida
    quis. Duis ultricies lacus sed turpis tincidunt id aliquet. In egestas erat
    imperdiet sed euismod nisi. Eget egestas purus viverra accumsan in nisl nisi
    scelerisque. Netus et malesuada fames ac.
  </p>
</div>
```

#### CSS

Das `subject`-Element und dessen enthaltenes `content`-Element werden minimal gestylt, und der Textinhalt erhält einige grundlegende Schriftarteinstellungen:

```css
.subject {
  width: 300px;
  height: 200px;
  margin: 0 auto;
  background-color: deeppink;
}

.content {
  width: 75%;
  max-width: 800px;
  margin: 0 auto;
}

p,
h1 {
  font-family: Arial, Helvetica, sans-serif;
}

h1 {
  font-size: 3rem;
}

p {
  font-size: 1.5rem;
  line-height: 1.5;
}
```

Das `<div>` mit der Klasse `subject` erhält auch eine Klasse von `animation` — hier wird `view-timeline` gesetzt, um eine benannte View-Progress-Zeitachse zu definieren. Wir geben ihm auch eine `view-timeline-inset`-Deklaration, um die Animation später als erwartet zu beginnen und früher zu beenden. Es erhält auch einen `animation-timeline`-Namen mit demselben Wert, um zu erklären, dass dies das Element sein wird, das animiert wird, wenn die View-Progress-Zeitachse fortschreitet.

Zuletzt wird eine Animation auf dem Element spezifiziert, die seine Deckkraft und Skalierung animiert, wodurch es beim Aufwärtsbewegen im Scroller verblasst und größer wird.

```css
.animation {
  view-timeline: --subjectReveal block;
  view-timeline-inset: 70% -100px;
  animation-timeline: --subjectReveal;

  animation-name: appear;
  animation-fill-mode: both;
  animation-duration: 1ms; /* Firefox requires this to apply the animation */
}

@keyframes appear {
  from {
    opacity: 0;
    transform: scaleX(0);
  }

  to {
    opacity: 1,
    transform: scaleX(1);
  }
}
```

#### Ergebnis

Scrollen Sie, um das Subjektelement animiert zu sehen.

{{EmbedLiveSample("Creating a named view progress timeline with inset", "100%", "480px")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`animation-timeline`](/de/docs/Web/CSS/animation-timeline)
- {{cssxref("timeline-scope")}}
- [`view-timeline`](/de/docs/Web/CSS/view-timeline), [`view-timeline-axis`](/de/docs/Web/CSS/view-timeline-axis), [`view-timeline-name`](/de/docs/Web/CSS/view-timeline-name)
- [CSS-Scroll-gesteuerte Animationen](/de/docs/Web/CSS/CSS_scroll-driven_animations)
