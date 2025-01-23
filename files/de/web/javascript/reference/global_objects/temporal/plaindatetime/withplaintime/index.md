---
title: Temporal.PlainDateTime.prototype.withPlainTime()
slug: Web/JavaScript/Reference/Global_Objects/Temporal/PlainDateTime/withPlainTime
l10n:
  sourceCommit: d0b9cef0713eb263934a98e94202b97c143204a4
---

{{JSRef}}{{SeeCompatTable}}

Die **`withPlainTime()`** Methode der {{jsxref("Temporal.PlainDateTime")}} Instanzen gibt ein neues `Temporal.PlainDateTime` Objekt zurück, das diesen Datum-Zeit-Wert darstellt, wobei der Zeitanteil vollständig durch die neue Zeit ersetzt wird (in einer Form, die durch {{jsxref("Temporal/PlainTime/from", "Temporal.PlainTime.from()")}} konvertierbar ist).

Diese Methode wird alle Zeiteigenschaften ersetzen und standardmäßig auf `0` setzen, wenn Eigenschaften nicht angegeben sind. Wenn Sie nur einige der Zeiteigenschaften ersetzen möchten, verwenden Sie stattdessen die {{jsxref("Temporal/PlainDateTime/with", "with()")}} Methode.

## Syntax

```js-nolint
withPlainTime()
withPlainTime(plainTime)
```

### Parameter

- `plainTime` {{optional_inline}}
  - : Ein String, ein Objekt oder eine {{jsxref("Temporal.PlainTime")}} Instanz, die die neue Zeit darstellt. Es wird mit demselben Algorithmus wie {{jsxref("Temporal/PlainTime/from", "Temporal.PlainTime.from()")}} in ein `Temporal.PlainTime` Objekt konvertiert. Wenn nicht angegeben, wird der Zeitanteil auf `00:00:00` gesetzt.

### Rückgabewert

Ein neues `Temporal.PlainDateTime` Objekt, bei dem der Datumsanteil aus dem ursprünglichen Datum-Zeit-Wert kopiert und der Zeitanteil durch die neue Zeit ersetzt wird.

## Beispiele

### Verwendung von withPlainTime()

```js
const dt = Temporal.PlainDateTime.from("2021-07-01T12:34:56");

// You can pass a string
const newDT = dt.withPlainTime("13:45:00");
console.log(newDT.toString()); // "2021-07-01T13:45:00"

// You can only specify some time properties, and the rest default to 0;
// for the with() method, they would be copied from the original date-time
const newDT2 = dt.withPlainTime({ hour: 13 });
console.log(newDT2.toString()); // "2021-07-01T13:00:00"

// You can pass nothing to set the time to midnight
const newDT3 = dt.withPlainTime();
console.log(newDT3.toString()); // "2021-07-01T00:00:00"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{jsxref("Temporal.PlainDateTime")}}
- {{jsxref("Temporal/PlainDateTime/with", "Temporal.PlainDateTime.prototype.with()")}}
- {{jsxref("Temporal/PlainDateTime/withCalendar", "Temporal.PlainDateTime.prototype.withCalendar()")}}
- {{jsxref("Temporal/PlainDateTime/toPlainTime", "Temporal.PlainDateTime.prototype.toPlainTime()")}}
- {{jsxref("Temporal/PlainDateTime/from", "Temporal.PlainDateTime.from()")}}
