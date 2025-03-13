---
title: 100 Continue
slug: Web/HTTP/Reference/Status/100
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{HTTPSidebar}}

Der HTTP-Statuscode **`100 Continue`** für [informative Antworten](/de/docs/Web/HTTP/Reference/Status#informational_responses) zeigt an, dass der erste Teil einer Anfrage empfangen wurde und vom Server noch nicht abgelehnt wurde.
Der Client sollte mit einer Anfrage fortfahren oder die 100-Antwort verwerfen, wenn die Anfrage bereits abgeschlossen ist.

Wenn eine Anfrage einen {{HTTPHeader("Expect", "Expect: 100-continue")}} Header enthält, zeigt die 100 Continue-Antwort an, dass der Server bereit oder in der Lage ist, den Anforderungsinhalt zu empfangen.
Das Warten auf eine 100 Continue-Antwort kann hilfreich sein, wenn ein Client erwartet, dass ein Fehler wahrscheinlich ist, zum Beispiel beim Senden von zustandsändernden Operationen ohne zuvor verifizierte Authentifizierungsinformationen.

## Status

```http
100 Continue
```

## Beispiele

### PUT-Anfrage mit 100 Continue

Die folgende {{HTTPMethod("PUT")}} Anfrage sendet Informationen über einen Datei-Upload an einen Server.
Der Client gibt an, dass er mit dem Inhalt fortfahren wird, wenn er eine 100-Antwort erhält, um zu vermeiden, dass Daten über das Netzwerk gesendet werden, die zu einem Fehler wie {{HTTPStatus("405")}}, {{HTTPStatus("401")}} oder {{HTTPStatus("403")}} führen könnten.
Zuerst sendet der Client nur Header, einschließlich eines {{HTTPHeader("Expect", "Expect: 100-continue")}} Headers:

```http
PUT /videos HTTP/1.1
Host: uploads.example.com
Content-Type: video/h264
Content-Length: 123456789
Expect: 100-continue
```

Der Server zeigt an, dass die Anfrage fortgesetzt werden kann:

```http
HTTP/1.1 100 Continue
```

Der Client vervollständigt die Anfrage, indem er die tatsächlichen Daten sendet:

```http
[Video data as content for PUT request]
```

## Spezifikationen

{{Specifications}}

## Siehe auch

- {{HTTPHeader("Expect")}}
- {{HTTPStatus(417)}}
