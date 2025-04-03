---
title: String.prototype.slice()
slug: Web/JavaScript/Reference/Global_Objects/String/slice
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{JSRef}}

Die **`slice()`**-Methode von {{jsxref("String")}}-Werten extrahiert einen Abschnitt dieses Strings und liefert ihn als neuen String zurück, ohne den ursprünglichen String zu ändern.

{{InteractiveExample("JavaScript Demo: String.prototype.slice()", "taller")}}

```js interactive-example
const str = "The quick brown fox jumps over the lazy dog.";

console.log(str.slice(31));
// Expected output: "the lazy dog."

console.log(str.slice(4, 19));
// Expected output: "quick brown fox"

console.log(str.slice(-4));
// Expected output: "dog."

console.log(str.slice(-9, -5));
// Expected output: "lazy"
```

## Syntax

```js-nolint
slice(indexStart)
slice(indexStart, indexEnd)
```

### Parameter

- `indexStart`
  - : Der Index des ersten Zeichens, das im zurückgegebenen Teilstring enthalten sein soll.
- `indexEnd` {{optional_inline}}
  - : Der Index des ersten Zeichens, das im zurückgegebenen Teilstring ausgeschlossen sein soll.

### Rückgabewert

Ein neuer String, der den extrahierten Abschnitt des Strings enthält.

## Beschreibung

`slice()` extrahiert den Text aus einem String und gibt einen neuen String zurück.

`slice()` extrahiert bis, aber nicht einschließlich `indexEnd`. Zum Beispiel extrahiert `str.slice(4, 8)` das fünfte Zeichen bis zum achten Zeichen (die Zeichen mit den Indizes `4`, `5`, `6` und `7`):

```plain
              indexStart        indexEnd
                  ↓               ↓
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| T | h | e |   | m | i | r | r | o | r |

                  m   i   r   r
                 _______________
                      ↑
                    Result
```

- Wenn `indexStart >= str.length`, wird ein leerer String zurückgegeben.
- Wenn `indexStart < 0`, wird der Index vom Ende des Strings gezählt. Genauer gesagt beginnt in diesem Fall der Teilstring bei `max(indexStart + str.length, 0)`.
- Wenn `indexStart` weggelassen, `undefined` ist oder nicht in eine Zahl [umgewandelt werden kann](/de/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion), wird es als `0` behandelt.
- Wenn `indexEnd` weggelassen oder `undefined` ist oder wenn `indexEnd >= str.length`, extrahiert `slice()` bis zum Ende des Strings.
- Wenn `indexEnd < 0`, wird der Index vom Ende des Strings gezählt. Genauer gesagt endet in diesem Fall der Teilstring bei `max(indexEnd + str.length, 0)`.
- Wenn `indexEnd <= indexStart` nach Normalisieren negativer Werte (d.h. `indexEnd` stellt ein Zeichen dar, das vor `indexStart` liegt), wird ein leerer String zurückgegeben.

## Beispiele

### Verwenden von slice(), um einen neuen String zu erstellen

Das folgende Beispiel verwendet `slice()`, um einen neuen String zu erstellen.

```js
const str1 = "The morning is upon us."; // The length of str1 is 23.
const str2 = str1.slice(1, 8);
const str3 = str1.slice(4, -2);
const str4 = str1.slice(12);
const str5 = str1.slice(30);
console.log(str2); // he morn
console.log(str3); // morning is upon u
console.log(str4); // is upon us.
console.log(str5); // ""
```

### Verwenden von slice() mit negativen Indizes

Das folgende Beispiel verwendet `slice()` mit negativen Indizes.

```js
const str = "The morning is upon us.";
str.slice(-3); // 'us.'
str.slice(-3, -1); // 'us'
str.slice(0, -1); // 'The morning is upon us'
str.slice(4, -1); // 'morning is upon us'
```

In diesem Beispiel wird rückwärts vom Ende des Strings um `11` gezählt, um den Startindex zu finden, und vorwärts vom Anfang des Strings um `16`, um den Endindex zu bestimmen.

```js
console.log(str.slice(-11, 16)); // "is u"
```

Hier wird vorwärts vom Anfang um `11` gezählt, um den Startindex zu bestimmen, und rückwärts vom Ende um `7`, um den Endindex zu finden.

```js
console.log(str.slice(11, -7)); // " is u"
```

Diese Argumente zählen rückwärts vom Ende um `5`, um den Startindex zu finden, und rückwärts vom Ende um `1`, um den Endindex zu bestimmen.

```js
console.log(str.slice(-5, -1)); // "n us"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{jsxref("String.prototype.substr()")}}
- {{jsxref("String.prototype.substring()")}}
- {{jsxref("Array.prototype.slice()")}}
