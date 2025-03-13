---
title: LinearAccelerationSensor
slug: Web/API/LinearAccelerationSensor
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{securecontext_header}}{{APIRef("Sensor API")}}

Das **`LinearAccelerationSensor`**-Interface der [Sensor-APIs](/de/docs/Web/API/Sensor_APIs) liefert bei jeder Ablesung die auf das Gerät wirkende Beschleunigung entlang aller drei Achsen, jedoch ohne den Beitrag der Schwerkraft.

Um diesen Sensor zu verwenden, muss der Benutzer die Erlaubnis für den `'accelerometer'` Gerätesensor über die [Permissions API](/de/docs/Web/API/Permissions_API) erteilen. Zusätzlich kann diese Funktion durch eine auf Ihrem Server gesetzte [Permissions Policy](/de/docs/Web/HTTP/Guides/Permissions_Policy) blockiert werden.

{{InheritanceDiagram}}

## Konstruktor

- [`LinearAccelerationSensor()`](/de/docs/Web/API/LinearAccelerationSensor/LinearAccelerationSensor)
  - : Erstellt ein neues `LinearAccelerationSensor`-Objekt.

## Instanz-Eigenschaften

_Erbt Eigenschaften von seinen Vorfahren, [`Accelerometer`](/de/docs/Web/API/Accelerometer), [`Sensor`](/de/docs/Web/API/Sensor) und [`EventTarget`](/de/docs/Web/API/EventTarget)._

## Instanz-Methoden

_`LinearAccelerationSensor` hat keine eigenen Methoden. Es erbt jedoch Methoden von seinen übergeordneten Schnittstellen, [`Sensor`](/de/docs/Web/API/Sensor) und [`EventTarget`](/de/docs/Web/API/EventTarget)._

## Ereignisse

_`LinearAccelerationSensor` hat keine eigenen Ereignisse. Es erbt jedoch Ereignisse von seiner übergeordneten Schnittstelle, [`Sensor`](/de/docs/Web/API/Sensor)._

## Beispiel

Die lineare Beschleunigung wird typischerweise im [`reading`](/de/docs/Web/API/Sensor/reading_event) Ereignis-Callback abgelesen. Im untenstehenden Beispiel geschieht dies sechzig Mal pro Sekunde.

```js
let laSensor = new LinearAccelerationSensor({ frequency: 60 });

laSensor.addEventListener("reading", (e) => {
  console.log(`Linear acceleration along the X-axis ${laSensor.x}`);
  console.log(`Linear acceleration along the Y-axis ${laSensor.y}`);
  console.log(`Linear acceleration along the Z-axis ${laSensor.z}`);
});
laSensor.start();
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
