---
title: Function.prototype.call()
slug: Web/JavaScript/Reference/Global_Objects/Function/call
l10n:
  sourceCommit: 9645d14f12d9b93da98daaf25a443bb6cac3f2a6
---

{{JSRef}}

Die **`call()`**-Methode von {{jsxref("Function")}}-Instanzen ruft diese Funktion mit einem gegebenen `this`-Wert und einzeln angegebenen Argumenten auf.

{{InteractiveExample("JavaScript Demo: Function.prototype.call()")}}

```js interactive-example
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = "food";
}

console.log(new Food("cheese", 5).name);
// Expected output: "cheese"
```

## Syntax

```js-nolint
call(thisArg)
call(thisArg, arg1)
call(thisArg, arg1, arg2)
call(thisArg, arg1, arg2, /* …, */ argN)
```

### Parameter

- `thisArg`
  - : Der Wert, der als `this` beim Aufruf von `func` verwendet wird. Wenn die Funktion nicht im [Strict-Modus](/de/docs/Web/JavaScript/Reference/Strict_mode) ist, werden [`null`](/de/docs/Web/JavaScript/Reference/Operators/null) und [`undefined`](/de/docs/Web/JavaScript/Reference/Global_Objects/undefined) durch das globale Objekt ersetzt, und primitive Werte werden in Objekte umgewandelt.
- `arg1`, …, `argN` {{optional_inline}}
  - : Argumente für die Funktion.

### Rückgabewert

Das Ergebnis des Aufrufs der Funktion mit dem angegebenen `this`-Wert und den Argumenten.

## Beschreibung

> [!NOTE]
> Diese Funktion ist nahezu identisch mit {{jsxref("Function/apply", "apply()")}}, außer dass die Funktionsargumente an `call()` einzeln als Liste übergeben werden, während sie bei `apply()` in einem Objekt, typischerweise einem Array, kombiniert werden — zum Beispiel, `func.call(this, "eat", "bananas")` vs. `func.apply(this, ["eat", "bananas"])`.

Normalerweise ist beim Aufruf einer Funktion der Wert von [`this`](/de/docs/Web/JavaScript/Reference/Operators/this) innerhalb der Funktion das Objekt, auf dem die Funktion aufgerufen wurde. Mit `call()` können Sie beim Aufruf einer bestehenden Funktion einen beliebigen Wert als `this` zuweisen, ohne die Funktion zuerst als Eigenschaft an das Objekt anzubinden. Dies erlaubt es, Methoden eines Objekts als allgemeine Dienstprogrammfunktionen zu verwenden.

> [!WARNING]
> Verwenden Sie `call()` nicht, um Konstruktoren zu verkette (zum Beispiel zur Implementierung von Vererbung). Dies führt dazu, dass die Konstruktorfunktion als normale Funktion aufgerufen wird, was bedeutet, dass [`new.target`](/de/docs/Web/JavaScript/Reference/Operators/new.target) `undefined` ist, und Klassen werfen einen Fehler, weil sie nicht ohne [`new`](/de/docs/Web/JavaScript/Reference/Operators/new) aufgerufen werden können. Verwenden Sie stattdessen {{jsxref("Reflect.construct()")}} oder [`extends`](/de/docs/Web/JavaScript/Reference/Classes/extends).

## Beispiele

### Verwendung von call(), um eine Funktion aufzurufen und den this-Wert zu spezifizieren

Im folgenden Beispiel wird beim Aufruf von `greet` der Wert von `this` an das Objekt `obj` gebunden, auch wenn `greet` keine Methode von `obj` ist.

```js
function greet() {
  console.log(this.animal, "typically sleep between", this.sleepDuration);
}

const obj = {
  animal: "cats",
  sleepDuration: "12 and 16 hours",
};

greet.call(obj); // cats typically sleep between 12 and 16 hours
```

### Verwendung von call(), um eine Funktion aufzurufen, ohne das erste Argument anzugeben

Wenn der erste Parameter `thisArg` weggelassen wird, wird er standardmäßig auf `undefined` gesetzt. Im Nicht-Strict-Modus wird der `this`-Wert dann durch {{jsxref("globalThis")}} (was dem globalen Objekt ähnlich ist) ersetzt.

```js
globalThis.globProp = "Wisen";

function display() {
  console.log(`globProp value is ${this.globProp}`);
}

display.call(); // Logs "globProp value is Wisen"
```

Im Strict-Modus wird der Wert von `this` nicht ersetzt, sodass er `undefined` bleibt.

```js
"use strict";

globalThis.globProp = "Wisen";

function display() {
  console.log(`globProp value is ${this.globProp}`);
}

display.call(); // throws TypeError: Cannot read the property of 'globProp' of undefined
```

### Methoden in Dienstprogramme umwandeln

`call()` ist fast gleichbedeutend mit einem normalen Funktionsaufruf, außer dass `this` als normales Parameter übergeben wird, anstatt als Wert, auf dem die Funktion aufgerufen wurde. Dies ähnelt der Arbeitsweise von allgemeinen Dienstprogrammfunktionen: Anstatt `array.map(callback)` aufzurufen, verwenden Sie `map(array, callback)`, was es ermöglicht, `map` mit array-ähnlichen Objekten zu verwenden, die keine Arrays sind (zum Beispiel [`arguments`](/de/docs/Web/JavaScript/Reference/Functions/arguments)), ohne `Object.prototype` zu verändern.

Nehmen Sie zum Beispiel {{jsxref("Array.prototype.slice()")}}, das Sie verwenden möchten, um ein array-ähnliches Objekt in ein echtes Array zu konvertieren. Sie könnten eine Abkürzung wie diese erstellen:

```js
const slice = Array.prototype.slice;

// ...

slice.call(arguments);
```

Beachten Sie, dass Sie `slice.call` nicht speichern und als normale Funktion aufrufen können, da die `call()`-Methode auch ihren `this`-Wert liest, der die Funktion ist, die sie aufrufen soll. In diesem Fall können Sie {{jsxref("Function/bind", "bind()")}} verwenden, um den Wert von `this` für `call()` zu binden. Im folgenden Codebeispiel ist `slice()` eine gebundene Version von `Function.prototype.call()`, wobei der `this`-Wert an {{jsxref("Array.prototype.slice()")}} gebunden ist. Dies bedeutet, dass zusätzliche `call()`-Aufrufe eliminiert werden können:

```js
// Same as "slice" in the previous example
const unboundSlice = Array.prototype.slice;
const slice = Function.prototype.call.bind(unboundSlice);

// ...

slice(arguments);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{jsxref("Function.prototype.bind()")}}
- {{jsxref("Function.prototype.apply()")}}
- {{jsxref("Reflect.apply()")}}
- [Spread-Syntax (`...`)](/de/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Einführung in objektorientiertes JavaScript](/de/docs/Learn_web_development/Extensions/Advanced_JavaScript_objects)
