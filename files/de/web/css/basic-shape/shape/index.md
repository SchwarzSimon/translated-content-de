---
title: shape()
slug: Web/CSS/basic-shape/shape
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

{{CSSRef}}

Die **`shape()`** [CSS-Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) wird verwendet, um eine Form für die Eigenschaften {{cssxref("clip-path")}} und {{cssxref("offset-path")}} zu definieren. Sie kombiniert einen anfänglichen Startpunkt mit einer Reihe von Formbefehlen, die den Pfad der Form definieren. Die `shape()`-Funktion ist ein Mitglied des Datentyps {{cssxref("&lt;basic-shape&gt;")}}.

## Syntax

```css
/* <fill-rule> */
clip-path: shape(nonzero from 0 0, line to 10px 10px);

/* <move-command>, <line-command>, and close */
offset-path: shape(from 10px 10px, move by 10px 5px, line by 20px 40%, close);

/* <hvline-command> */
offset-path: shape(from 10px 10px, hline by 50px, vline to 5rem);

/* <curve-command> */
offset-path: shape(from 10px 10px, curve to 80px 80px via 160px 1px 20% 16px);

/* <smooth-command> */
offset-path: shape(from 10px 10px, smooth to 100px 50pt);

/* <arc-command> */
offset-path: shape(
  from 5% 0.5rem,
  arc to 80px 1pt of 10% ccw large rotate 25deg
);

/* Using a CSS math function */
offset-path: shape(
  from 5px -5%,
  hline to 50px,
  vline by calc(0% + 160px),
  hline by 70.5px,
  close,
  vline by 60px
);

clip-path: shape(
  evenodd from 10px 10px,
  curve to 60px 20% via 40px 0,
  smooth to 90px 0,
  curve by -20px 60% via 10% 40px 20% 20px,
  smooth by -40% -10px via -10px 70px
);
```

### Parameter

- [`<fill-rule>`](/de/docs/Web/SVG/Reference/Attribute/fill-rule) {{optional_inline}}

  - : Gibt an, wie überlappende Bereiche einer Form gefüllt werden sollen. Die möglichen Werte sind:

    - `nonzero`: Ein Punkt wird als innerhalb der Form betrachtet, wenn ein Strahl vom Punkt aus mehr von links nach rechts als von rechts nach links Pfadsegmente kreuzt, was zu einer nicht-null Summe führt. Dies ist der Standardwert, wenn `<fill-rule>` weggelassen wird.

    - `evenodd`: Ein Punkt wird als innerhalb der Form betrachtet, wenn ein Strahl vom Punkt aus eine ungerade Anzahl von Pfadsegmenten kreuzt. Das bedeutet, dass für jedes Mal, dass der Strahl die Form betritt, er nicht die gleiche Anzahl von Malen sie verlässt, was auf eine ungerade Anzahl von Eintritten ohne entsprechende Austritte hinweist.

    > **Warning:** `<fill-rule>` wird in {{cssxref("offset-path")}} nicht unterstützt und die Verwendung macht die Eigenschaft ungültig.

