---
title: result
slug: Web/SVG/Reference/Attribute/result
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

Das **`result`**-Attribut definiert den zugewiesenen Namen für dieses Filter-Primitive. Wenn angegeben, können Grafiken, die aus der Verarbeitung dieses Filter-Primitives resultieren, durch ein {{SVGAttr("in")}}-Attribut in einem nachfolgenden Filter-Primitive innerhalb desselben {{SVGElement("filter")}}-Elements referenziert werden. Wenn kein Wert angegeben ist, wird die Ausgabe nur zur Wiederverwendung als implizite Eingabe in das nächste Filter-Primitive zur Verfügung stehen, sofern dieses keine Wertangabe für sein `in`-Attribut bereitstellt.

Dieses Attribut kann mit den folgenden SVG-Elementen verwendet werden:

- {{SVGElement("feBlend")}}
- {{SVGElement("feColorMatrix")}}
- {{SVGElement("feComponentTransfer")}}
- {{SVGElement("feComposite")}}
- {{SVGElement("feConvolveMatrix")}}
- {{SVGElement("feDiffuseLighting")}}
- {{SVGElement("feDisplacementMap")}}
- {{SVGElement("feDropShadow")}}
- {{SVGElement("feFlood")}}
- {{SVGElement("feGaussianBlur")}}
- {{SVGElement("feImage")}}
- {{SVGElement("feMerge")}}
- {{SVGElement("feMorphology")}}
- {{SVGElement("feOffset")}}
- {{SVGElement("feSpecularLighting")}}
- {{SVGElement("feTile")}}
- {{SVGElement("feTurbulence")}}

## Beispiel

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg viewBox="0 0 220 220" xmlns="http://www.w3.org/2000/svg">
  <filter id="displacementFilter">
    <feTurbulence
      type="turbulence"
      baseFrequency="0.05"
      numOctaves="2"
      result="turbulence" />
    <feDisplacementMap
      in2="turbulence"
      in="SourceGraphic"
      scale="50"
      xChannelSelector="R"
      yChannelSelector="G" />
  </filter>

  <circle cx="100" cy="100" r="100" style="filter: url(#displacementFilter)" />
</svg>
```

{{EmbedLiveSample("Example", 220, 220)}}

## Nutzungshinweise

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Wert</th>
      <td><code>&#x3C;filter-primitive-reference></code></td>
    </tr>
    <tr>
      <th scope="row">Standardwert</th>
      <td><em>Keiner</em></td>
    </tr>
    <tr>
      <th scope="row">Animierbar</th>
      <td>Ja</td>
    </tr>
  </tbody>
</table>

- `<filter-primitive-reference>`
  - : Dieser Wert ist ein {{cssxref("custom-ident")}} und definiert den Namen für das Filter-Primitive. Es ist nur innerhalb eines bestimmten {{SVGElement("filter")}}-Elements sinnvoll und hat daher nur lokalen Geltungsbereich. Es ist zulässig, dass derselbe `<filter-primitive-reference>` mehrfach innerhalb desselben `<filter>`-Elements erscheint. Wenn referenziert, verwendet dieser Wert das nächstgelegene vorhergehende Filter-Primitive mit dem angegebenen Ergebnis.

## Spezifikationen

{{Specifications}}
