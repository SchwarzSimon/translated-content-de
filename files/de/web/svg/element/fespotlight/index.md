---
title: <feSpotLight>
slug: Web/SVG/Element/feSpotLight
l10n:
  sourceCommit: 332c4375206089fa38609d6d9e3fe2cd7a502f22
---

{{SVGRef}}

Das **`<feSpotLight>`** [SVG](/de/docs/Web/SVG)-Filter-Primitiv definiert eine Lichtquelle, die verwendet werden kann, um einen Spotlight-Effekt zu erzeugen.
Es wird innerhalb eines Beleuchtungs-Filter-Primitives verwendet: {{SVGElement("feDiffuseLighting")}} oder {{SVGElement("feSpecularLighting")}}.

Wie andere Filter-Primitiven verarbeitet es Farbkomponenten standardmäßig im `linearRGB`-{{Glossary("color_space", "Farbraum")}}. Sie können {{svgattr("color-interpolation-filters")}} verwenden, um stattdessen `sRGB` zu nutzen.

## Verwendungskontext

{{svginfo}}

## Attribute

- {{SVGAttr("x")}}
- {{SVGAttr("y")}}
- {{SVGAttr("z")}}
- {{SVGAttr("pointsAtX")}}
- {{SVGAttr("pointsAtY")}}
- {{SVGAttr("pointsAtZ")}}
- {{SVGAttr("specularExponent")}}
- {{SVGAttr("limitingConeAngle")}}

## DOM-Schnittstelle

Dieses Element implementiert die [`SVGFESpotLightElement`](/de/docs/Web/API/SVGFESpotLightElement)-Schnittstelle.

## Beispiel

### HTML

```html
<svg
  width="200"
  height="200"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <filter id="spotlight">
      <feSpecularLighting
        result="spotlight"
        specularConstant="1.5"
        specularExponent="4"
        lighting-color="#FFF">
        <feSpotLight x="600" y="600" z="400" limitingConeAngle="5.5" />
      </feSpecularLighting>
      <feComposite
        in="SourceGraphic"
        in2="spotlight"
        operator="out"
        k1="0"
        k2="1"
        k3="1"
        k4="0" />
    </filter>
  </defs>

  <image
    href="mdn_logo_only_color.png"
    x="10%"
    y="10%"
    width="80%"
    height="80%"
    style="filter:url(#spotlight);" />
</svg>
```

### Ergebnis

{{EmbedLiveSample("Example", 200, 200)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{SVGElement("filter")}}
- {{SVGElement("animate")}}
- {{SVGElement("set")}}
- {{SVGElement("feDiffuseLighting")}}
- {{SVGElement("feSpecularLighting")}}
- {{SVGElement("feDistantLight")}}
- {{SVGElement("fePointLight")}}
- [SVG-Tutorial: Filtereffekte](/de/docs/Web/SVG/Tutorial/Filter_effects)
