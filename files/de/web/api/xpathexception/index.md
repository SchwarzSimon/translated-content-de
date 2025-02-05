---
title: XPathException
slug: Web/API/XPathException
l10n:
  sourceCommit: 3e1b5277c6451e7d27ab628f23fb9702947a7a7b
---

{{APIRef("DOM XPath")}}{{Deprecated_Header}}

In der [DOM XPath API](/de/docs/Web/XML/XPath) repräsentiert das **`XPathException`**-Interface Ausnahmebedingungen, die während der Ausführung von XPath-Operationen auftreten können.

## Instanz-Eigenschaften

- [`XPathException.code`](/de/docs/Web/API/XPathException/code) {{ReadOnlyInline}}
  - : Gibt einen `short` zurück, der einen der [Fehlercode-Konstanten](#konstanten) enthält.

## Konstanten

<table class="no-markdown">
  <thead>
    <tr>
      <th scope="col">Konstante</th>
      <th scope="col">Wert</th>
      <th scope="col">Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>INVALID_EXPRESSION_ERR</code></td>
      <td><code>51</code></td>
      <td>
        Wenn der Ausdruck einen Syntaxfehler enthält oder anderweitig kein gültiger Ausdruck gemäß den Regeln des spezifischen [`XPathEvaluator`](/de/docs/Web/API/XPathEvaluator) ist oder spezialisierte Erweiterungsfunktionen oder Variablen enthält, die von dieser Implementierung nicht unterstützt werden.
      </td>
    </tr>
    <tr>
      <td><code>TYPE_ERR</code></td>
      <td><code>52</code></td>
      <td>
        Wenn der Ausdruck nicht in den angegebenen Typ umgewandelt werden kann.
      </td>
    </tr>
  </tbody>
</table>

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`Document.createExpression()`](/de/docs/Web/API/Document/createExpression)
- [`XPathExpression`](/de/docs/Web/API/XPathExpression)
