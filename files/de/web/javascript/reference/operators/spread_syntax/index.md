---
title: Spread-Syntaxus (...)
slug: Web/JavaScript/Reference/Operators/Spread_syntax
l10n:
  sourceCommit: 9645d14f12d9b93da98daaf25a443bb6cac3f2a6
---

{{jsSidebar("Operators")}}

Die **Spread-Syntaxus (`...`)** ermöglicht es, einen iterierbaren, wie ein Array oder einen String, an Stellen zu expandieren, an denen null oder mehr Argumente (für Funktionsaufrufe) oder Elemente (für Array-Literale) erwartet werden. In einem Objektliteral listet die Spread-Syntaxus die Eigenschaften eines Objekts auf und fügt die Schlüssel-Wert-Paare dem neu erstellten Objekt hinzu.

Die Spread-Syntaxus sieht genau wie die Rest-Syntaxus aus. In gewisser Weise ist die Spread-Syntaxus das Gegenteil der Rest-Syntaxus. Die Spread-Syntaxus "erweitert" ein Array in seine Elemente, während die Rest-Syntaxus mehrere Elemente sammelt und sie zu einem einzigen Element "verdichtet". Siehe [Rest-Parameter](/de/docs/Web/JavaScript/Reference/Functions/rest_parameters) und [Rest-Eigenschaft](/de/docs/Web/JavaScript/Reference/Operators/Destructuring#rest_property).

{{InteractiveExample("JavaScript Demo: Spread-Syntaxus (...)")}}

```js interactive-example
function sum(x, y, z) {
  return x + y + z;
}

const numbers = [1, 2, 3];

console.log(sum(...numbers));
// Expected output: 6

console.log(sum.apply(null, numbers));
// Expected output: 6
```

## Syntax

```js-nolint
myFunction(a, ...iterableObj, b)
[1, ...iterableObj, '4', 'five', 6]
{ ...obj, key: 'value' }
```

## Beschreibung

Die Spread-Syntaxus kann verwendet werden, wenn alle Elemente aus einem Objekt oder Array in einem neuen Array oder Objekt enthalten sein sollen oder ein Element nach dem anderen in der Argumentenliste eines Funktionsaufrufs angewendet werden soll. Es gibt drei verschiedene Orte, die die Spread-Syntaxus akzeptieren:

- [Funktionsargumentenliste](#spread_in_funktionsaufrufen) (`myFunction(a, ...iterableObj, b)`)
- [Array-Literale](#spread_in_array-literalen) (`[1, ...iterableObj, '4', 'five', 6]`)
- [Objekt-Literale](#spread_in_objekt-literalen) (`{ ...obj, key: 'value' }`)

Obwohl die Syntax gleich aussieht, haben sie leicht unterschiedliche Semantiken.

Nur [iterierbare](/de/docs/Web/JavaScript/Reference/Iteration_protocols) Werte, wie {{jsxref("Array")}} und {{jsxref("String")}}, können in [Array-Literalen](/de/docs/Web/JavaScript/Guide/Grammar_and_types#array_literals) und Argumentlisten gespreadet werden. Viele Objekte sind nicht iterierbar, einschließlich aller [einfachen Objekte](/de/docs/Web/JavaScript/Reference/Global_Objects/Object), die keine [`Symbol.iterator`](/de/docs/Web/JavaScript/Reference/Global_Objects/Symbol/iterator)-Methode haben:

```js example-bad
const obj = { key1: "value1" };
const array = [...obj]; // TypeError: obj is not iterable
```

Andererseits, das Spreaden in [Objekt-Literalen](/de/docs/Web/JavaScript/Reference/Operators/Object_initializer) [zählt](/de/docs/Web/JavaScript/Guide/Enumerability_and_ownership_of_properties#traversing_object_properties) die eigenen Eigenschaften des Wertes auf. Für typische Arrays sind alle Indizes aufzählbare eigene Eigenschaften, sodass Arrays in Objekte gespreadet werden können.

```js
const array = [1, 2, 3];
const obj = { ...array }; // { 0: 1, 1: 2, 2: 3 }
```

Alle [Primitiven](/de/docs/Web/JavaScript/Guide/Data_structures#primitive_values) können in Objekte gespreadet werden. Nur Strings haben aufzählbare eigene Eigenschaften, und das Spreaden von allem anderen erzeugt keine Eigenschaften auf dem neuen Objekt.

```js
const obj = { ...true, ..."test", ...10 };
// { '0': 't', '1': 'e', '2': 's', '3': 't' }
```

Beim Verwenden der Spread-Syntaxus für Funktionsaufrufe achten Sie auf die Möglichkeit, das Längenlimit der JavaScript-Engine für Argumente zu überschreiten. Siehe {{jsxref("Function.prototype.apply()")}} für weitere Details.

## Beispiele

### Spread in Funktionsaufrufen

#### Anwendung von apply() ersetzen

Es ist üblich, {{jsxref("Function.prototype.apply()")}} in Fällen zu verwenden, in denen Sie die Elemente eines Arrays als Argumente für eine Funktion verwenden möchten.

```js
function myFunction(x, y, z) {}
const args = [0, 1, 2];
myFunction.apply(null, args);
```

Mit der Spread-Syntaxus kann das obige wie folgt geschrieben werden:

```js
function myFunction(x, y, z) {}
const args = [0, 1, 2];
myFunction(...args);
```

Jedes Argument in der Argumentenliste kann die Spread-Syntaxus verwenden, und die Spread-Syntaxus kann mehrfach verwendet werden.

```js
function myFunction(v, w, x, y, z) {}
const args = [0, 1];
myFunction(-1, ...args, 2, ...[3]);
```

#### Anwendung für den new-Operator

Beim Aufruf eines Konstruktors mit {{jsxref("Operators/new", "new")}} ist es nicht möglich, **direkt** ein Array und `apply()` zu verwenden, da `apply()` die Ziel-Funktion _aufruft_ anstatt sie _zu konstruieren_, was unter anderem bedeutet, dass [`new.target`](/de/docs/Web/JavaScript/Reference/Operators/new.target) `undefined` sein wird. Ein Array kann jedoch problemlos mit `new` verwendet werden, dank der Spread-Syntaxus:

```js
const dateFields = [1970, 0, 1]; // 1 Jan 1970
const d = new Date(...dateFields);
```

### Spread in Array-Literalen

#### Ein mächtigeres Array-Literal

Ohne Spread-Syntaxus reicht die Array-Literal-Syntax nicht mehr aus, um ein neues Array mit einem existierenden Array als Teil davon zu erstellen. Stattdessen muss imperativer Code verwendet werden, der Methoden wie {{jsxref("Array/push", "push()")}}, {{jsxref("Array/splice", "splice()")}}, {{jsxref("Array/concat", "concat()")}} usw. kombiniert. Mit der Spread-Syntaxus wird dies wesentlich prägnanter:

```js
const parts = ["shoulders", "knees"];
const lyrics = ["head", ...parts, "and", "toes"];
//  ["head", "shoulders", "knees", "and", "toes"]
```

Genau wie bei Argumentlisten kann `...` überall im Array-Literal verwendet werden und mehrfach verwendet werden.

#### Ein Array kopieren

Sie können die Spread-Syntaxus verwenden, um eine {{Glossary("shallow_copy", "flache Kopie")}} eines Arrays zu erstellen. Jedes Array-Element behält seine Identität, ohne kopiert zu werden.

```js
const arr = [1, 2, 3];
const arr2 = [...arr]; // like arr.slice()

arr2.push(4);
// arr2 becomes [1, 2, 3, 4]
// arr remains unaffected
```

Die Spread-Syntaxus geht effektiv nur eine Ebene tief, während sie ein Array kopiert. Daher kann es ungeeignet sein, mehrdimensionale Arrays zu kopieren. Dasselbe gilt für {{jsxref("Object.assign()")}} – keine native Operation in JavaScript führt ein tiefes Klonen durch. Die Web-API-Methode [`structuredClone()`](/de/docs/Web/API/Window/structuredClone) erlaubt das tiefere Kopieren von Werten bestimmter [unterstützter Typen](/de/docs/Web/API/Web_Workers_API/Structured_clone_algorithm#supported_types). Siehe {{Glossary("Shallow_copy", "flache Kopie")}} für weitere Details.

```js example-bad
const a = [[1], [2], [3]];
const b = [...a];

b.shift().shift();
// 1

// Oh no! Now array 'a' is affected as well:
console.log(a);
// [[], [2], [3]]
```

#### Eine bessere Art, Arrays zu verketten

{{jsxref("Array.prototype.concat()")}} wird häufig verwendet, um ein Array an das Ende eines vorhandenen Arrays zu verketten. Ohne Spread-Syntaxus geschieht dies wie folgt:

```js
let arr1 = [0, 1, 2];
const arr2 = [3, 4, 5];

// Append all items from arr2 onto arr1
arr1 = arr1.concat(arr2);
```

Mit der Spread-Syntaxus wird dies:

```js
let arr1 = [0, 1, 2];
const arr2 = [3, 4, 5];

arr1 = [...arr1, ...arr2];
// arr1 is now [0, 1, 2, 3, 4, 5]
```

{{jsxref("Array.prototype.unshift()")}} wird häufig verwendet, um ein Array von Werten am Anfang eines bestehenden Arrays einzufügen. Ohne Spread-Syntaxus geschieht dies so:

```js
const arr1 = [0, 1, 2];
const arr2 = [3, 4, 5];

//  Prepend all items from arr2 onto arr1
Array.prototype.unshift.apply(arr1, arr2);
console.log(arr1); // [3, 4, 5, 0, 1, 2]
```

Mit der Spread-Syntaxus wird dies:

```js
let arr1 = [0, 1, 2];
const arr2 = [3, 4, 5];

arr1 = [...arr2, ...arr1];
console.log(arr1); // [3, 4, 5, 0, 1, 2]
```

> [!NOTE]
> Anders als `unshift()`, erstellt dies ein neues `arr1`, anstatt das originale `arr1` Array direkt zu verändern.

#### Bedingtes Hinzufügen von Werten zu einem Array

Sie können ein Element in einem Array-Literal präsent oder abwesend machen, abhängig von einer Bedingung, mit einem [bedingten Operator](/de/docs/Web/JavaScript/Reference/Operators/Conditional_operator).

```js
const isSummer = false;
const fruits = ["apple", "banana", ...(isSummer ? ["watermelon"] : [])];
// ['apple', 'banana']
```

Wenn die Bedingung `false` ist, spreaden wir ein leeres Array, sodass nichts zum endgültigen Array hinzugefügt wird. Beachten Sie, dass dies anders ist als folgendes:

```js
const fruits = ["apple", "banana", isSummer ? "watermelon" : undefined];
// ['apple', 'banana', undefined]
```

In diesem Fall wird ein zusätzliches `undefined`-Element hinzugefügt, wenn `isSummer` `false` ist, und dieses Element wird von Methoden wie {{jsxref("Array.prototype.map()")}} besucht.

### Spread in Objekt-Literalen

#### Kopieren und Mergen von Objekten

Sie können die Spread-Syntaxus verwenden, um mehrere Objekte in ein neues Objekt zusammenzuführen.

```js
const obj1 = { foo: "bar", x: 42 };
const obj2 = { bar: "baz", y: 13 };

const mergedObj = { ...obj1, ...obj2 };
// { foo: "bar", x: 42, bar: "baz", y: 13 }
```

Ein einzelnes Spread erzeugt eine flache Kopie des ursprünglichen Objekts (aber ohne nicht aufzählbare Eigenschaften und ohne das Kopieren des Prototyps), ähnlich wie [beim Kopieren eines Arrays](#ein_array_kopieren).

```js
const clonedObj = { ...obj1 };
// { foo: "bar", x: 42 }
```

#### Überschreiben von Eigenschaften

Wenn ein Objekt in ein anderes Objekt gespreadet wird oder wenn mehrere Objekte in ein Objekt gespreadet werden, und Eigenschaften mit identischen Namen auftreten, erhält die Eigenschaft den zuletzt zugewiesenen Wert, während die Position erhalten bleibt, an der sie ursprünglich festgelegt wurde.

```js
const obj1 = { foo: "bar", x: 42 };
const obj2 = { foo: "baz", y: 13 };

const mergedObj = { x: 41, ...obj1, ...obj2, y: 9 }; // { x: 42, foo: "baz", y: 9 }
```

#### Bedingtes Hinzufügen von Eigenschaften zu einem Objekt

Sie können ein Element in einem Objektliteral präsent oder abwesend machen, abhängig von einer Bedingung, mit einem [bedingten Operator](/de/docs/Web/JavaScript/Reference/Operators/Conditional_operator).

```js
const isSummer = false;
const fruits = {
  apple: 10,
  banana: 5,
  ...(isSummer ? { watermelon: 30 } : {}),
};
// { apple: 10, banana: 5 }
```

Der Fall, wenn die Bedingung `false` ist, ist ein leeres Objekt, sodass nichts in das endgültige Objekt gespreadet wird. Beachten Sie, dass dies anders ist als folgendes:

```js
const fruits = {
  apple: 10,
  banana: 5,
  watermelon: isSummer ? 30 : undefined,
};
// { apple: 10, banana: 5, watermelon: undefined }
```

In diesem Fall ist die `watermelon`-Eigenschaft immer vorhanden und wird von Methoden wie {{jsxref("Object.keys()")}} besucht.

Weil Primitiven ebenfalls in Objekte gespreadet werden können und aus der Beobachtung, dass alle {{Glossary("falsy", "falsy")}} Werte keine aufzählbaren Eigenschaften haben, können Sie einfach einen [logischen UND](/de/docs/Web/JavaScript/Reference/Operators/Logical_AND) Operator verwenden:

```js
const isSummer = false;
const fruits = {
  apple: 10,
  banana: 5,
  ...(isSummer && { watermelon: 30 }),
};
```

In diesem Fall wird keine Eigenschaft auf dem `fruits`-Objekt erstellt, wenn `isSummer` ein beliebiger falsy Wert ist.

#### Vergleich mit Object.assign()

Beachten Sie, dass {{jsxref("Object.assign()")}} verwendet werden kann, um ein Objekt zu verändern, während die Spread-Syntaxus dies nicht kann.

```js
const obj1 = { foo: "bar", x: 42 };
Object.assign(obj1, { x: 1337 });
console.log(obj1); // { foo: "bar", x: 1337 }
```

Außerdem löst {{jsxref("Object.assign()")}} Setter auf dem Zielobjekt aus, während die Spread-Syntaxus dies nicht tut.

```js
const objectAssign = Object.assign(
  {
    set foo(val) {
      console.log(val);
    },
  },
  { foo: 1 },
);
// Logs "1"; objectAssign.foo is still the original setter

const spread = {
  set foo(val) {
    console.log(val);
  },
  ...{ foo: 1 },
};
// Nothing is logged; spread.foo is 1
```

Sie können die {{jsxref("Object.assign()")}} Funktion nicht naiv durch ein einfaches Spread-Implementierung nachbilden:

```js
const obj1 = { foo: "bar", x: 42 };
const obj2 = { foo: "baz", y: 13 };
const merge = (...objects) => ({ ...objects });

const mergedObj1 = merge(obj1, obj2);
// { 0: { foo: 'bar', x: 42 }, 1: { foo: 'baz', y: 13 } }

const mergedObj2 = merge({}, obj1, obj2);
// { 0: {}, 1: { foo: 'bar', x: 42 }, 2: { foo: 'baz', y: 13 } }
```

Im obigen Beispiel funktioniert die Spread-Syntaxus nicht wie erwartet: Sie spreadet ein _Array_ von Argumenten in das Objektliteral, aufgrund des Rest-Parameters. Hier ist eine Implementierung von `merge` mit der Spread-Syntaxus, deren Verhalten ähnlich ist wie {{jsxref("Object.assign()")}}, außer dass sie keine Setter auslöst, noch Objekte verändert:

```js
const obj1 = { foo: "bar", x: 42 };
const obj2 = { foo: "baz", y: 13 };
const merge = (...objects) =>
  objects.reduce((acc, cur) => ({ ...acc, ...cur }));

const mergedObj1 = merge(obj1, obj2);
// { foo: 'baz', x: 42, y: 13 }
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Rest-Parameter](/de/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Rest-Eigenschaft](/de/docs/Web/JavaScript/Reference/Operators/Destructuring#rest_property)
- {{jsxref("Function.prototype.apply()")}}
