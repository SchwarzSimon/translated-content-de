---
title: 502 Bad Gateway
slug: Web/HTTP/Reference/Status/502
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{HTTPSidebar}}

Der HTTP-Statuscode **`502 Bad Gateway`** der [Serverfehlerantwort](/de/docs/Web/HTTP/Reference/Status#server_error_responses) zeigt an, dass ein Server als Gateway oder {{Glossary("Proxy_server", "Proxy")}} fungierte und eine ungültige Antwort vom Upstream-Server erhalten hat.

Diese Antwort ähnelt einer {{HTTPStatus("500", "500 Internal Server Error")}}-Antwort, da sie ein generisches "Catch-All" für Serverfehler darstellt. Der Unterschied besteht darin, dass sie spezifisch für den Punkt in der Anforderungskette ist, an dem der Fehler aufgetreten ist. Wenn der Ursprungsserver eine gültige HTTP-Fehlerantwort an das Gateway sendet, sollte die Antwort anstelle einer `502` an den Client weitergegeben werden, um den Grund für das Scheitern transparent zu machen. Wenn der Proxy oder das Gateway keine HTTP-Antwort vom Ursprungsserver erhalten hat, sendet es stattdessen eine {{HTTPStatus("504", "504 Gateway Timeout")}} an den Client.

Es gibt viele Ursachen für `502`-Fehler, und die Behebung solcher Probleme erfordert wahrscheinlich eine Untersuchung durch Serverbesitzer oder Administratoren. Ausnahmen sind Netzwerkfehler des Clients, insbesondere wenn der Dienst für andere Besucher funktioniert und wenn Clients VPNs oder andere benutzerdefinierte Netzwerkeinstellungen verwenden. In solchen Fällen sollten die Clients die Netzwerkeinstellungen, Firewall-Konfiguration, Proxy-Einstellungen, DNS-Konfiguration usw. überprüfen.

## Status

```http
502 Bad Gateway
```

## Beispiele

### 502 Gateway-Fehlerantwort

Die folgende Anfrage versucht, eine Webseite abzurufen, erhält jedoch eine `502`-Antwort zurück. Der Antwortinhalt enthält eine Seite, die den Serverzustand beschreibt, mit einem Link zu einer Support-Seite für Besucher.

```http
GET /highlights HTTP/1.1
Host: example.com
User-Agent: curl/8.6.0
Accept: */*
```

```http
HTTP/1.1 502 Bad Gateway
Content-Type: text/html;
Content-Length: 123

<!doctype html>
<html lang="en">
<head>
  <title>502 Bad Gateway</title>
</head>
<body>
  <h1>Bad Gateway</h1>
  <p>The server was unable to complete your request. Please try again later.</p>
  <p>If this problem persists, please <a href="https://example.com/support">contact support</a>.</p>
</body>
</html>
```

## Spezifikationen

{{Specifications}}

## Siehe auch

- [HTTP-Antwortstatuscodes](/de/docs/Web/HTTP/Reference/Status)
- {{HTTPStatus("504", "504 Gateway Timeout")}}
