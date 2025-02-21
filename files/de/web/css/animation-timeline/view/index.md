---
title: view()
slug: Web/CSS/animation-timeline/view
l10n:
  sourceCommit: 891bc513a3349040a16c4896197d6a3a910ca42b
---

{{CSSRef}}{{SeeCompatTable}}

Die **`view()`** [CSS-Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) kann mit {{cssxref("animation-timeline")}} verwendet werden, um ein Subjektelement anzugeben, das eine anonyme Sichtfortschrittszeitleiste zur Animation bereitstellen wird. Die Sichtfortschrittszeitleiste schreitet durch eine Änderung der Sichtbarkeit des Subjektelements innerhalb des nächstgelegenen Vorfahrscrollers voran. Die Sichtbarkeit des Subjekts innerhalb des Scrollers wird verfolgt — standardmäßig befindet sich die Zeitleiste bei 0%, wenn das Subjekt erstmals an einem Rand des Scrollers sichtbar ist, und bei 100%, wenn es den gegenüberliegenden Rand erreicht.

Die Funktionsparameter können die Scrollbalkenachse angeben, entlang derer der Fortschritt der Zeitleiste verfolgt wird, und einen Versatz, der die Position des Kastens anpasst, in dem das Subjekt als sichtbar angesehen wird.

> [!NOTE]
> Wenn die angegebene Achse keinen Scrollbalken enthält, ist die Animationszeitleiste inaktiv (hat keinen Fortschritt).

> [!NOTE]
> Jede Verwendung von `view()` entspricht einer eigenen Instanz von [`ViewTimeline`](/de/docs/Web/API/ViewTimeline) in der [Web Animations API](/de/docs/Web/API/Web_Animations_API).

## Syntax

```css
/* Function with no parameters set */
animation-timeline: view();

/* Values for selecting the axis */
animation-timeline: view(block); /* Default */
animation-timeline: view(inline);
animation-timeline: view(y);
animation-timeline: view(x);

/* Values for the inset */
animation-timeline: view(auto); /* Default */
animation-timeline: view(20%);
animation-timeline: view(200px);
animation-timeline: view(20% 40%);
animation-timeline: view(20% 200px);
animation-timeline: view(100px 200px);
animation-timeline: view(auto 200px);

/* Examples that specify axis and inset */
animation-timeline: view(block auto); /* Default */
animation-timeline: view(inline 20%);
animation-timeline: view(x 200px auto);
```

### Parameter

- axis

  - : Der Scrollbalkenachsenwert kann einer der folgenden sein:

    - `block`
      - : Der Scrollbalken auf der Blockachse des Scrollcontainers, was die Achse in der Richtung senkrecht zum Fluss des Textes innerhalb einer Zeile ist.
        Für horizontale Schreibrichtungen, wie zum Beispiel im Englischen, ist dies dasselbe wie `y`, während es für vertikale Schreibrichtungen dasselbe wie `x` ist. Dies ist der Standardwert.
    - `inline`
      - : Der Scrollbalken auf der Inline-Achse des Scrollcontainers, was die Achse in der Richtung parallel zum Fluss des Textes innerhalb einer Zeile ist.
        Für horizontale Schreibrichtungen ist dies dasselbe wie `x`, während es für vertikale Schreibrichtungen dasselbe wie `y` ist.
    - `y`
      - : Der Scrollbalken auf der vertikalen Achse des Scrollcontainers.
    - `x`
      - : Der Scrollbalken auf der horizontalen Achse des Scrollcontainers.

- inset

  - : Der Versatzwert kann ein oder zwei Werte sein, die entweder `auto` oder ein {{cssxref("length-percentage")}} sein können. Es spezifiziert eine Einwärts- (positiv) oder Auswärts- (negativ) Anpassung des {{Glossary("Scroll_container#scrollport", "Scrollports")}}. Der Versatz wird verwendet, um zu bestimmen, ob das Element sichtbar ist, was die Länge der Animationszeitleiste bestimmt. Mit anderen Worten, die Animation dauert so lange, wie das Element im durch den Versatz angepassten Sichtfeld ist.

    - start
      - : Einwärtsversatz vom Anfang des Scrollports.
    - end
      - : Einwärtsversatz vom Ende des Scrollports.

