---
title: <set>
slug: Web/SVG/Reference/Element/set
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

Das **`<set>`** [SVG](/de/docs/Web/SVG)-Element bietet eine Methode, um den Wert eines Attributs für eine bestimmte Dauer festzulegen.

Es unterstützt alle Attributtypen, einschließlich solcher, die nicht sinnvoll interpoliert werden können, wie Zeichenfolgen und boolesche Werte. Für Attribute, die sinnvoll interpoliert werden können, wird normalerweise das {{SVGElement('animate')}} bevorzugt.

> [!NOTE]
> Das `<set>`-Element ist nicht additiv. Die Attribute {{SVGAttr('additive')}} und {{SVGAttr('accumulate')}} sind nicht erlaubt und werden ignoriert, falls sie angegeben werden.

## Beispiel

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg viewBox="0 0 10 10" xmlns="http://www.w3.org/2000/svg">
  <style>
    rect {
      cursor: pointer;
    }
    .round {
      rx: 5px;
      fill: green;
    }
  </style>

  <rect id="me" width="10" height="10">
    <set attributeName="class" to="round" begin="me.click" dur="2s" />
  </rect>
</svg>
```

{{EmbedLiveSample('Example', 150, '100%')}}

## Attribute

- {{SVGAttr("to")}}
  - : Dieses Attribut definiert den Wert, der dem Zielattribut für die Dauer der Animation zugewiesen wird. Der Wert muss den Anforderungen des Zielattributs entsprechen.
    _Werttyp_: [**\<anything>**](/de/docs/Web/SVG/Guides/Content_type#anything); _Standardwert_: keiner; _Animierbar_: **nein**

## Nutzungskontext

{{svginfo}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{SVGAttr("attributeName")}} Attribut
- [Animationstiming-Attribute](/de/docs/Web/SVG/Reference/Attribute#animation_timing_attributes), einschließlich {{SVGAttr("begin")}}, {{SVGAttr("dur")}}, {{SVGAttr("end")}}, {{SVGAttr("min")}}, {{SVGAttr("max")}}, {{SVGAttr("restart")}}, {{SVGAttr("repeatCount")}}, {{SVGAttr("repeatDur")}}, und {{SVGAttr("fill")}}.
- {{SVGElement("animate")}}
