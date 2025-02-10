---
title: <feTurbulence>
slug: Web/SVG/Element/feTurbulence
l10n:
  sourceCommit: 332c4375206089fa38609d6d9e3fe2cd7a502f22
---

{{SVGRef}}

Der **`<feTurbulence>`** [SVG](/de/docs/Web/SVG)-Filterprimitive erzeugt ein Bild mithilfe der [Perlin-Turbulenzfunktion](https://en.wikipedia.org/wiki/Perlin_noise). Dies ermöglicht die Synthese künstlicher Texturen wie Wolken oder Marmor. Das resultierende Bild füllt die gesamte Subregion des Filterprimitives aus.

Wie bei anderen Filterprimitives werden Farbbestandteile standardmäßig im `linearRGB`-{{Glossary("color_space", "Farbraum")}} verarbeitet. Sie können {{svgattr("color-interpolation-filters")}} verwenden, um stattdessen `sRGB` zu nutzen.

## Verwendungskontext

{{svginfo}}

## Attribute

- {{SVGAttr("baseFrequency")}}
- {{SVGAttr("numOctaves")}}
- {{SVGAttr("seed")}}
- {{SVGAttr("stitchTiles")}}
- {{SVGAttr("type")}}

## DOM-Schnittstelle

Dieses Element implementiert die Schnittstelle [`SVGFETurbulenceElement`](/de/docs/Web/API/SVGFETurbulenceElement).

## Beispiel

```html
<svg
  width="200"
  height="200"
  viewBox="0 0 220 220"
  xmlns="http://www.w3.org/2000/svg">
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

{{EmbedLiveSample('Example', 220, 220)}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [SVG-Filterprimitive-Attribute](/de/docs/Web/SVG/Attribute#filter_primitive_attributes), einschließlich {{SVGAttr('result')}}.
- {{SVGElement("filter")}}
- {{SVGElement("animate")}}
- {{SVGElement("set")}}
- {{SVGElement("feBlend")}}
- {{SVGElement("feColorMatrix")}}
- {{SVGElement("feComponentTransfer")}}
- {{SVGElement("feComposite")}}
- {{SVGElement("feConvolveMatrix")}}
- {{SVGElement("feDiffuseLighting")}}
- {{SVGElement("feDisplacementMap")}}
- {{SVGElement("feFlood")}}
- {{SVGElement("feGaussianBlur")}}
- {{SVGElement("feImage")}}
- {{SVGElement("feMerge")}}
- {{SVGElement("feMorphology")}}
- {{SVGElement("feOffset")}}
- {{SVGElement("feSpecularLighting")}}
- {{SVGElement("feTile")}}
- [SVG-Tutorial: Filter-Effekte](/de/docs/Web/SVG/Tutorial/Filter_effects)
