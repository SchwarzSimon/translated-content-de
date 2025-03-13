---
title: "Navigator: requestMIDIAccess() Methode"
short-title: requestMIDIAccess()
slug: Web/API/Navigator/requestMIDIAccess
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{APIRef("Web MIDI API")}}{{SecureContext_Header}}

Die **`requestMIDIAccess()`** Methode der [`Navigator`](/de/docs/Web/API/Navigator) Schnittstelle gibt ein {{jsxref('Promise')}} zurück, das eine Anfrage für den Zugriff auf MIDI-Geräte auf dem System eines Benutzers darstellt. Diese Methode ist Teil der [Web MIDI API](/de/docs/Web/API/Web_MIDI_API), die eine Möglichkeit zum Zugriff auf, Aufzählen und Manipulieren von MIDI-Geräten bietet.

Diese Methode kann den Benutzer um Zugang zu den auf seinem System verfügbaren MIDI-Geräten bitten oder eine zuvor festgelegte Präferenz verwenden, um den Zugang zu gewähren oder zu verweigern. Wenn die Erlaubnis erteilt wird, wird das {{jsxref('Promise')}} aufgelöst und ein [`MIDIAccess`](/de/docs/Web/API/MIDIAccess) Objekt zurückgegeben.

## Syntax

```js-nolint
requestMIDIAccess()
requestMIDIAccess(MIDIOptions)
```

### Parameter

- `MIDIOptions` {{optional_inline}}
  - : Ein {{jsxref('Object')}}, das Optionen darstellt, die in die Methode übergeben werden können. Diese Optionen sind:
    - `sysex`
      - : Ein {{jsxref('Boolean')}} Wert, der, wenn er auf `true` gesetzt ist, die Möglichkeit erlaubt, System Exclusive (sysex) Nachrichten zu senden und zu empfangen. Der Standardwert ist `false`.
    - `software`
      - : Ein {{jsxref('Boolean')}} Wert, der, wenn er auf `true` gesetzt ist, dem System ermöglicht, installierte Software-Synthesizer zu nutzen. Der Standardwert ist `false`.

### Rückgabewert

Ein {{jsxref('Promise')}} das mit einem [`MIDIAccess`](/de/docs/Web/API/MIDIAccess) Objekt aufgelöst wird.

### Ausnahmen

- `AbortError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn das Dokument oder die Seite aufgrund der Navigation des Benutzers geschlossen wird.
- `InvalidStateError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn das zugrunde liegende System Fehler meldet.
- `NotSupportedError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn die Funktion oder Optionen vom System nicht unterstützt werden.
- `SecurityError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn der Benutzer oder das System der Anwendung das Erstellen eines [MIDIAccess](/de/docs/Web/API/MIDIAccess) Objekts mit den angeforderten Optionen verweigert oder wenn das Dokument nicht berechtigt ist, die Funktion zu nutzen (zum Beispiel wegen einer [Berechtigungsrichtlinie](/de/docs/Web/HTTP/Guides/Permissions_Policy) oder weil der Benutzer zuvor eine Berechtigungsanfrage abgelehnt hat).

## Sicherheitsanforderungen

Der Zugriff auf die API unterliegt den folgenden Einschränkungen:

- Die Methode muss in einem [sicheren Kontext](/de/docs/Web/Security/Secure_Contexts) aufgerufen werden.
- Der Zugang kann durch die [`midi`](/de/docs/Web/HTTP/Reference/Headers/Permissions-Policy/midi) HTTP [Berechtigungsrichtlinie](/de/docs/Web/HTTP/Guides/Permissions_Policy) eingeschränkt sein.
- Der Benutzer muss der Nutzung der API ausdrücklich über einen benutzerspezifischen Mechanismus zustimmen oder bereits zuvor die Zustimmung erteilt haben. Beachten Sie, dass, wenn der Zugriff durch eine Berechtigungsrichtlinie verweigert wird, er nicht durch eine Benutzergenehmigung erteilt werden kann.

Der Berechtigungsstatus kann mit der [Permissions API](/de/docs/Web/API/Permissions_API) Methode [`navigator.permissions.query()`](/de/docs/Web/API/Permissions/query) abgefragt werden. Dabei wird ein Berechtigungsdeskriptor mit der `midi`-Berechtigung und (optional) der `sysex`-Eigenschaft übergeben:

```js
navigator.permissions.query({ name: "midi", sysex: true }).then((result) => {
  if (result.state === "granted") {
    // Access granted.
  } else if (result.state === "prompt") {
    // Using API will prompt for permission
  }
  // Permission was denied by user prompt or permission policy
});
```

## Beispiele

### MIDI-Zugang anfordern

Im folgenden Beispiel gibt die Methode `Navigator.requestMIDIAccess()` das [`MIDIAccess`](/de/docs/Web/API/MIDIAccess) Objekt zurück, das den Zugriff auf Informationen über die Eingabe- und Ausgabemöglichkeit von MIDI-Ports ermöglicht.

```js
navigator.requestMIDIAccess().then((access) => {
  // Get lists of available MIDI controllers
  const inputs = access.inputs.values();
  const outputs = access.outputs.values();
  // …
});
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Web MIDI API](/de/docs/Web/API/Web_MIDI_API)
- [Einführung in Web MIDI](https://code.tutsplus.com/introduction-to-web-midi--cms-25220t)
