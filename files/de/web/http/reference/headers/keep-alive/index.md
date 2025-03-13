---
title: Keep-Alive
slug: Web/HTTP/Reference/Headers/Keep-Alive
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{HTTPSidebar}}

Der HTTP-**`Keep-Alive`** {{Glossary("request_header", "Anforderungs-")}} und {{Glossary("response_header", "Antwortheader")}} erlaubt es dem Sender, Hinweise zu geben, wie eine Verbindung hinsichtlich eines Zeitlimits und einer maximalen Anzahl von Anfragen verwendet werden kann.

> [!NOTE]
> Damit `Keep-Alive` eine Wirkung hat, muss die Nachricht auch einen {{HTTPHeader("Connection", "Connection: keep-alive")}} Header enthalten.

HTTP/1.0 schließt die Verbindung standardmäßig nach jeder Anforderungs-/Antwortinteraktion, sodass für persistente Verbindungen in HTTP/1.0 eine explizite Aushandlung erforderlich ist.
Einige Clients und Server möchten möglicherweise mit früheren Ansätzen für persistente Verbindungen kompatibel sein und können dies durch einen `Connection: keep-alive` Anforderungsheader tun.
Zusätzliche Parameter für die Verbindung können mit dem `Keep-Alive` Header angefordert werden.

> [!WARNING]
> Verbindungsspezifische Headerfelder wie {{HTTPHeader("Connection")}} und `Keep-Alive` sind in [HTTP/2](https://httpwg.org/specs/rfc9113.html#ConnectionSpecific) und [HTTP/3](https://httpwg.org/specs/rfc9114.html#header-formatting) verboten.
> Chrome und Firefox ignorieren sie in HTTP/2-Antworten, aber Safari entspricht den Anforderungen der HTTP/2-Spezifikation und lädt keine Antwort, die sie enthält.

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Header-Typ</th>
      <td>
        {{Glossary("Request_header", "Anforderungsheader")}},
        {{Glossary("Response_header", "Antwortheader")}}
      </td>
    </tr>
    <tr>
      <th scope="row">{{Glossary("Forbidden_request_header", "Verbotener Anforderungsheader")}}</th>
      <td>Ja</td>
    </tr>
  </tbody>
</table>

## Syntax

```http
Keep-Alive: <parameters>
```

## Direktiven

- `<parameters>`
  - : Eine kommagetrennte Liste von Parametern, die jeweils aus einem Bezeichner und einem Wert bestehen, die durch das Gleichheitszeichen (`=`) getrennt sind.
    Die folgenden Bezeichner sind möglich:
    - `timeout`
      - : Eine ganze Zahl, die die Zeit in Sekunden angibt, die der Host eine inaktive Verbindung geöffnet lässt, bevor sie geschlossen wird.
        Eine Verbindung ist inaktiv, wenn weder Daten gesendet noch empfangen werden. Ein Host kann eine inaktive Verbindung länger als die `timeout` Sekunden offen halten, aber der Host sollte versuchen, eine Verbindung für mindestens die `timeout` Sekunden aufrechtzuerhalten.
    - `max`
      - : Eine ganze Zahl, die die maximale Anzahl von Anfragen angibt, die bei dieser Verbindung gesendet werden können, bevor sie geschlossen wird.
        Außer `0` wird dieser Wert für nicht-übertragene Verbindungen ignoriert, da eine andere Anfrage in der nächsten Antwort gesendet wird.
        Eine HTTP-Pipeline kann ihn verwenden, um das Pipelining zu begrenzen.

## Beispiele

Eine Antwort, die einen `Keep-Alive` Header enthält:

```http
HTTP/1.1 200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Thu, 11 Aug 2016 15:23:13 GMT
Keep-Alive: timeout=5, max=200
Last-Modified: Mon, 25 Jul 2016 04:32:39 GMT
Server: Apache

(body)
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{HTTPHeader("Connection")}}
- [Verwaltung von Verbindungen in HTTP/1.x](/de/docs/Web/HTTP/Guides/Connection_management_in_HTTP_1.x)
