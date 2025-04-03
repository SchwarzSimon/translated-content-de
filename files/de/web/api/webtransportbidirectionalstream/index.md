---
title: WebTransportBidirectionalStream
slug: Web/API/WebTransportBidirectionalStream
l10n:
  sourceCommit: cc41ecd796870c2b6c77ad0b04fcb8d8c7d877d2
---

{{APIRef("WebTransport API")}}{{SecureContext_Header}} {{AvailableInWorkers}}

Das **`WebTransportBidirectionalStream`** Interface der [WebTransport API](/de/docs/Web/API/WebTransport_API) repräsentiert einen bidirektionalen Stream, der von einem Server oder Client erstellt wurde und für den zuverlässigen Transport verwendet werden kann. Es bietet Zugriff auf einen [`WebTransportReceiveStream`](/de/docs/Web/API/WebTransportReceiveStream) zum Lesen eingehender Daten und einen [`WebTransportSendStream`](/de/docs/Web/API/WebTransportSendStream) zum Schreiben ausgehender Daten.

{{InheritanceDiagram}}

## Instanzeigenschaften

- [`readable`](/de/docs/Web/API/WebTransportBidirectionalStream/readable) {{ReadOnlyInline}}
  - : Gibt eine Instanz von [`WebTransportReceiveStream`](/de/docs/Web/API/WebTransportReceiveStream) zurück, die zum Lesen eingehender Daten verwendet werden kann.
- [`writable`](/de/docs/Web/API/WebTransportBidirectionalStream/writable) {{ReadOnlyInline}}
  - : Gibt eine Instanz von [`WebTransportSendStream`](/de/docs/Web/API/WebTransportSendStream) zurück, die zum Schreiben ausgehender Daten verwendet werden kann.

## Beispiele

### Bidirektionale Übertragung, initiiert durch den User-Agent

Um einen bidirektionalen Stream von einem User-Agent zu öffnen, verwenden Sie die Methode [`WebTransport.createBidirectionalStream()`](/de/docs/Web/API/WebTransport/createBidirectionalStream), um eine Referenz zu einem `WebTransportBidirectionalStream` zu erhalten. Die Eigenschaften `readable` und `writable` geben Referenzen zu `WebTransportReceiveStream`- und `WebTransportSendStream`-Instanzen zurück.
Diese erben jeweils von `ReadableStream` und `WritableStream` und können verwendet werden, um vom Server zu lesen und an diesen zu schreiben.

```js
async function setUpBidirectional() {
  const stream = await transport.createBidirectionalStream();
  // stream is a WebTransportBidirectionalStream
  // stream.readable is a WebTransportReceiveStream
  const readable = stream.readable;
  // stream.writable is a WebTransportSendStream
  const writable = stream.writable;

  // …
}
```

Das Lesen vom `WebTransportReceiveStream` kann auf die gleiche Weise erfolgen wie das Lesen eines `ReadableStream`:

```js
async function readData(readable) {
  const reader = readable.getReader();
  while (true) {
    const { value, done } = await reader.read();
    if (done) {
      break;
    }
    // value is a Uint8Array.
    console.log(value);
  }
}
```

Und das Schreiben in den `WebTransportSendStream` kann folgendermaßen erfolgen:

```js
async function writeData(writable) {
  const writer = writable.getWriter();
  const data1 = new Uint8Array([65, 66, 67]);
  const data2 = new Uint8Array([68, 69, 70]);
  writer.write(data1);
  writer.write(data2);
}
```

### Bidirektionale Übertragung, initiiert durch den Server

Wenn der Server einen bidirektionalen Stream öffnet, um Daten an den Client zu übertragen und zu empfangen, kann darauf über die Eigenschaft [`WebTransport.incomingBidirectionalStreams`](/de/docs/Web/API/WebTransport/incomingBidirectionalStreams) zugegriffen werden, die einen [`ReadableStream`](/de/docs/Web/API/ReadableStream) von `WebTransportBidirectionalStream`-Objekten zurückgibt. Jeder dieser Streams kann verwendet werden, um {{jsxref("Uint8Array")}}-Instanzen zu lesen und zu schreiben, wie oben gezeigt. Allerdings benötigen Sie eine initiale Funktion, um den bidirektionalen Stream zu lesen:

```js
async function receiveBidirectional() {
  const bds = transport.incomingBidirectionalStreams;
  const reader = bds.getReader();
  while (true) {
    const { done, value } = await reader.read();
    if (done) {
      break;
    }
    // value is an instance of WebTransportBidirectionalStream
    await readData(value.readable);
    await writeData(value.writable);
  }
}
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Verwendung von WebTransport](https://developer.chrome.com/docs/capabilities/web-apis/webtransport)
- [WebSockets API](/de/docs/Web/API/WebSockets_API)
- [Streams API](/de/docs/Web/API/Streams_API)
- [WebTransport über HTTP/3](https://datatracker.ietf.org/doc/html/draft-ietf-webtrans-http3/)
