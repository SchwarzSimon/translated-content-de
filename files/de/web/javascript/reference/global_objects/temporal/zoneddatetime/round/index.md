---
title: Temporal.ZonedDateTime.prototype.round()
slug: Web/JavaScript/Reference/Global_Objects/Temporal/ZonedDateTime/round
l10n:
  sourceCommit: d0b9cef0713eb263934a98e94202b97c143204a4
---

{{JSRef}}{{SeeCompatTable}}

Die **`round()`**-Methode von {{jsxref("Temporal.ZonedDateTime")}}-Instanzen gibt ein neues `Temporal.ZonedDateTime`-Objekt zurück, das diesen Datum-Zeit-Wert auf die angegebene Einheit gerundet darstellt.

## Syntax

```js-nolint
round(smallestUnit)
round(options)
```

### Parameter

- `smallestUnit`
  - : Ein String, der die [`smallestUnit`](#smallestunit_2)-Option darstellt. Dies ist eine Komfortüberladung, sodass `round(smallestUnit)` gleichbedeutend mit `round({ smallestUnit })` ist, wobei `smallestUnit` ein String ist.
- `options`
  - : Ein Objekt, das einige oder alle der folgenden Eigenschaften enthält (in der Reihenfolge, in der sie abgerufen und validiert werden):
    - `roundingIncrement` {{optional_inline}}
      - : Eine Zahl (auf eine ganze Zahl gerundet), die den Rundungsinkrement in der angegebenen `smallestUnit` darstellt. Standard ist `1`. Für alle Werte von `smallestUnit` außer `"day"` muss der Inkrement ein Teiler des maximalen Werts der Einheit sein; zum Beispiel, wenn die Einheit Stunden ist, muss der Inkrement ein Teiler von 24 sein und darf nicht 24 selbst sein, was bedeutet, dass er 1, 2, 3, 4, 6, 8 oder 12 sein kann. Für `"day"` muss der Inkrement 1 sein.
    - `roundingMode` {{optional_inline}}
      - : Ein String, der angibt, wie der Bruchteil der `smallestUnit` gerundet werden soll. Siehe [`Intl.NumberFormat()`](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat#roundingmode). Standard ist `"halfExpand"`.
    - `smallestUnit`
      - : Ein String, der die kleinste Einheit darstellt, die im Ergebnis enthalten sein soll. Der Wert muss einer der folgenden sein: `"day"`, `"hour"`, `"minute"`, `"second"`, `"millisecond"`, `"microsecond"`, `"nanosecond"` oder deren Pluralformen. Für Einheiten größer als `"nanosecond"` werden Bruchteile der `smallestUnit` gemäß den Einstellungen `roundingIncrement` und `roundingMode` gerundet.

### Rückgabewert

Ein neues {{jsxref("Temporal.ZonedDateTime")}}-Objekt, das diesen Datum-Zeit-Wert gerundet auf die angegebene Einheit darstellt, wobei alle Einheiten kleiner als `smallestUnit` auf null gesetzt sind.

Wenn `smallestUnit` `"day"` ist, wird der zurückgegebene Datum-Zeit-Wert der [Beginn des Tages](/de/docs/Web/JavaScript/Reference/Global_Objects/Temporal/ZonedDateTime/startOfDay) dieses Datums oder des nächsten Tages sein, abhängig vom `roundingMode` und der Entfernung zu diesen beiden Zeitpunkten. Andernfalls wird das Runden zuerst auf seinem `PlainDateTime` durchgeführt (gleich {{jsxref("Temporal/PlainDateTime/round", "Temporal.PlainDateTime.prototype.round()")}}) und dann in der gleichen Zeitzone neu interpretiert, mit `disambiguation: "compatible", offset: "prefer"`. Siehe [Mehrdeutigkeit und Lücken von lokaler Zeit zu UTC-Zeit](/de/docs/Web/JavaScript/Reference/Global_Objects/Temporal/ZonedDateTime#ambiguity_and_gaps_from_local_time_to_utc_time) und [Offset-Mehrdeutigkeit](/de/docs/Web/JavaScript/Reference/Global_Objects/Temporal/ZonedDateTime#offset_ambiguity).

### Ausnahmen

- {{jsxref("RangeError")}}
  - : Wird ausgelöst, wenn eine der Optionen ungültig ist.

## Beispiele

### Kleine Einheiten runden

```js
const zdt = Temporal.ZonedDateTime.from(
  "2021-07-01T12:34:56.123456789[America/New_York]",
);
const nearestMillisecond = zdt.round("millisecond");
console.log(nearestMillisecond.toString()); // 2021-07-01T12:34:56.123-04:00[America/New_York]

const nearestHalfHour = zdt.round({
  smallestUnit: "minute",
  roundingIncrement: 30,
});
console.log(nearestHalfHour.toString()); // 2021-07-01T12:30:00-04:00[America/New_York]

const nextDay = zdt.round({ smallestUnit: "day", roundingMode: "ceil" });
console.log(nextDay.toString()); // 2021-07-02T00:00:00-04:00[America/New_York]
```

### Mehrdeutigkeit nach dem Runden

Es ist möglich, dass der gerundete Datum-Zeit-Wert in der angegebenen Zeitzone mehrdeutig ist. Die Mehrdeutigkeit wird immer mit `disambiguation: "compatible", offset: "prefer"` aufgelöst. Hier ist ein schnelles Beispiel:

```js
const zdt = Temporal.ZonedDateTime.from(
  "2024-03-10T01:00:00-05:00[America/New_York]",
);
const rounded = zdt.round({ smallestUnit: "hour", roundingIncrement: 2 });
// The result is supposed to be 2024-03-10T02:00:00-05:00[America/New_York],
// but this time does not exist. `disambiguation: "compatible"` tells us to move
// forward by 1 hour.
console.log(rounded.toString()); // 2024-03-10T03:00:00-04:00[America/New_York]
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{jsxref("Temporal.ZonedDateTime")}}
