---
title: filter
slug: Web/SVG/Attribute/filter
l10n:
  sourceCommit: 4030a3382d2f2ee9a2aa6232c1fbb5724a27cc8b
---

{{SVGRef}}

Das **`filter`** Attribut gibt die durch das {{SVGElement("filter")}}-Element definierten Filtereffekte an, die auf das jeweilige Element angewendet werden sollen.

> [!NOTE]
> Als Präsentationsattribut kann `filter` als CSS-Eigenschaft verwendet werden. Weitere Informationen finden Sie unter CSS {{cssxref("filter")}}.

Als Präsentationsattribut kann es auf jedes Element angewendet werden, hat jedoch nur Wirkung auf [Container-Elemente](/de/docs/Web/SVG/Element#container_elements) ohne das {{SVGElement("defs")}}-Element, auf alle [Grafikelemente](/de/docs/Web/SVG/Element#graphics_elements) und das {{SVGElement("use")}}-Element.

## Beispiel

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <filter id="blur">
    <feGaussianBlur stdDeviation="2" />
  </filter>

  <rect x="10" y="10" width="80" height="80" filter="url(#blur)" />
</svg>
```

{{EmbedLiveSample("Example", "220", "220")}}

## Nutzungshinweise

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Wert</th>
      <td>
        <code>none</code>
        <a
          href="/de/docs/Web/CSS/Value_definition_syntax#single_bar"
          title="Einzelner Balken: genau eine der Einheiten muss vorhanden sein"
          >|</a
        >
        <code>&#x3C;filter-value-list></code>
      </td>
    </tr>
    <tr>
      <th scope="row">Standardwert</th>
      <td><code>none</code></td>
    </tr>
    <tr>
      <th scope="row">Animierbar</th>
      <td>Ja</td>
    </tr>
  </tbody>
</table>

Eine Beschreibung der Werte finden Sie in der CSS-Eigenschaft {{cssxref("filter")}}.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{SVGElement("filter")}}
- {{cssxref("filter")}}