> [!NOTE]
> Die Scroller- und Versatzwerte können in beliebiger Reihenfolge angegeben werden.

## Formale Syntax

{{CSSSyntax}}

## Beispiele

### Einstellen einer anonymen Sichtfortschrittszeitleiste

Eine anonyme Sichtfortschrittszeitleiste wird auf ein Element mit der Klasse `subject` mit `animation-timeline: view()` gesetzt. Das Ergebnis ist, dass das `subject`-Element animiert wird, wenn es sich durch das Dokument bewegt, während gescrollt wird.

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

  <div class="subject-container">
    <div class="subject animation"></div>
  </div>

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
<div class="overlay top">inset start 50%</div>
<div class="overlay bottom">inset end 10%</div>
```

#### CSS

Das `subject`-Element und die `content`-Elemente sind minimal gestylt und dem Textinhalt werden einige grundlegende Schriftart-Einstellungen gegeben:

```css
.subject {
  width: 300px;
  height: 200px;
  background-color: deeppink;
}

.content {
  width: 75%;
  max-width: 800px;
  margin: 0 auto;
}

p {
  font-size: 1.5rem;
  line-height: 1.8;
}
```

Zur besseren Verständlichkeit wurden zusätzliche Elemente `subject-container`, `top` und `bottom` verwendet. Der `subject-container` zeigt die Grenzen der Animation. Halbtransparente Überlagerungen `top` und `bottom` markieren den versatzversetzten Scrollport.

```css
.subject-container {
  border: 2px dashed black;
  width: 300px;
  margin: 0 auto;
}

.overlay {
  position: fixed;
  width: 100%;
  background-color: #f5deb3aa;
  display: flex;
  font-size: 1.2rem;
  font-weight: bold;
  color: red;
  justify-content: flex-end;
}

.top {
  top: 0;
  height: 244px;
  align-items: end;
}

.bottom {
  top: 432px;
  height: 48px;
}
```

Im folgenden Code wird dem `<div>` mit der Klasse `subject` auch eine Klasse `animation` zugewiesen. Die `grow`-Animation bewirkt, dass das `subject`-Element wächst oder schrumpft. Die `animation-timeline: view(block 55% 10%)` wird gesetzt, um zu erklären, dass sie animiert wird, während sie durch die Sichtfortschrittszeitleiste fortschreitet, die von ihrem scrollenden Vorfahr bereitgestellt wird (in diesem Fall das Wurzelelement des Dokuments).

Beim Herunterscrollen beachten Sie, wie der Versatzwert von `50% 10%` bewirkt, dass die Animation bei 10% vom unteren Rand beginnt und bei 50% vom oberen Rand endet. Während die Animation entlang der Zeitleiste voranschreitet, wächst das `subject`. Umgekehrt, beim Hochscrollen schreitet die Animation in umgekehrter Richtung voran, beginnend bei 50% vom oberen Rand, rückwärts durch die Animation, und endend bei 10% vom unteren Rand. Daher schrumpft das `subject`, während die Animation rückwärts geschieht.

Ein wichtiger Punkt, den es zu beachten gilt, ist, dass die Animation so lange dauert, wie das `subject`-Element im Sichtfeld ist, das eingestellt ist und durch die Versatzwerte `50% 10%` verschoben wird.

```css
.animation {
  animation-timeline: view(block 50% 10%);

  animation-name: grow;
  animation-fill-mode: both;
  animation-duration: 1ms; /* Firefox requires this to apply the animation */
  animation-timing-function: linear;
}

@keyframes grow {
  from {
    transform: scaleX(0);
  }

  to {
    transform: scaleX(1);
  }
}
```

#### Ergebnis

Scrollen Sie, um zu sehen, wie das Subjektelement animiert wird.

{{EmbedLiveSample("Setting an anonymous view progress timeline", "100%", "480px")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [CSS scrollgetriebene Animationen](/de/docs/Web/CSS/CSS_scroll-driven_animations)
- [Verwendung von CSS-Animationen](/de/docs/Web/CSS/CSS_animations/Using_CSS_animations)
- [`animation-timeline`](/de/docs/Web/CSS/animation-timeline)
