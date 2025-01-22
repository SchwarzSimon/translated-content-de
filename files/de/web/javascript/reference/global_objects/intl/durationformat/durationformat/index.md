---
title: Intl.DurationFormat() Konstruktor
slug: Web/JavaScript/Reference/Global_Objects/Intl/DurationFormat/DurationFormat
l10n:
  sourceCommit: 537aeae8ea6f3f080941261af7229dba30f791ac
---

{{JSRef}}

Der **`Intl.DurationFormat()`** Konstruktor erstellt {{jsxref("Intl.DurationFormat")}} Objekte.

## Syntax

```js-nolint
new Intl.DurationFormat()
new Intl.DurationFormat(locales)
new Intl.DurationFormat(locales, options)
```

> **Hinweis:** `Intl.DurationFormat()` kann nur mit [`new`](/de/docs/Web/JavaScript/Reference/Operators/new) konstruiert werden. Der Versuch, es ohne `new` aufzurufen, wirft einen {{jsxref("TypeError")}}.

### Parameter

- `locales` {{optional_inline}}

  - : Ein String mit einem BCP 47 Sprach-Tag oder eine {{jsxref("Intl.Locale")}} Instanz, oder ein Array solcher Locale-Identifikatoren. Die Standard-Locale der Laufzeitumgebung wird verwendet, wenn `undefined` übergeben wird oder wenn keiner der angegebenen Locale-Identifikatoren unterstützt wird. Für die allgemeine Form und Interpretation des `locales` Arguments siehe [die Parameterbeschreibung auf der Hauptseite von `Intl`](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl#locales_argument).

    Der folgende Unicode-Erweiterungsschlüssel ist erlaubt:

    - `nu`
      - : Siehe [`numberingSystem`](#numberingsystem).

    Dieser Schlüssel kann auch mit `options` (wie unten aufgeführt) gesetzt werden. Wenn beide gesetzt sind, hat die Eigenschaft `options` Vorrang.

- `options` {{optional_inline}}

  - : Ein Objekt, das die folgenden Eigenschaften enthält, in der Reihenfolge, in der sie abgerufen werden (alle sind optional):

    - `localeMatcher`
      - : Der Locale-Abgleichsalgorithmus, der verwendet werden soll. Mögliche Werte sind `"lookup"` und `"best fit"`; der Standard ist `"best fit"`. Für Informationen über diese Option siehe [Locale-Identifikation und -Verhandlung](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl#locale_identification_and_negotiation).
    - `numberingSystem`
      - : Das Nummerierungssystem, das für die Zahlenformatierung verwendet werden soll, wie `"arab"`, `"hans"`, `"mathsans"`, usw. Für eine Liste der unterstützten Nummerierungssystemtypen siehe [`Intl.supportedValuesOf()`](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl/supportedValuesOf#supported_numbering_system_types). Diese Option kann auch durch den `nu` Unicode-Erweiterungsschlüssel gesetzt werden; wenn beide angegeben sind, hat diese `options` Eigenschaft Vorrang.
    - `style`
      - : Der Stil der formatierten Dauer. Dieser Wert wird als Standard für alle anderen Einheitsoptionen verwendet und entspricht auch der `style` Option von {{jsxref("Intl/ListFormat/ListFormat", "Intl.ListFormat()")}} beim Zusammenfügen der Liste von Dauer-Einheiten. Mögliche Werte sind:
        - `"long"`
          - : Z.B., 1 hour and 50 minutes
        - `"short"` (standardmäßig)
          - : Z.B., 1 hr, 50 min
        - `"narrow"`
          - : Z.B., 1h 50m
        - `"digital"`
          - : Z.B., 1:50:00
    - `years`
      - : Der Stil der formatierten Jahre. Mögliche Werte sind `"long"`, `"short"`, und `"narrow"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"short"` sonst.
    - `yearsDisplay`
      - : Ob immer Jahre angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `years` nicht angegeben ist, und `"always"` sonst.
    - `months`
      - : Der Stil der formatierten Monate. Mögliche Werte sind `"long"`, `"short"`, und `"narrow"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"short"` sonst.
    - `monthsDisplay`
      - : Ob immer Monate angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `months` nicht angegeben ist, und `"always"` sonst.
    - `weeks`
      - : Der Stil der formatierten Wochen. Mögliche Werte sind `"long"`, `"short"`, und `"narrow"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"short"` sonst.
    - `weeksDisplay`
      - : Ob immer Wochen angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `weeks` nicht angegeben ist, und `"always"` sonst.
    - `days`
      - : Der Stil der formatierten Tage. Mögliche Werte sind `"long"`, `"short"`, und `"narrow"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"short"` sonst.
    - `daysDisplay`
      - : Ob immer Tage angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `days` nicht angegeben ist, und `"always"` sonst.
    - `hours`
      - : Der Stil der formatierten Stunden. Mögliche Werte sind `"long"`, `"short"`, `"narrow"`, `"numeric"`, und `"2-digit"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"numeric"` sonst.
    - `hoursDisplay`
      - : Ob immer Stunden angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `hours` nicht angegeben ist und `options.style` nicht `"digital"` ist, und `"always"` sonst.
    - `minutes`
      - : Der Stil der formatierten Minuten.
        - Wenn `hours` `"numeric"` oder `"2-digit"` ist, sind mögliche Werte `"numeric"` und `"2-digit"`, und `"numeric"` wird zu `"2-digit"` normalisiert; der Standard ist `"numeric"`.
        - Ansonsten sind mögliche Werte `"long"`, `"short"`, `"narrow"`, `"numeric"`, und `"2-digit"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"numeric"` sonst.
    - `minutesDisplay`
      - : Ob immer Minuten angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `minutes` nicht angegeben ist und `options.style` nicht `"digital"` ist, und `"always"` sonst.
    - `seconds`
      - : Der Stil der formatierten Sekunden.
        - Wenn `minutes` `"numeric"` oder `"2-digit"` ist, sind mögliche Werte `"numeric"` und `"2-digit"`, und `"numeric"` wird zu `"2-digit"` normalisiert; der Standard ist `"numeric"`.
        - Ansonsten sind mögliche Werte `"long"`, `"short"`, `"narrow"`, `"numeric"`, und `"2-digit"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"numeric"` sonst.
    - `secondsDisplay`
      - : Ob immer Sekunden angezeigt werden sollen, oder nur wenn sie ungleich null sind. Mögliche Werte sind `"always"` und `"auto"`; der Standard ist `"auto"` wenn `seconds` nicht angegeben ist und `options.style` nicht `"digital"` ist, und `"always"` sonst.
    - `milliseconds`
      - : Der Stil der formatierten Millisekunden.
        - Wenn `seconds` `"numeric"` oder `"2-digit"` ist, ist der einzige mögliche Wert `"numeric"`; der Standard ist `"numeric"`.
        - Ansonsten sind mögliche Werte `"long"`, `"short"`, `"narrow"`, und `"numeric"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"numeric"` sonst.
    - `millisecondsDisplay`
      - : Ob immer Millisekunden angezeigt werden sollen, oder nur wenn sie ungleich null sind.
        - Wenn `seconds` `"numeric"` oder `"2-digit"` ist, ist der einzige mögliche Wert `"auto"`; der Standard ist nur `"auto"` wenn `milliseconds` nicht angegeben ist.
        - Ansonsten sind mögliche Werte `"always"` und `"auto"`; der Standard ist `"auto"` wenn `milliseconds` nicht angegeben ist, und `"always"` sonst.
    - `microseconds`
      - : Der Stil der formatierten Mikrosekunden.
        - Wenn `milliseconds` `"numeric"` ist, ist der einzige mögliche Wert `"numeric"`; der Standard ist `"numeric"`.
        - Ansonsten sind mögliche Werte `"long"`, `"short"`, `"narrow"`, und `"numeric"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"numeric"` sonst.
    - `microsecondsDisplay`
      - : Ob immer Mikrosekunden angezeigt werden sollen, oder nur wenn sie ungleich null sind.
        - Wenn `milliseconds` `"numeric"` ist, ist der einzige mögliche Wert `"auto"`; der Standard ist nur `"auto"` wenn `microseconds` nicht angegeben ist.
        - Ansonsten sind mögliche Werte `"always"` und `"auto"`; der Standard ist `"auto"` wenn `microseconds` nicht angegeben ist, und `"always"` sonst.
    - `nanoseconds`
      - : Der Stil der formatierten Nanosekunden.
        - Wenn `microseconds` `"numeric"` ist, ist der einzige mögliche Wert `"numeric"`; der Standard ist `"numeric"`.
        - Ansonsten sind mögliche Werte `"long"`, `"short"`, `"narrow"`, und `"numeric"`; der Standard ist `options.style` wenn es nicht `"digital"` ist, und `"numeric"` sonst.
    - `nanosecondsDisplay`
      - : Ob immer Nanosekunden angezeigt werden sollen, oder nur wenn sie ungleich null sind.
        - Wenn `microseconds` `"numeric"` ist, ist der einzige mögliche Wert `"auto"`; der Standard ist nur `"auto"` wenn `nanoseconds` nicht angegeben ist.
        - Ansonsten sind mögliche Werte `"always"` und `"auto"`; der Standard ist `"auto"` wenn `nanoseconds` nicht angegeben ist, und `"always"` sonst.
    - `fractionalDigits`
      - : Anzahl der anzuzeigenden Sekundenbruchteile im Ausgabewert. Mögliche Werte sind von `0` bis `9`; der Standard ist `undefined` (einbeziehen so vieler Bruchteile wie nötig).

### Ausnahmen

- {{jsxref("RangeError")}}
  - : Wird ausgelöst, wenn `locales` oder `options` ungültige Werte enthalten.

## Beschreibung

Für jedes Zeitsegment wird im Hintergrund ein {{jsxref("Intl.NumberFormat")}} Objekt konstruiert. Es verwendet die folgenden Optionen (siehe {{jsxref("Intl/NumberFormat/NumberFormat", "Intl.NumberFormat()")}} für Details):

- `numberingSystem`: der Wert von `options.numberingSystem`

Wenn `milliseconds`, `microseconds` oder `nanoseconds` den `"numeric"` Stil verwenden, werden folgende Optionen ebenfalls verwendet:

- `minimumFractionDigits`: `0` wenn `options.fractionalDigits` `undefined` ist, `options.fractionalDigits` sonst
- `maximumFractionDigits`: `9` wenn `options.fractionalDigits` `undefined` ist, `options.fractionalDigits` sonst
- `roundingMode`: `"trunc"`

Wenn das Zeitsegment den `"2-digit"` Stil verwendet, werden folgende Optionen ebenfalls verwendet:

- `minimumIntegerDigits`: `2`

Wenn das Zeitsegment den `"long"`, `"short"`, oder `"narrow"` Stil verwendet, werden folgende Optionen ebenfalls verwendet:

- `style`: `"unit"` wenn `"long"`, `"short"`, oder `"narrow"` angegeben ist, `undefined` sonst
- `unit`: die momentan formatierte Einheit (`"years"`, `"days"`, `"nanoseconds"`, etc.)
- `unitDisplay`: der Wert des Zeitsegmentstils (`"long"`, `"short"`, oder `"narrow"`)

## Beispiele

### Verwendung des Intl.DurationFormat() Konstruktors

```js
const duration = {
  hours: 2,
  minutes: 20,
  seconds: 35,
};

console.log(new Intl.DurationFormat("pt", { style: "long" }).format(duration));
// "2 horas, 20 minutos e 35 segundos"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{jsxref("Intl.DurationFormat")}}
- {{jsxref("Intl.supportedValuesOf()")}}
- {{jsxref("Intl")}}
