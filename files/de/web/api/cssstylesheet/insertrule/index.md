---
title: "CSSStyleSheet: insertRule() Methode"
short-title: insertRule()
slug: Web/API/CSSStyleSheet/insertRule
l10n:
  sourceCommit: 5b20f5f4265f988f80f513db0e4b35c7e0cd70dc
---

{{APIRef("CSSOM")}}

Die **`CSSStyleSheet.insertRule()`**-Methode fügt eine neue [CSS-Regel](/de/docs/Web/API/CSSRule) in das [aktuelle Stylesheet](/de/docs/Web/API/CSSStyleSheet) ein.

> [!NOTE]
> Obwohl `insertRule()` exklusiv eine Methode von
> [`CSSStyleSheet`](/de/docs/Web/API/CSSStyleSheet) ist, fügt sie die Regel tatsächlich in
> `[CSSStyleSheet](/de/docs/Web/API/CSSStyleSheet).cssRules` ein — seine interne
> [`CSSRuleList`](/de/docs/Web/API/CSSRuleList).

## Syntax

```js-nolint
insertRule(rule)
insertRule(rule, index)
```

### Parameter

- `rule`

  - : Ein String, der die einzufügende Regel enthält. Was die eingefügte
    Regel enthalten muss, hängt von ihrem Typ ab:

    - **Für [Rule-Sets](/de/docs/Web/CSS/Syntax#css_statements)**, sowohl
      einen [Selektor](/de/docs/Learn_web_development/Core/Styling_basics/Basic_selectors) als auch eine
      Stil-Deklaration.
    - **Für [At-Rules](/de/docs/Web/CSS/At-rule)**, sowohl eine
      At-Kennung als auch den Regelinhalt.

- `index` {{optional_inline}}
  - : Ein positiver Integer, der kleiner oder gleich `stylesheet.cssRules.length` ist,
    und die Position der neu eingefügten Regel in
    `[CSSStyleSheet](/de/docs/Web/API/CSSStyleSheet).cssRules` darstellt. Der Standardwert ist
    `0`. (In älteren Implementierungen war dies erforderlich. Siehe [Browser-Kompatibilität](#browser-kompatibilität) für Details.)

### Rückgabewert

Der Index der neu eingefügten Regel innerhalb der Regel-Liste des Stylesheets.

### Ausnahmen

- `IndexSizeError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn `index` > `[CSSRuleList](/de/docs/Web/API/CSSRuleList).length` ist.
- `HierarchyRequestError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn `rule` aufgrund einer CSS-Beschränkung nicht an `index` `0` eingefügt werden kann.
- `SyntaxError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn mehr als eine Regel im `rule`-Parameter angegeben wird.
- `HierarchyRequestError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn versucht wird, ein {{cssxref("@import")}} At-Regel nach einer Stilregel einzufügen.
- `InvalidStateError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn `rule` ein {{cssxref("@namespace")}} ist und die Regel-Liste mehr als nur `@import` At-Regeln und/oder `@namespace` At-Regeln enthält.

## Beispiele

### Einfügen einer neuen Regel

Dieser Ausschnitt fügt eine neue Regel an den Anfang meines Stylesheets ein.

```js
myStyle.insertRule("#blanc { color: white }", 0);
```

### Funktion zum Hinzufügen einer Stylesheet-Regel

```js
/**
 * Add a stylesheet rule to the document (it may be better practice
 * to dynamically change classes, so style information can be kept in
 * genuine stylesheets and avoid adding extra elements to the DOM).
 * Note that an array is needed for declarations and rules since ECMAScript does
 * not guarantee a predictable object iteration order, and since CSS is
 * order-dependent.
 * @param {Array} rules Accepts an array of JSON-encoded declarations
 * @example
addStylesheetRules([
  ['h2', // Also accepts a second argument as an array of arrays instead
    ['color', 'red'],
    ['background-color', 'green', true] // 'true' for !important rules
  ],
  ['.myClass',
    ['background-color', 'yellow']
  ]
]);
*/
function addStylesheetRules(rules) {
  const styleEl = document.createElement("style");

  // Append <style> element to <head>
  document.head.appendChild(styleEl);

  // Grab style element's sheet
  const styleSheet = styleEl.sheet;

  for (let i = 0; i < rules.length; i++) {
    let j = 1,
      rule = rules[i],
      selector = rule[0],
      propStr = "";
    // If the second argument of a rule is an array of arrays, correct our variables.
    if (Array.isArray(rule[1][0])) {
      rule = rule[1];
      j = 0;
    }

    for (let pl = rule.length; j < pl; j++) {
      const prop = rule[j];
      propStr += `${prop[0]}: ${prop[1]}${prop[2] ? " !important" : ""};\n`;
    }

    // Insert CSS Rule
    styleSheet.insertRule(
      `${selector}{${propStr}}`,
      styleSheet.cssRules.length,
    );
  }
}
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`CSSStyleSheet.deleteRule`](/de/docs/Web/API/CSSStyleSheet/deleteRule)
- [Konstruierbare Stylesheets](https://web.dev/articles/constructable-stylesheets) (web.dev)