- `from <coordinate-pair>`

  - : Definiert den Startpunkt des ersten `<shape-command>` als ein Paar von Koordinaten, die von der oberen linken Ecke des [Referenzrahmens](/de/docs/Web/CSS/CSS_shapes/Basic_shapes#the_reference_box) gemessen werden. Die Koordinaten werden als durch Leerzeichen getrennte `<x> <y>` {{cssxref("&lt;length-percentage&gt;")}}-Werte angegeben, die den linken Offset bzw. den oberen Offset darstellen. Prozentuale Werte beziehen sich jeweils auf die Breite bzw. Höhe des Referenzrahmens des Elements. Fügen Sie nach diesem Parameter ein Komma hinzu.

- `<shape-command>`

  - : Gibt eine Liste von einem oder mehreren durch Kommas getrennten Befehlen an, die die Form definieren und eine Syntax ähnlich den [SVG-Pfadbefehlen](/de/docs/Web/SVG/Reference/Attribute/d#path_commands) verwenden. Zu den Befehlen gehören `<move-command>`, `<line-command>`, `<hv-line-command>`, `<curve-command>`, `<smooth-command>`, `<arc-command>` und `close`. Der Startpunkt jedes Befehls ist der Endpunkt des vorherigen Befehls, wobei der erste Punkt der Form durch den Parameter [`from <coordinate-pair>`](#from_coordinate-pair) definiert wird.

    Die Syntax der meisten Formbefehle ist ein Schlüsselwort, das eine Anweisung gibt, wie `move` oder `line`, gefolgt vom Schlüsselwort `by` oder `to` und einem Satz von Koordinaten.

    `by`: Gibt an, dass das `<coordinate-pair>` relativ zum Startpunkt des Befehls ist (ein "relativer" Wert).

    `to`: Gibt an, dass das `<coordinate-pair>` relativ zur oberen linken Ecke des Referenzrahmens ist (ein "absoluter" Wert).

    > [!NOTE]
    > Wenn eine Koordinate in einem `<coordinate-pair>` als Prozentsatz angegeben ist, wird der Wert relativ zur jeweiligen Breite oder Höhe des Referenzrahmens berechnet.

    Die folgenden `<shape-command>`s können angegeben werden: `<move-command>`, `<line-command>`, `<hv-line-command>`, `<curve-command>`, `<smooth-command>`, `<arc-command>` und `close`.

    `<move-command>`: Angegeben als `move [by | to] <coordinate-pair>`. Dieser Befehl fügt der Liste der Formbefehle einen [MoveTo-Befehl](/de/docs/Web/SVG/Reference/Attribute/d#moveto_path_commands) hinzu. Er zeichnet nichts, sondern gibt die Startposition für den nächsten Befehl an. Das Schlüsselwort `by` oder `to` gibt an, ob der Punkt `<coordinate-pair>` relativ oder absolut ist. Wenn das `<move-command>` dem `close`-Befehl folgt, identifiziert es den Startpunkt der nächsten Form oder Unterpfad.

    `<line-command>`: Angegeben als `line [by | to] <coordinate-pair>`. Dieser Befehl fügt der Liste der Formbefehle einen [LineTo-Befehl](/de/docs/Web/SVG/Reference/Attribute/d#lineto_path_commands) hinzu. Er zeichnet eine gerade Linie vom Startpunkt des Befehls zu seinem Endpunkt. Das Schlüsselwort `by` oder `to` gibt an, ob der durch `<coordinate-pair>` angegebene Endpunkt relativ oder absolut ist.

    `<hv-line-command>`: Angegeben als `[hline | vline] [by | to] <length-percentage>`. Dieser Befehl fügt der Liste der Formbefehle einen horizontalen (`hline`) oder vertikalen (`vline`) [LineTo-Befehl](/de/docs/Web/SVG/Reference/Attribute/d#lineto_path_commands) hinzu. Mit `hline` wird eine horizontale Linie vom Startpunkt des Befehls `to` oder `by` der durch `<length-percentage>` definierten `x`-Position gezogen. Mit `vline` wird eine vertikale Linie vom Startpunkt des Befehls `to` oder `by` der durch `<length-percentage>` definierten `y`-Position gezogen. Das Schlüsselwort `by` oder `to` bestimmt den relativen oder absoluten Endpunkt. Dieser Befehl ist äquivalent zu `<line-command>` mit einem durch den Einzelwert `<length-percentage>` festgelegten Koordinatenwert und dem anderen Koordinatenwert, der von seinem Startbefehl unverändert bleibt.

    `<curve-command>`: Angegeben als `curve [by | to] <coordinate-pair> via <coordinate-pair> [<coordinate-pair>]`. Dieser Befehl fügt der Liste der Formbefehle einen [Bézier-Kurvenbefehl](/de/docs/Web/SVG/Reference/Attribute/d#cubic_bézier_curve) hinzu. Das Schlüsselwort `by` oder `to` bestimmt, ob der Endpunkt der Kurve, der durch das erste `<coordinate-pair>` angegeben wird, relativ oder absolut ist. Das Schlüsselwort `via` gibt die Kontrollpunkte der Bézier-Kurve an.

    - Wenn nur ein einzelnes `<coordinate-pair>` angegeben wird, zeichnet der Befehl eine [quadratische Bézier-Kurve](/de/docs/Web/SVG/Reference/Attribute/d#quadratic_bézier_curve), die durch drei Punkte definiert wird (den Startpunkt, den Kontrollpunkt und den Endpunkt).
    - Wenn zwei `<coordinate-pair>`-Werte angegeben werden, zeichnet der Befehl eine kubische Bézier-Kurve, die durch vier Punkte definiert wird (den Startpunkt, zwei Kontrollpunkte und den Endpunkt).

    `<smooth-command>`: Angegeben als `smooth [by | to] <coordinate-pair> [via <coordinate-pair>]`. Dieser Befehl fügt der Liste der Formbefehle einen glatten [Bézier-Kurvenbefehl](/de/docs/Web/SVG/Reference/Attribute/d#cubic_bézier_curve) hinzu. Das Schlüsselwort `by` oder `to` bestimmt, ob der Endpunkt der Kurve, der durch das erste `<coordinate-pair>` angegeben wird, relativ oder absolut ist.

    - Wenn `via <coordinate-pair>` weggelassen wird, zeichnet der Befehl eine glatte quadratische Bézier-Kurve, die den vorherigen Kontrollpunkt und den aktuellen Endpunkt verwendet, um die Kurve zu definieren.
    - Wenn das optionale Schlüsselwort `via` enthalten ist, gibt es die Kontrollpunkte der Kurve über `<coordinate-pair>` an und zeichnet eine glatte kubische Bézier-Kurve, die durch den vorherigen Kontrollpunkt, den aktuellen Kontrollpunkt und den aktuellen Endpunkt definiert wird.

    Glatte Kurven sorgen für einen kontinuierlichen Übergang aus der Form, während quadratische Kurven dies nicht tun. Glatte quadratische Kurven gewährleisten einen nahtlosen Übergang mit einem einzelnen Kontrollpunkt, während glatte kubische Kurven einen verfeinerten Übergang mit zwei Kontrollpunkten bieten.

    `<arc-command>`: Angegeben als `arc [by | to] <coordinate-pair> of <length-percentage> [<length-percentage>] [<arc-sweep> | <arc-size> | rotate <angle>]`. Dieser Befehl fügt der Liste der Formbefehle einen [elliptischen Bogenkurvenbefehl](/de/docs/Web/SVG/Reference/Attribute/d#elliptical_arc_curve) hinzu. Er zeichnet einen elliptischen Bogen zwischen einem Startpunkt und einem Endpunkt. Das Schlüsselwort `by` oder `to` bestimmt, ob der Endpunkt der Kurve, der durch das erste `<coordinate-pair>` angegeben wird, relativ oder absolut ist.

    Der elliptische Bogenkurvenbefehl definiert zwei mögliche Ellipsen, die sowohl den Start- als auch den Endpunkt schneiden können, und jede kann im Uhrzeigersinn oder gegen den Uhrzeigersinn verfolgt werden, was zu vier möglichen Bögen je nach Bogenrichtung, -größe und Winkel führt. Das Schlüsselwort `of` gibt die Größe der Ellipse an, aus der der Bogen genommen wird: der erste `<length-percentage>` gibt den horizontalen Radius der Ellipse an und der zweite `<length-percentage>` gibt den vertikalen Radius an.

    Geben Sie die folgenden Parameter an, um den zu verwendenden der vier möglichen Bögen auszuwählen:

    - `<arc-sweep>`: Gibt an, ob der gewünschte Bogen der ist, der die Ellipse im Uhrzeigersinn (`cw`) oder gegen den Uhrzeigersinn (`ccw`) durchläuft. Wenn weggelassen, ist der Standardwert `ccw`.
    - `<arc-size>`: Gibt an, ob der gewünschte Bogen der größere (`large`) oder kleinere (`small`) der beiden Bögen ist. Wenn weggelassen, ist der Standardwert `small`.
    - `<angle>`: Gibt den Winkel in Grad an, um den die Ellipse relativ zur x-Achse gedreht wird. Ein positiver Winkel dreht die Ellipse im Uhrzeigersinn, ein negativer Winkel gegen den Uhrzeigersinn. Wenn weggelassen, ist der Standardwert `0deg`.

    Besondere Situationen werden wie folgt behandelt:

    - Wenn nur ein `<length-percentage>` angegeben wird, wird derselbe Wert sowohl für den horizontalen als auch für den vertikalen Radius verwendet, was effektiv einen Kreis ergibt. In diesem Fall haben `<arc-size>` und `<angle>` keine Auswirkungen.
    - Wenn entweder der horizontale oder der vertikale Radius null ist, entspricht der Befehl einem `<line-command>` zum Endpunkt.
    - Wenn entweder der horizontale oder vertikale Radius negativ ist, wird sein absoluter Wert verwendet.
    - Wenn die horizontalen und vertikalen Radien keine Ellipse beschreiben, die groß genug ist, um sowohl den Start- als auch den Endpunkt (nach der Drehung um den angegebenen `<angle>`) zu schneiden, werden die Radien gleichmäßig skaliert, bis die Ellipse gerade groß genug ist, um beide Punkte zu schneiden.
    - Wenn die Start- und Endpunkte des Bogens genau auf gegenüberliegenden Seiten der Ellipse liegen, gibt es nur eine mögliche Ellipse und zwei mögliche Bögen. In diesem Fall spezifiziert `<arc-sweep>` den zu wählenden Bogen, und `<arc-size>` hat keine Auswirkungen.

    `close`: Fügt der Liste der Formbefehle einen [ClosePath-Befehl](/de/docs/Web/SVG/Reference/Attribute/d#closepath) hinzu und zeichnet eine gerade Linie von der aktuellen Position (Endpunkt des letzten Befehls) zum ersten Punkt im Pfad, der im `from <coordinate-pair>`-Parameter definiert ist. Um die Form zu schließen, ohne eine Linie zu zeichnen, fügen Sie vor dem Schließen-Befehl ein `<move-command>` mit den ursprünglichen Koordinaten hinzu. Wenn der `close`-Befehl unmittelbar von einem `<move-command>` gefolgt wird, legt er den Startpunkt der nächsten Form oder des nächsten Unterpfads fest.

## Beschreibung

Die `shape()`-Funktion ermöglicht Ihnen die Definition komplexer Formen. Sie ist in mehreren Punkten der {{cssxref("basic-shape/path","path()")}}-Formfunktion ähnlich:

- Der `<fill-rule>`-Parameter in der `shape()`-Funktion funktioniert genau wie derselbe Parameter in der `path()`-Funktion.
- Die `shape()`-Funktion erfordert die Angabe von einem oder mehreren `<shape-command>`-Befehlen, wobei jeder Befehl einen zugrunde liegenden [Pfadbefehl](/de/docs/Web/SVG/Reference/Attribute/d#path_commands) verwendet, wie [MoveTo](/de/docs/Web/SVG/Reference/Attribute/d#moveto_path_commands), [LineTo](/de/docs/Web/SVG/Reference/Attribute/d#lineto_path_commands), und [ClosePath](/de/docs/Web/SVG/Reference/Attribute/d#closepath).

Allerdings bietet `shape()` mehrere Vorteile gegenüber der Verwendung von `path()`:

- `shape()` verwendet die standardmäßige CSS-Syntax, was es einfacher macht, Formen direkt in Ihrem Stylesheet zu erstellen und zu ändern. Im Vergleich dazu verwendet `path()` die [SVG-Pfad](/de/docs/Web/SVG/Reference/Element/path)-Syntax, die für diejenigen weniger intuitiv sein kann, die mit SVG nicht vertraut sind.
- `shape()` unterstützt eine Vielzahl von CSS-Einheiten, einschließlich Prozentsätzen, `rem` und `em`. `path()` hingegen definiert Formen als einen einzigen String und beschränkt die Einheiten auf `px`.
- `shape()` ermöglicht auch die Verwendung von CSS-Mathematikfunktionen, wie {{cssxref("calc")}}, {{cssxref("max")}}, und {{cssxref("abs")}}, was mehr Vielseitigkeit bei der Definition von Formen bietet.

## Formale Syntax

{{csssyntax}}

## Beispiele

### Verwendung von `shape()`, um einen Pfad zu definieren

Dieses Beispiel zeigt, wie die `shape()`-Funktion in der {{cssxref("offset-path")}}-Eigenschaft verwendet werden kann, um die Form des Pfades zu definieren, dem ein Element folgen kann.

Die erste Form, `shape1`, folgt einem kubischen Bézier-Kurvenpfad, der durch den `curve to`-Befehl definiert wird. Der `close`-Befehl zieht eine gerade Linie vom Endpunkt der Kurve zurück zum Anfangspunkt, der im `from`-Befehl definiert ist. Schließlich bewegt sich `shape1` zu ihrer neuen Position bei `0px 150px` und folgt dann einer horizontalen Linie.

Die zweite Form, `shape2`, folgt zunächst einer horizontalen Linie, bewegt sich dann zurück zu ihrem Startpunkt bei `50px 90px`. Danach folgt sie einer vertikalen Linie, bevor sie den Pfad zurück zum Anfangspunkt schließt.

Beide Formen beginnen mit ihren ursprünglichen Farben und wechseln allmählich zu `hotpink` am Ende der `move`-Animation, kehren zu ihrer ursprünglichen Farbe zurück, wenn die Animation neu startet. Dieser zyklische Farbwechsel gibt Ihnen einen visuellen Hinweis auf den Fortschritt und den Neustart der Animation.

```html hidden
<div class="container">
  Using <code>&lt;curve-command&gt;</code>
  <div class="shape shape1">>></div>
</div>

<div class="container">
  Using <code>&lt;move-command&gt;</code> and
  <code>&lt;hvline-command&gt;</code>
  <div class="shape shape2">>></div>
</div>
```

```css hidden
body {
  align-items: center;
  justify-content: center;
  display: flex;
}

.container {
  position: relative;
  display: inline-block;
  width: 250px;
  height: 250px;
  border: 2px dotted green;
  margin: 20px;
}

@supports not (offset-path: shape(from 0 0, move to 0 0)) {
  .container {
    display: none;
  }
  body::after {
    content: "Your browser doesn't support the `shape()` function yet.";
  }
}
```

```css
.shape {
  width: 50px;
  height: 50px;
  background: #2bc4a2;
  position: absolute;
  text-align: center;
  line-height: 50px;
  animation: move 6s infinite linear;
}

.shape1 {
  offset-path: shape(
    from 30% 60px,
    curve to 180px 180px via 90px 190px,
    close,
    move by 0px 150px,
    hline by 40%
  );
}

.shape2 {
  offset-path: shape(
    from 50px 90px,
    hline to 8em,
    move to 50px 90px,
    vline by 20%,
    close
  );
}

@keyframes move {
  0% {
    offset-distance: 0%;
  }
  100% {
    offset-distance: 100%;
    background-color: hotpink;
  }
}
```

#### Ergebnis

{{EmbedLiveSample('Using shape() to define a path', '100%', 300)}}

### Verwendung von `shape()`, um den sichtbaren Teil eines Elements zu definieren

Dieses Beispiel zeigt, wie die `shape()`-Funktion in der {{cssxref("clip-path")}}-Eigenschaft verwendet werden kann, um verschiedene Formen für das Clippinggebiet zu erstellen. Die erste Form (`shape1`) verwendet ein durch gerade Linien definiertes Dreieck. Die zweite Form (`shape2`) enthält Kurven und glatte Übergänge; sie zeigt auch die Verwendung des `<move-command>` nach dem `close`-Befehl, der eine rechteckige Form zum Clippinggebiet hinzufügt.

```html hidden
<div class="container">
  <div class="shape shape1"></div>
</div>

<div class="container">
  <div class="shape shape2"></div>
</div>
```

```css hidden
body {
  align-items: center;
  justify-content: center;
  display: flex;
}

.container {
  position: relative;
  display: inline-block;
  width: 200px;
  height: 200px;
  margin: 20px;
  background-color: lightgray;
}

@supports not (clip-path: shape(from 0 0, move to 0 0)) {
  .container {
    display: none;
  }
  body::after {
    content: "Your browser doesn't support the `shape()` function yet.";
  }
}
```

```css
.shape {
  width: 100%;
  height: 100%;
  background: #2bc4a2;
  position: absolute;
  text-align: center;
  line-height: 50px;
}

/* Triangular clipping region */
.shape1 {
  clip-path: shape(from 0% 0%, line to 100% 0%, line to 50% 100%, close);
}

/* Clipping region with curves and smooth transitions and a box */
.shape2 {
  clip-path: shape(
    from 10px 10px,
    curve to 60px 20% via 40px 0,
    smooth to 90px 0,
    curve by -20px 60% via 10% 40px 20% 20px,
    smooth by -40% -10px via -10px 70px,
    close,
    move to 100px 100px,
    hline by 50px,
    vline by 50px,
    hline by -50px,
    close
  );
}
```

#### Ergebnis

{{EmbedLiveSample('Using shape() to define the visible part of an element', '100%', 300)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{cssxref("clip-path")}}
- {{cssxref("offset-path")}}
- [CSS-Formen](/de/docs/Web/CSS/CSS_shapes) Modul
- [Übersicht über Formen](/de/docs/Web/CSS/CSS_shapes/Overview_of_shapes) Leitfaden
- [Grundformen](/de/docs/Web/CSS/CSS_shapes/Basic_shapes) Leitfaden
