---
title: String.prototype.toWellFormed()
slug: Web/JavaScript/Reference/Global_Objects/String/toWellFormed
l10n:
  sourceCommit: e8320dfbed49d37589d0fe759ef6506885f340f7
---

{{JSRef}}

Die **`toWellFormed()`** Methode von {{jsxref("String")}}-Werten gibt einen String zurück, bei dem alle [einsamen Surrogate](/de/docs/Web/JavaScript/Reference/Global_Objects/String#utf-16_characters_unicode_code_points_and_grapheme_clusters) dieses Strings durch das Unicode-Ersatzzeichen U+FFFD ersetzt werden.

## Syntax

```js-nolint
toWellFormed()
```

### Parameter

Keine.

### Rückgabewert

Ein neuer String, der eine Kopie dieses Strings ist, wobei alle einsamen Surrogate durch das Unicode-Ersatzzeichen U+FFFD ersetzt wurden. Wenn `str` [wohlgeformt ist](/de/docs/Web/JavaScript/Reference/Global_Objects/String/isWellFormed), wird dennoch ein neuer String zurückgegeben (im Wesentlichen eine Kopie von `str`).

## Beschreibung

Strings in JavaScript sind UTF-16 kodiert. In der UTF-16-Kodierung gibt es das Konzept der _Surrogatpaare_, das im Abschnitt über [UTF-16-Zeichen, Unicode-Codepunkte und Graphemcluster](/de/docs/Web/JavaScript/Reference/Global_Objects/String#utf-16_characters_unicode_code_points_and_grapheme_clusters) ausführlich erläutert wird.

`toWellFormed()` durchläuft die Codeeinheiten dieses Strings und ersetzt alle einsamen Surrogate durch das [Unicode-Ersatzzeichen](<https://en.wikipedia.org/wiki/Specials_(Unicode_block)#Replacement_character>) U+FFFD `�`. Dies stellt sicher, dass der zurückgegebene String wohlgeformt ist und in Funktionen verwendet werden kann, die wohlgeformte Strings erwarten, wie z.B. {{jsxref("encodeURI")}}. Im Vergleich zu einer benutzerdefinierten Implementierung ist `toWellFormed()` effizienter, da Engines direkt auf die interne Darstellung von Strings zugreifen können.

Wenn schlecht geformte Strings in bestimmten Kontexten verwendet werden, wie zum Beispiel beim [`TextEncoder`](/de/docs/Web/API/TextEncoder), werden sie automatisch in wohlgeformte Strings umgewandelt, indem das gleiche Ersatzzeichen verwendet wird. Wenn einsame Surrogate gerendert werden, werden sie ebenfalls als Ersatzzeichen gerendert (ein Diamant mit einem Fragezeichen darin).

## Beispiele

### Verwendung von toWellFormed()

```js
const strings = [
  // Lone leading surrogate
  "ab\uD800",
  "ab\uD800c",
  // Lone trailing surrogate
  "\uDFFFab",
  "c\uDFFFab",
  // Well-formed
  "abc",
  "ab\uD83D\uDE04c",
];

for (const str of strings) {
  console.log(str.toWellFormed());
}
// Logs:
// "ab�"
// "ab�c"
// "�ab"
// "c�ab"
// "abc"
// "ab😄c"
```

### Vermeidung von Fehlern in encodeURI()

{{jsxref("encodeURI")}} wirft einen Fehler, wenn der übergebene String nicht wohlgeformt ist. Dies kann vermieden werden, indem `toWellFormed()` verwendet wird, um den String zuerst in einen wohlgeformten String umzuwandeln.

```js
const illFormed = "https://example.com/search?q=\uD800";

try {
  encodeURI(illFormed);
} catch (e) {
  console.log(e); // URIError: URI malformed
}

console.log(encodeURI(illFormed.toWellFormed())); // "https://example.com/search?q=%EF%BF%BD"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Polyfill von `String.prototype.toWellFormed` in `core-js`](https://github.com/zloirock/core-js#well-formed-unicode-strings)
- [es-shims Polyfill von `String.prototype.toWellFormed`](https://www.npmjs.com/package/string.prototype.towellformed)
- {{jsxref("String.prototype.isWellFormed()")}}
- {{jsxref("String.prototype.normalize()")}}
