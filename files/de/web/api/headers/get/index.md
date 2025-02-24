---
title: "Headers: get() Methode"
short-title: get()
slug: Web/API/Headers/get
l10n:
  sourceCommit: 442db82028668b17b888ee439468ae2ac9d589a5
---

{{APIRef("Fetch API")}} {{AvailableInWorkers}}

Die **`get()`** Methode des [`Headers`](/de/docs/Web/API/Headers) Interfaces gibt einen Byte-String aller Werte eines Headers innerhalb eines `Headers` Objekts mit einem gegebenen Namen zurück. Wenn der angeforderte Header im `Headers` Objekt nicht existiert, wird `null` zurückgegeben.

Aus Sicherheitsgründen können einige Header nur vom User-Agent gesteuert werden. Diese Header umfassen die {{Glossary("Forbidden_request_header", "verbotenen Anfrage-Header")}} und die {{Glossary("Forbidden_response_header_name", "verbotenen Antwort-Header-Namen")}}.

## Syntax

```js-nolint
get(name)
```

### Parameter

- `name`
  - : Der Name des HTTP-Headers, dessen Werte Sie aus dem `Headers` Objekt abrufen möchten. Wenn der angegebene Name nicht der Name eines HTTP-Headers ist, wirft diese Methode einen {{jsxref("TypeError")}}. Der Name ist nicht case-sensitiv.

### Rückgabewert

Eine {{jsxref("String")}} Sequenz, die die Werte des abgerufenen Headers repräsentiert oder `null`, falls dieser Header nicht gesetzt ist.

## Beispiele

Ein leeres `Headers` Objekt zu erstellen, ist einfach:

```js
const myHeaders = new Headers(); // Currently empty
myHeaders.get("Not-Set"); // Returns null
```

Sie könnten einen Header hinzufügen, indem Sie [`Headers.append`](/de/docs/Web/API/Headers/append) verwenden und ihn dann mit `get()` abrufen:

```js
myHeaders.append("Content-Type", "image/jpeg");
myHeaders.get("Content-Type"); // Returns "image/jpeg"
```

Wenn der Header mehrere damit verbundene Werte hat, enthält der Byte-String alle Werte, in der Reihenfolge, in der sie dem Headers Objekt hinzugefügt wurden:

```js
myHeaders.append("Accept-Encoding", "deflate");
myHeaders.append("Accept-Encoding", "gzip");
myHeaders.get("Accept-Encoding"); // Returns "deflate, gzip"
myHeaders
  .get("Accept-Encoding")
  .split(",")
  .map((v) => v.trimStart()); // Returns [ "deflate", "gzip" ]
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [ServiceWorker API](/de/docs/Web/API/Service_Worker_API)
- [HTTP Zugriffskontrolle (CORS)](/de/docs/Web/HTTP/CORS)
- [HTTP](/de/docs/Web/HTTP)
