---
title: HTTP-Antwortstatuscodes
slug: Web/HTTP/Status
l10n:
  sourceCommit: bd4d7bc4176d9f67297e3940ae7163a258f07ef5
---

{{HTTPSidebar}}

HTTP-Antwortstatuscodes zeigen an, ob eine bestimmte [HTTP](/de/docs/Web/HTTP)-Anfrage erfolgreich abgeschlossen wurde. Antworten sind in fünf Kategorien gruppiert:

1. [Informationelle Antworten](#informationelle_antworten) (`100` – `199`)
2. [Erfolgreiche Antworten](#erfolgreiche_antworten) (`200` – `299`)
3. [Umleitungsnachrichten](#umleitungsnachrichten) (`300` – `399`)
4. [Client-Fehlerantworten](#client-fehlerantworten) (`400` – `499`)
5. [Server-Fehlerantworten](#server-fehlerantworten) (`500` – `599`)

Die unten aufgeführten Statuscodes sind in [RFC 9110](https://httpwg.org/specs/rfc9110.html#overview.of.status.codes) definiert.

> [!NOTE]
> Wenn Sie eine Antwort erhalten, die hier nicht aufgeführt ist, handelt es sich um eine nicht standardmäßige Antwort, möglicherweise individuell auf die Server-Software zugeschnitten.

## Informationelle Antworten

- {{HTTPStatus(100, "100 Continue")}}
  - : Diese vorläufige Antwort weist darauf hin, dass der Client die Anfrage fortsetzen oder die Antwort ignorieren sollte, wenn die Anfrage bereits abgeschlossen ist.
- {{HTTPStatus(101, "101 Switching Protocols")}}
  - : Dieser Code wird als Antwort auf einen {{HTTPHeader("Upgrade")}}-Anforderungs-Header vom Client gesendet und zeigt an, zu welchem Protokoll der Server wechselt.
- {{HTTPStatus(102, "102 Processing")}} {{deprecated_inline}}
  - : Dieser Code wurde in {{Glossary("WebDAV", "WebDAV")}}-Kontexten verwendet, um anzuzeigen, dass eine Anfrage vom Server empfangen wurde, aber zum Zeitpunkt der Antwort kein Status verfügbar war.
- {{HTTPStatus(103, "103 Early Hints")}}
  - : Dieser Statuscode ist hauptsächlich dafür vorgesehen, mit dem {{HTTPHeader("Link")}}-Header verwendet zu werden, um dem User Agent das [Preloading](/de/docs/Web/HTML/Attributes/rel/preload) von Ressourcen zu ermöglichen, während der Server eine Antwort vorbereitet oder eine [Preconnect](/de/docs/Web/HTML/Attributes/rel/preconnect) zu einer Quelle herstellt, von der die Seite Ressourcen benötigt.

## Erfolgreiche Antworten

- {{HTTPStatus(200, "200 OK")}}
  - : Die Anfrage war erfolgreich. Das Ergebnis und die Bedeutung von "Erfolg" hängen von der HTTP-Methode ab:
    - {{HTTPMethod("GET")}}: Die Ressource wurde abgerufen und im Nachrichtenkörper übertragen.
    - {{HTTPMethod("HEAD")}}: Repräsentations-Header sind in der Antwort enthalten, jedoch ohne Nachrichtenkörper.
    - {{HTTPMethod("PUT")}} oder {{HTTPMethod("POST")}}: Die Ressource, die das Ergebnis der Aktion beschreibt, wird im Nachrichtenkörper übertragen.
    - {{HTTPMethod("TRACE")}}: Der Nachrichtenkörper enthält die Anfrage, so wie sie vom Server empfangen wurde.
- {{HTTPStatus(201, "201 Created")}}
  - : Die Anfrage war erfolgreich und eine neue Ressource wurde als Ergebnis erstellt. Dies ist typischerweise die Antwort, die nach {{HTTPMethod("POST")}}-Anfragen oder einigen {{HTTPMethod("PUT")}}-Anfragen gesendet wird.
- {{HTTPStatus(202, "202 Accepted")}}
  - : Die Anfrage wurde empfangen, aber noch nicht bearbeitet.
    Es ist unverbindlich, da es in HTTP keine Möglichkeit gibt, später eine asynchrone Antwort zu senden, die das Ergebnis der Anfrage anzeigt.
    Es ist für Fälle gedacht, in denen ein anderer Prozess oder Server die Anfrage bearbeitet oder für Batch-Verarbeitungen.
- {{HTTPStatus(203, "203 Non-Authoritative Information")}}
  - : Dieser Antwortcode bedeutet, dass die zurückgegebenen Metadaten nicht genau dieselben sind, wie sie vom Ursprungsserver verfügbar sind, sondern aus einer lokalen oder einer Drittanbieterkopie stammen.
    Dies wird hauptsächlich für Spiegel- oder Backup-Ressourcen verwendet.
    Mit Ausnahme dieses spezifischen Falls wird die {{HTTPStatus(200, "200 OK")}}-Antwort gegenüber diesem Status bevorzugt.
- {{HTTPStatus(204, "204 No Content")}}
  - : Es gibt keinen Inhalt zum Senden für diese Anfrage, aber die Header sind nützlich.
    Der User Agent kann die zwischengespeicherten Header für diese Ressource mit den neuen aktualisieren.
- {{HTTPStatus(205, "205 Reset Content")}}
  - : Weist den User Agent an, das Dokument zurückzusetzen, das diese Anfrage gesendet hat.
- {{HTTPStatus(206, "206 Partial Content")}}
  - : Dieser Antwortcode wird als Antwort auf eine [Bereichsanfrage](/de/docs/Web/HTTP/Range_requests) verwendet, wenn der Client einen Teil oder Teile einer Ressource angefordert hat.
- {{HTTPStatus(207, "207 Multi-Status")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Übermittelt Informationen über mehrere Ressourcen für Situationen, in denen mehrere Statuscodes angemessen sein könnten.
- {{HTTPStatus(208, "208 Already Reported")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Wird innerhalb eines `<dav:propstat>`-Antwort-Elements verwendet, um zu vermeiden, dass die internen Mitglieder mehrerer Bindungen zu derselben Sammlung wiederholt aufgezählt werden.
- {{HTTPStatus(226, "226 IM Used")}} ([HTTP Delta encoding](https://datatracker.ietf.org/doc/html/rfc3229))
  - : Der Server hat eine {{HTTPMethod("GET")}}-Anfrage für die Ressource erfüllt, und die Antwort ist eine Repräsentation des Ergebnisses einer oder mehrerer Instanz-Manipulationen, die auf die aktuelle Instanz angewendet wurden.

## Umleitungsnachrichten

- {{HTTPStatus(300, "300 Multiple Choices")}}
  - : Bei der [agentengesteuerten Inhaltsverhandlung](/de/docs/Web/HTTP/Content_negotiation#agent-driven_negotiation) hat die Anfrage mehr als eine mögliche Antwort und der User-Agent oder der Nutzer sollte eine davon auswählen.
    Es gibt keinen standardisierten Weg für Clients, automatisch eine der Antworten auszuwählen, daher wird dies selten verwendet.
- {{HTTPStatus(301, "301 Moved Permanently")}}
  - : Die URL der angeforderten Ressource wurde dauerhaft geändert. Die neue URL wird in der Antwort angegeben.
- {{HTTPStatus(302, "302 Found")}}
  - : Dieser Antwortcode bedeutet, dass sich die URI der angeforderten Ressource _vorübergehend_ geändert hat.
    Weitere Änderungen an der URI könnten in der Zukunft vorgenommen werden, daher sollte die gleiche URI vom Client in zukünftigen Anfragen verwendet werden.
- {{HTTPStatus(303, "303 See Other")}}
  - : Der Server hat diese Antwort gesendet, um den Client zu einer anderen URI mit einer {{HTTPMethod("GET")}}-Anfrage weiterzuleiten, um die angeforderte Ressource abzurufen.
- {{HTTPStatus(304, "304 Not Modified")}}
  - : Dies wird für Caching-Zwecke verwendet.
    Es teilt dem Client mit, dass die Antwort nicht modifiziert wurde, sodass der Client weiterhin die gleiche [zwischengespeicherte](/de/docs/Web/HTTP/Caching) Version der Antwort verwenden kann.
- `305 Use Proxy` {{deprecated_inline}}
  - : In einer früheren Version der HTTP-Spezifikation definiert, um anzuzeigen, dass auf eine angeforderte Antwort über einen Proxy zugegriffen werden muss.
    Es wurde aufgrund von Sicherheitsbedenken bezüglich der In-Band-Konfiguration eines Proxys veraltet.
- `306 unused`
  - : Dieser Antwortcode wird nicht mehr verwendet, ist jedoch reserviert. Er wurde in einer früheren Version der HTTP/1.1-Spezifikation verwendet.
- {{HTTPStatus(307, "307 Temporary Redirect")}}
  - : Der Server sendet diese Antwort, um den Client zu einer anderen URI mit der gleichen Methode zu leiten, die in der vorherigen Anfrage verwendet wurde.
    Dies hat die gleichen Semantiken wie der `302 Found`-Antwortcode, mit der Ausnahme, dass der User Agent die verwendete HTTP-Methode _nicht ändern darf_: Wenn eine {{HTTPMethod("POST")}} in der ersten Anfrage verwendet wurde, muss eine `POST` auch in der weitergeleiteten Anfrage verwendet werden.
- {{HTTPStatus(308, "308 Permanent Redirect")}}
  - : Dies bedeutet, dass die Ressource jetzt dauerhaft unter einer anderen URI lokalisiert ist, die im {{HTTPHeader("Location")}}-Antwort-Header angegeben ist.
    Dies hat die gleichen Semantiken wie der `301 Moved Permanently` HTTP-Antwortcode, mit der Ausnahme, dass der User Agent die verwendete HTTP-Methode _nicht ändern darf_: Wenn eine {{HTTPMethod("POST")}} in der ersten Anfrage verwendet wurde, muss eine `POST` in der zweiten Anfrage verwendet werden.

## Client-Fehlerantworten

- {{HTTPStatus(400, "400 Bad Request")}}
  - : Der Server kann oder wird die Anfrage aufgrund eines wahrgenommenen Client-Fehlers (z. B. fehlerhafte Anfragesyntax, ungültige Anforderungsnachricht-Rahmenstruktur oder täuschende Anforderungsleitung) nicht verarbeiten.
- {{HTTPStatus(401, "401 Unauthorized")}}
  - : Obwohl der HTTP-Standard "unauthorized" angibt, bedeutet diese Antwort semantisch "unauthenticated".
    Das heißt, der Client muss sich authentifizieren, um die angeforderte Antwort zu erhalten.
- {{HTTPStatus(402, "402 Payment Required")}}
  - : Der ursprüngliche Zweck dieses Codes war für digitale Zahlungssysteme, dieser Statuscode wird jedoch selten verwendet und es gibt keine standardisierte Konvention.
- {{HTTPStatus(403, "403 Forbidden")}}
  - : Der Client hat keine Zugriffsrechte auf den Inhalt; das heißt, es ist unberechtigt, sodass der Server die angeforderte Ressource verweigert.
    Im Gegensatz zu `401 Unauthorized` ist die Identität des Clients dem Server bekannt.
- {{HTTPStatus(404, "404 Not Found")}}
  - : Der Server kann die angeforderte Ressource nicht finden.
    Im Browser bedeutet dies, dass die URL nicht erkannt wird.
    In einer API kann dies auch bedeuten, dass der Endpunkt gültig ist, die Ressource selbst jedoch nicht existiert.
    Server können diese Antwort auch anstelle von `403 Forbidden` senden, um die Existenz einer Ressource vor einem unberechtigten Client zu verbergen.
    Dieser Antwortcode ist wahrscheinlich der bekannteste, da er im Web häufig auftritt.
- {{HTTPStatus(405, "405 Method Not Allowed")}}
  - : Die [Anfragemethode](/de/docs/Web/HTTP/Methods) ist dem Server bekannt, wird jedoch von der Zielressource nicht unterstützt.
    Zum Beispiel darf eine API kein `DELETE` für eine Ressource zulassen oder die `TRACE`-Methode insgesamt.
- {{HTTPStatus(406, "406 Not Acceptable")}}
  - : Diese Antwort wird gesendet, wenn der Webserver nach der Durchführung einer [servergesteuerten Inhaltsverhandlung](/de/docs/Web/HTTP/Content_negotiation#server-driven_content_negotiation) keinen Inhalt findet, der den vom User Agent angegebenen Kriterien entspricht.
- {{HTTPStatus(407, "407 Proxy Authentication Required")}}
  - : Dies ist ähnlich wie `401 Unauthorized`, aber die Authentifizierung muss über einen Proxy erfolgen.
- {{HTTPStatus(408, "408 Request Timeout")}}
  - : Diese Antwort wird von einigen Servern über eine inaktive Verbindung gesendet, auch ohne dass eine vorherige Anfrage des Clients erfolgt.
    Es bedeutet, dass der Server diese unbenutzte Verbindung schließen möchte.
    Diese Antwort wird viel mehr verwendet, seit einige Browser HTTP-Vorverbindungen verwenden, um das Surfen zu beschleunigen.
    Einige Server können eine Verbindung schließen, ohne diese Nachricht zu senden.
- {{HTTPStatus(409, "409 Conflict")}}
  - : Diese Antwort wird gesendet, wenn eine Anfrage mit dem aktuellen Zustand des Servers in Konflikt steht.
    Im {{Glossary("WebDAV", "WebDAV")}} Remote-Web-Authoring sind `409`-Antworten Fehler, die an den Client gesendet werden, damit ein Benutzer einen Konflikt lösen und die Anfrage erneut senden kann.
- {{HTTPStatus(410, "410 Gone")}}
  - : Diese Antwort wird gesendet, wenn der angeforderte Inhalt dauerhaft vom Server gelöscht wurde, ohne Weiterleitungsadresse.
    Die Clients sollten ihre Caches und Links zur Ressource entfernen.
    Die HTTP-Spezifikation beabsichtigt, dass dieser Statuscode für "zeitlich begrenzte, Werbedienste" verwendet wird.
    APIs sollten sich nicht verpflichtet fühlen, Ressourcen, die gelöscht wurden, mit diesem Statuscode anzugeben.
- {{HTTPStatus(411, "411 Length Required")}}
  - : Der Server hat die Anfrage abgelehnt, weil das {{HTTPHeader("Content-Length")}}-Headerfeld nicht definiert ist und der Server es benötigt.
- {{HTTPStatus(412, "412 Precondition Failed")}}
  - : Bei [bedingten Anfragen](/de/docs/Web/HTTP/Conditional_requests) hat der Client Vorbedingungen in seinen Headern angegeben, die der Server nicht erfüllt.
- {{HTTPStatus(413, "413 Content Too Large")}}
  - : Der Anfragetext ist größer als die vom Server definierten Grenzen.
    Der Server könnte die Verbindung schließen oder ein {{HTTPHeader("Retry-After")}}-Headerfeld zurückgeben.
- {{HTTPStatus(414, "414 URI Too Long")}}
  - : Die vom Client angeforderte URI ist länger, als der Server interpretieren möchte.
- {{HTTPStatus(415, "415 Unsupported Media Type")}}
  - : Das Medienformat der angeforderten Daten wird vom Server nicht unterstützt, daher lehnt der Server die Anfrage ab.
- {{HTTPStatus(416, "416 Range Not Satisfiable")}}
  - : Die durch das `Range`-Headerfeld in der Anfrage spezifizierten [Bereiche](/de/docs/Web/HTTP/Range_requests) können nicht erfüllt werden.
    Es ist möglich, dass der Bereich außerhalb der Datengröße der Zielressource liegt.
- {{HTTPStatus(417, "417 Expectation Failed")}}
  - : Dieser Antwortcode bedeutet, dass die durch das {{HTTPHeader("Expect")}}-Anforderungs-Headerfeld angegebene Erwartung vom Server nicht erfüllt werden kann.
- {{HTTPStatus(418, "418 I'm a teapot")}}
  - : Der Server lehnt den Versuch ab, Kaffee mit einer Teekanne zu brühen.
- {{HTTPStatus(421, "421 Misdirected Request")}}
  - : Die Anfrage wurde an einen Server gerichtet, der nicht in der Lage ist, eine Antwort zu erstellen.
    Dies kann von einem Server gesendet werden, der nicht so konfiguriert ist, dass er Antworten für die Kombination aus Schema und Autorität erzeugt, die in der Anforderungs-URI enthalten sind.
- {{HTTPStatus(422, "422 Unprocessable Content")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Die Anfrage war gut geformt, konnte jedoch aufgrund semantischer Fehler nicht bearbeitet werden.
- {{HTTPStatus(423, "423 Locked")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Die Ressource, auf die zugegriffen wird, ist gesperrt.
- {{HTTPStatus(424, "424 Failed Dependency")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Die Anfrage schlug aufgrund eines Fehlers einer vorherigen Anfrage fehl.
- {{HTTPStatus(425, "425 Too Early")}} {{experimental_inline}}
  - : Gibt an, dass der Server nicht bereit ist, das Risiko der Ausführung einer Anfrage einzugehen, die möglicherweise wiederholt wird.
- {{HTTPStatus(426, "426 Upgrade Required")}}
  - : Der Server weigert sich, die Anfrage mit dem aktuellen Protokoll durchzuführen, könnte dies jedoch tun, nachdem der Client zu einem anderen Protokoll wechselt.
    Der Server sendet in einer 426-Antwort einen {{HTTPHeader("Upgrade")}}-Header, um das erforderliche Protokoll anzuzeigen.
- {{HTTPStatus(428, "428 Precondition Required")}}
  - : Der Ursprungsserver verlangt, dass die Anfrage [bedingt](/de/docs/Web/HTTP/Conditional_requests) ist.
    Diese Antwort soll das 'Lost Update'-Problem verhindern, bei dem ein Client den Zustand einer Ressource holt, ihn modifiziert und ihn zurück zum Server stellt, währenddessen eine dritte Partei den Zustand auf dem Server geändert hat, was zu einem Konflikt führt.
- {{HTTPStatus(429, "429 Too Many Requests")}}
  - : Der Benutzer hat zu viele Anfragen in einer bestimmten Zeitspanne gesendet ({{Glossary("Rate_limit", "Rate Limiting")}}).
- {{HTTPStatus(431, "431 Request Header Fields Too Large")}}
  - : Der Server ist nicht bereit, die Anfrage zu verarbeiten, da deren Headerfelder zu groß sind.
    Die Anfrage kann nach Reduzierung der Größe der Anforderungs-Headerfelder erneut gesendet werden.
- {{HTTPStatus(451, "451 Unavailable For Legal Reasons")}}
  - : Der User Agent hat eine Ressource angefordert, die aus rechtlichen Gründen nicht bereitgestellt werden kann, wie z. B. eine von einer Regierung zensierte Webseite.

## Server-Fehlerantworten

- {{HTTPStatus(500, "500 Internal Server Error")}}
  - : Der Server hat eine Situation festgestellt, mit der er nicht umgehen kann.
    Dieser Fehler ist generisch und zeigt an, dass der Server keinen passenderen `5XX`-Statuscode hat, um zu antworten.
- {{HTTPStatus(501, "501 Not Implemented")}}
  - : Die Anfragemethode wird vom Server nicht unterstützt und kann nicht bearbeitet werden. Die einzigen Methoden, die Server unterstützen müssen (und daher diesen Code nicht zurückgeben dürfen), sind {{HTTPMethod("GET")}} und {{HTTPMethod("HEAD")}}.
- {{HTTPStatus(502, "502 Bad Gateway")}}
  - : Diese Fehlerantwort bedeutet, dass der Server, während er als Gateway arbeitet, eine ungültige Antwort erhalten hat, die zur Bearbeitung der Anfrage benötigt wird.
- {{HTTPStatus(503, "503 Service Unavailable")}}
  - : Der Server ist nicht bereit, die Anfrage zu bearbeiten.
    Häufige Ursachen sind ein Server, der für Wartungsarbeiten ausgefallen ist oder überlastet ist.
    Beachten Sie, dass zusammen mit dieser Antwort eine benutzerfreundliche Seite gesendet werden sollte, die das Problem erklärt.
    Diese Antwort sollte für temporäre Bedingungen verwendet werden, und der {{HTTPHeader("Retry-After")}} HTTP-Header sollte, falls möglich, die geschätzte Zeit vor der Wiederherstellung des Dienstes enthalten.
    Der Webmaster muss auch auf die Caching-bezogenen Header achten, die zusammen mit dieser Antwort gesendet werden, da diese Antworten auf temporäre Bedingungen normalerweise nicht zwischengespeichert werden sollten.
- {{HTTPStatus(504, "504 Gateway Timeout")}}
  - : Diese Fehlerantwort wird gegeben, wenn der Server als Gateway fungiert und keine Antwort rechtzeitig erhalten kann.
- {{HTTPStatus(505, "505 HTTP Version Not Supported")}}
  - : Die in der Anfrage verwendete HTTP-Version wird vom Server nicht unterstützt.
- {{HTTPStatus(506, "506 Variant Also Negotiates")}}
  - : Der Server hat einen internen Konfigurationsfehler: während der Inhaltsaushandlung ist die gewählte Variante so konfiguriert, dass sie selbst an der Inhaltsaushandlung teilnimmt, was bei der Erstellung von Antworten zu zirkulären Verweisen führt.
- {{HTTPStatus(507, "507 Insufficient Storage")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Die Methode konnte nicht für die Ressource durchgeführt werden, da der Server nicht in der Lage ist, die zur erfolgreichen Durchführung der Anfrage benötigte Repräsentation zu speichern.
- {{HTTPStatus(508, "508 Loop Detected")}} ({{Glossary("WebDAV", "WebDAV")}})
  - : Der Server hat eine Endlosschleife beim Verarbeiten der Anfrage erkannt.
- {{HTTPStatus(510, "510 Not Extended")}}
  - : Die Anfrage des Clients gibt eine HTTP-Erweiterung ({{RFC("2774")}}) an, die zur Bearbeitung der Anfrage verwendet werden soll, aber die Erweiterung wird nicht unterstützt.
- {{HTTPStatus(511, "511 Network Authentication Required")}}
  - : Gibt an, dass der Client authentifizieren muss, um Netzwerkzugang zu erlangen.

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Liste der HTTP-Statuscodes auf Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
- [Offizielles IANA-Register der HTTP-Statuscodes](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)
