---
title: Array.prototype.toSorted()
slug: Web/JavaScript/Reference/Global_Objects/Array/toSorted
l10n:
  sourceCommit: e8320dfbed49d37589d0fe759ef6506885f340f7
---

{{JSRef}}

Die **`toSorted()`** Methode von {{jsxref("Array")}} Instanzen ist die [kopierende](/de/docs/Web/JavaScript/Reference/Global_Objects/Array#copying_methods_and_mutating_methods) Version der {{jsxref("Array/sort", "sort()")}} Methode. Sie gibt ein neues Array zurück, dessen Elemente in aufsteigender Reihenfolge sortiert sind.

## Syntax

```js-nolint
toSorted()
toSorted(compareFn)
```

### Parameter

- `compareFn` {{optional_inline}}
  - : Eine Funktion, die die Reihenfolge der Elemente bestimmt. Wird sie weggelassen, werden die Array-Elemente in Strings konvertiert und dann entsprechend dem Unicode-Codepunktwert jedes Zeichens sortiert. Weitere Informationen finden Sie unter {{jsxref("Array/sort", "sort()")}}.

### Rückgabewert

Ein neues Array mit den in aufsteigender Reihenfolge sortierten Elementen.

## Beschreibung

Weitere Informationen zum `compareFn` Parameter finden Sie unter {{jsxref("Array/sort", "sort()")}}.

Beim Einsatz auf [sparse Arrays](/de/docs/Web/JavaScript/Guide/Indexed_collections#sparse_arrays) iteriert die `toSorted()` Methode leere Stellen, als ob sie den Wert `undefined` hätten.

Die `toSorted()` Methode ist [generisch](/de/docs/Web/JavaScript/Reference/Global_Objects/Array#generic_array_methods). Sie erwartet lediglich, dass der `this` Wert eine `length` Eigenschaft und integerindizierte Eigenschaften besitzt.

## Beispiele

### Sortieren eines Arrays

```js
const months = ["Mar", "Jan", "Feb", "Dec"];
const sortedMonths = months.toSorted();
console.log(sortedMonths); // ['Dec', 'Feb', 'Jan', 'Mar']
console.log(months); // ['Mar', 'Jan', 'Feb', 'Dec']

const values = [1, 10, 21, 2];
const sortedValues = values.toSorted((a, b) => a - b);
console.log(sortedValues); // [1, 2, 10, 21]
console.log(values); // [1, 10, 21, 2]
```

Für weitere Anwendungsbeispiele siehe {{jsxref("Array/sort", "sort()")}}.

### Verwendung von toSorted() bei sparse Arrays

Leere Stellen werden sortiert, als hätten sie den Wert `undefined`. Sie werden immer ans Ende des Arrays sortiert, und `compareFn` wird für sie nicht aufgerufen.

```js
console.log(["a", "c", , "b"].toSorted()); // ['a', 'b', 'c', undefined]
console.log([, undefined, "a", "b"].toSorted()); // ["a", "b", undefined, undefined]
```

### Aufrufen von toSorted() auf Nicht-Array-Objekten

Die `toSorted()` Methode liest die `length` Eigenschaft von `this`. Dann sammelt sie alle existierenden integerindizierten Eigenschaften im Bereich von `0` bis `length - 1`, sortiert sie und schreibt sie in ein neues Array.

```js
const arrayLike = {
  length: 3,
  unrelated: "foo",
  0: 5,
  2: 4,
  3: 3, // ignored by toSorted() since length is 3
};
console.log(Array.prototype.toSorted.call(arrayLike));
// [4, 5, undefined]
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Polyfill von `Array.prototype.toSorted` in `core-js`](https://github.com/zloirock/core-js#change-array-by-copy)
- [es-shims Polyfill von `Array.prototype.toSorted`](https://www.npmjs.com/package/array.prototype.tosorted)
- [Leitfaden zu indizierten Sammlungen](/de/docs/Web/JavaScript/Guide/Indexed_collections)
- {{jsxref("Array.prototype.sort()")}}
- {{jsxref("Array.prototype.toReversed()")}}
- {{jsxref("Array.prototype.toSpliced()")}}
- {{jsxref("Array.prototype.with()")}}
- {{jsxref("TypedArray.prototype.toSorted()")}}
