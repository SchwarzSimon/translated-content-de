---
title: "NavigationCurrentEntryChangeEvent: NavigationCurrentEntryChangeEvent()-Konstruktor"
short-title: NavigationCurrentEntryChangeEvent()
slug: Web/API/NavigationCurrentEntryChangeEvent/NavigationCurrentEntryChangeEvent
l10n:
  sourceCommit: 1bd08bc0642029f650d2da7df5fd1baef09148ef
---

{{APIRef("Navigation API")}}{{SeeCompatTable}}

Der **`NavigationCurrentEntryChangeEvent()`**-Konstruktor erstellt ein neues [`NavigationCurrentEntryChangeEvent`](/de/docs/Web/API/NavigationCurrentEntryChangeEvent)-Objekt.

## Syntax

```js-nolint
new NavigationCurrentEntryChangeEvent(type, init)
```

### Parameter

- `type`
  - : Ein String, der den Typ des Ereignisses repräsentiert.
- `init`
  - : Ein Objekt, das _zusätzlich zu den Eigenschaften, die in [`Event()`](/de/docs/Web/API/Event/Event) definiert sind_, die folgenden Eigenschaften besitzt:
    - `from`
      - : Ein [`NavigationHistoryEntry`](/de/docs/Web/API/NavigationHistoryEntry)-Objekt, das den Ort repräsentiert, zu dem navigiert wird.
    - `navigationType` {{optional_inline}}
      - : Der Typ der Navigation, die zur Änderung geführt hat. Mögliche Werte sind `push`, `reload`, `replace` und `traverse`. Standardwert ist `null`.

### Rückgabewert

Ein neues [`NavigationCurrentEntryChangeEvent`](/de/docs/Web/API/NavigationCurrentEntryChangeEvent)-Objekt.

## Beispiele

Ein Entwickler würde diesen Konstruktor nicht manuell verwenden. Ein neues `NavigationCurrentEntryChangeEvent`-Objekt wird erstellt, wenn ein Handler aufgerufen wird, als Ergebnis des Abfeuerns des [`currententrychange`](/de/docs/Web/API/Navigation/currententrychange_event)-Ereignisses.

```js
navigation.addEventListener("currententrychange", (event) => {
  console.log(event.navigationType);
});
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Modernes clientseitiges Routing: die Navigation API](https://developer.chrome.com/docs/web-platform/navigation-api/)
- [Navigation API Erklärer](https://github.com/WICG/navigation-api/blob/main/README.md)
- Domenic Denicolas [Navigation API Live-Demo](https://gigantic-honored-octagon.glitch.me/)
