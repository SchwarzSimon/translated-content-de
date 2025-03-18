---
title: SVGAnimatedAngle
slug: Web/API/SVGAnimatedAngle
l10n:
  sourceCommit: c2fd97474834e061404b992c8397d4ccc4439a71
---

{{APIRef("SVG")}}

## Überblick über die Schnittstelle

Die `SVGAnimatedAngle`-Schnittstelle wird für Attribute des Basistyps [\<angle>](/de/docs/Web/SVG/Guides/Content_type#angle) verwendet, die animiert werden können.

### Schnittstellenübersicht

<table class="no-markdown">
  <tbody>
    <tr>
      <th scope="row">Implementiert auch</th>
      <td><em>Keine</em></td>
    </tr>
    <tr>
      <th scope="row">Methoden</th>
      <td><em>Keine</em></td>
    </tr>
    <tr>
      <th scope="row">Eigenschaften</th>
      <td>
        <ul>
          <li>
            readonly [`SVGAngle`](/de/docs/Web/API/SVGAngle) <code>baseVal</code>
          </li>
          <li>
            readonly [`SVGAngle`](/de/docs/Web/API/SVGAngle) <code>animVal</code>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th scope="row">Normatives Dokument</th>
      <td>
        <a
          href="https://www.w3.org/TR/SVG11/types.html#InterfaceSVGAnimatedAngle"
          >SVG 1.1 (2nd Edition)</a
        >
      </td>
    </tr>
  </tbody>
</table>

## Instanz-Eigenschaften

<table class="no-markdown">
  <thead>
    <tr>
      <th>Name</th>
      <th>Typ</th>
      <th>Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>[`SVGAnimatedAngle.baseVal`](/de/docs/Web/API/SVGAnimatedAngle/baseVal)</code></td>
      <td>[`SVGAngle`](/de/docs/Web/API/SVGAngle)</td>
      <td>
        Der Basiswert des gegebenen Attributs vor dem Anwenden von Animationen.
      </td>
    </tr>
    <tr>
      <td><code>[`SVGAnimatedAngle.animVal`](/de/docs/Web/API/SVGAnimatedAngle/animVal)</code></td>
      <td>[`SVGAngle`](/de/docs/Web/API/SVGAngle)</td>
      <td>
        Ein schreibgeschützter [`SVGAngle`](/de/docs/Web/API/SVGAngle), der den aktuellen
        animierten Wert des gegebenen Attributs darstellt. Wenn das gegebene Attribut derzeit
        nicht animiert wird, hat der [`SVGAngle`](/de/docs/Web/API/SVGAngle) denselben Inhalt wie
        <code>baseVal</code>. Das durch <code>animVal</code> referenzierte Objekt wird immer
        vom durch <code>baseVal</code> referenzierten Objekt unterscheidbar sein, auch wenn
        das Attribut nicht animiert ist.
      </td>
    </tr>
  </tbody>
</table>

## Instanz-Methoden

Die `SVGAnimatedAngle`-Schnittstelle bietet keine spezifischen Methoden.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
