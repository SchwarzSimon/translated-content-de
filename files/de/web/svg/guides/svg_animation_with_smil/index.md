---
title: SVG-Animation mit SMIL
slug: Web/SVG/Guides/SVG_animation_with_SMIL
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

[Synchronisiertes Multimedia-Integrationssprache](https://www.w3.org/TR/REC-smil/) (SMIL) ist eine XML-basierte Sprache zur Erstellung interaktiver Multimedia-Präsentationen. Autoren können die SMIL-Syntax in anderen XML-basierten Sprachen verwenden, um das Timing und Layout von Elementen für Animationen zu definieren. SMIL ermöglicht Ihnen:

- die numerischen Attribute eines Elements zu animieren ([x](/de/docs/Web/SVG/Reference/Attribute/x), [y](/de/docs/Web/SVG/Reference/Attribute/y), usw.)
- [transform](/de/docs/Web/SVG/Reference/Attribute/transform)-Attribute zu animieren ([translation](/de/docs/Web/SVG/Reference/Attribute/transform#translate), [rotate](/de/docs/Web/SVG/Reference/Attribute/transform#rotate), usw.)
- [color](/de/docs/Web/SVG/Reference/Attribute/color)-Attribute zu animieren
- einem Bewegungs-[path](/de/docs/Web/SVG/Reference/Element/path) zu folgen

Die folgenden Abschnitte zeigen, wie man SMIL in [SVG](/de/docs/Web/SVG) für diese vier Anwendungsfälle einsetzt.

## Attribute eines Elements animieren

Das folgende Beispiel animiert das [`cx`-Attribut](/de/docs/Web/SVG/Reference/Attribute/cx) eines Kreises. Dazu fügen wir ein {{ SVGElement("animate") }}-Element innerhalb des {{ SVGElement("circle") }}-Elements hinzu. Die wichtigen Attribute für {{ SVGElement("animate") }} sind:

- `attributeName`
  - : Der Name des Attributs, das animiert werden soll.
- `from`
  - : Der Anfangswert des Attributs.
- `to`
  - : Der Endwert.
- `dur`
  - : Die Dauer der Animation (z. B. schreiben Sie '5s' für 5 Sekunden).

Wenn Sie mehr Attribute innerhalb desselben Elements animieren möchten, können Sie weitere {{ SVGElement("animate") }}-Elemente hinzufügen.

```html
<svg width="300" height="100">
  <title>Attribute Animation with SMIL</title>
  <rect x="0" y="0" width="300" height="100" stroke="black" stroke-width="1" />
  <circle cx="0" cy="50" r="15" fill="blue" stroke="black" stroke-width="1">
    <animate
      attributeName="cx"
      from="0"
      to="500"
      dur="5s"
      repeatCount="indefinite" />
  </circle>
</svg>
```

{{ EmbedLiveSample('Animating_attributes_of_an_element', '100%', 120) }}

## Transform-Attribute animieren

Das {{ SVGElement("animateTransform") }}-Element erlaubt es Ihnen, [transform](/de/docs/Web/SVG/Reference/Attribute/transform)-Attribute zu animieren. Dieses Element ist notwendig, da wir kein einzelnes Attribut wie [x](/de/docs/Web/SVG/Reference/Attribute/x) animieren, welches eine Zahl ist. Rotationsattribute sehen so aus: `rotation(theta, x, y)`, wobei `theta` der Winkel in Grad ist und `x` und `y` absolute Positionen sind. Im unteren Beispiel animieren wir das Rotationszentrum und den Winkel.

```html
<svg width="300" height="100">
  <title>SVG SMIL Animate with transform</title>
  <rect x="0" y="0" width="300" height="100" stroke="black" stroke-width="1" />
  <rect
    x="0"
    y="50"
    width="15"
    height="34"
    fill="blue"
    stroke="black"
    stroke-width="1">
    <animateTransform
      attributeName="transform"
      begin="0s"
      dur="20s"
      type="rotate"
      from="0 60 60"
      to="360 100 60"
      repeatCount="indefinite" />
  </rect>
</svg>
```

{{ EmbedLiveSample('Animating_the_transform_attributes', '100%', 120) }}

## Animation entlang eines Pfades

Das {{ SVGElement("animateMotion") }}-Element ermöglicht es Ihnen, die Position und Rotation eines Elements entsprechend einem Pfad zu animieren. Der Pfad wird genauso definiert wie im {{ SVGElement("path") }}. Sie können das Attribut einstellen, um festzulegen, ob das Objekt der Tangente des Pfades folgend rotiert.

### Beispiel 1: Lineare Bewegung

In diesem Beispiel prallt ein blauer Kreis zwischen den linken und rechten Kanten eines schwarzen Kastens immer wieder in einer Schleife. Die Animation wird hier durch das {{ SVGElement("animateMotion") }}-Element gehandhabt. In diesem Fall legen wir einen Pfad fest, der aus einem **MoveTo**-Befehl besteht, um den Startpunkt für die Animation zu definieren, dann der **Horizontal-line**-Befehl, um den Kreis um 300 Pixel nach rechts zu verschieben, gefolgt vom **Z-Befehl**, der den Pfad schließt und eine Schleife zurück zum Anfang etabliert. Durch Festlegen des Wertes des **repeatCount**-Attributs auf `indefinite` geben wir an, dass die Animation für immer in Schleife laufen soll, solange das SVG-Bild existiert.

```html
<svg xmlns="http://www.w3.org/2000/svg" width="300" height="100">
  <title>SVG SMIL Animate with Path</title>
  <rect x="0" y="0" width="300" height="100" stroke="black" stroke-width="1" />
  <circle cx="0" cy="50" r="15" fill="blue" stroke="black" stroke-width="1">
    <animateMotion path="M 0 0 H 300 Z" dur="3s" repeatCount="indefinite" />
  </circle>
</svg>
```

{{ EmbedLiveSample('Example_1_Linear_motion', '100%', 120) }}

[Siehe Live-Beispiel](https://mdn.dev/archives/media/samples/svg/svganimdemo1.html)

### Beispiel 2: Gebogene Bewegung

Das gleiche Beispiel wie zuvor, nur mit einem gebogenen Pfad und folgend der Richtung des Pfades.

```html
<svg width="300" height="100">
  <title>SVG SMIL Animate with Path</title>
  <rect x="0" y="0" width="300" height="100" stroke="black" stroke-width="1" />
  <rect
    x="0"
    y="0"
    width="20"
    height="20"
    fill="blue"
    stroke="black"
    stroke-width="1">
    <animateMotion
      path="M 250,80 H 50 Q 30,80 30,50 Q 30,20 50,20 H 250 Q 280,20,280,50 Q 280,80,250,80Z"
      dur="3s"
      repeatCount="indefinite"
      rotate="auto" />
  </rect>
</svg>
```

{{ EmbedLiveSample('Example_2_Curved_motion', '100%', 120) }}

## Siehe auch

- [SVG](/de/docs/Web/SVG)
- [SVG Animation Spezifikation](https://www.w3.org/TR/SVG/animate.html)
- [SMIL Spezifikation](https://www.w3.org/TR/REC-smil/)
