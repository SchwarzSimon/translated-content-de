---
title: "PressureObserver: PressureObserver() Konstruktor"
short-title: PressureObserver()
slug: Web/API/PressureObserver/PressureObserver
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{APIRef("Compute Pressure API")}}{{SeeCompatTable}}{{AvailableInWorkers("window_and_worker_except_service")}}{{securecontext_header}}

Der **`PressureObserver()`** Konstruktor erstellt ein neues [`PressureObserver`](/de/docs/Web/API/PressureObserver) Objekt, um Änderungen des Drucks von Systemressourcen wie der CPU zu beobachten.

## Syntax

```js-nolint
new PressureObserver(callback)
```

### Parameter

- `callback`
  - : Ein Callback, das aufgerufen wird, wenn Druckaufzeichnungen beobachtet werden. Wenn das Callback aufgerufen wird, sind die folgenden Parameter verfügbar:
    - `changes`
      - : Ein Array, das alle [`PressureRecord`](/de/docs/Web/API/PressureRecord) Objekte enthält, die seit dem letzten Aufruf des Callbacks oder seit dem letzten Aufruf der [`takeRecords()`](/de/docs/Web/API/PressureObserver/takeRecords) Methode des Observers aufgezeichnet wurden.
    - `observer`
      - : Das [`observer`](/de/docs/Web/API/PressureObserver) Objekt, das die obigen Aufzeichnungen empfängt.

### Rückgabewert

Ein neues [`PressureObserver`](/de/docs/Web/API/PressureObserver) Objekt mit der angegebenen `callback` Funktion, die aufgerufen wird, wenn [`PressureObserver.observe()`](/de/docs/Web/API/PressureObserver/observe) aufgerufen wurde, um Druckänderungen zu beobachten.

### Ausnahmen

- `NotAllowedError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn die [Compute Pressure API](/de/docs/Web/API/Compute_Pressure_API) durch eine {{httpheader('Permissions-Policy/compute-pressure','compute-pressure')}} [Berechtigungsrichtlinie](/de/docs/Web/HTTP/Guides/Permissions_Policy) nicht erlaubt wird.

## Beispiele

### Aktuellen Druck protokollieren

Dieses Beispiel erstellt einen [`PressureObserver`](/de/docs/Web/API/PressureObserver) und führt eine Aktion aus, sobald sich der Druck ändert. Das Probenintervall ist auf 1000ms gesetzt, was bedeutet, dass es höchstens jede Sekunde Aktualisierungen gibt.

```js
function callback(records) {
  const lastRecord = records[records.length - 1];
  console.log(`Current pressure ${lastRecord.state}`);
  if (lastRecord.state === "critical") {
    // disable video feeds
  } else if (lastRecord.state === "serious") {
    // disable video filter effects
  } else {
    // enable all video feeds and filter effects
  }
}

try {
  const observer = new PressureObserver(callback);
  await observer.observe("cpu", {
    sampleInterval: 1000, // 1000ms
  });
} catch (error) {
  // report error setting up the observer
}
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}
