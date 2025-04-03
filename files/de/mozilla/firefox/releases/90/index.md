---
title: Firefox 90 für Entwickler
slug: Mozilla/Firefox/Releases/90
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{FirefoxSidebar}}

Dieser Artikel bietet Informationen über die Änderungen in Firefox 90, die Entwickler betreffen werden. Firefox 90 wurde am 13. Juli 2021 veröffentlicht.

> [!NOTE]
> Siehe auch [Getting lively with Firefox 90](https://hacks.mozilla.org/2021/07/getting-lively-with-firefox-90/) auf Mozilla Hacks.

## Änderungen für Webentwickler

### Entwicklerwerkzeuge

- Die Antwortansicht zeigt jetzt eine [Vorschau für Web-Schriftarten](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/request_details/index.html#response-tab) ([Firefox-Bug 872078](https://bugzil.la/872078)).

### HTML

- Eine Korrektur zur Behandlung von Formular-Nutzlasten in Bezug auf das Normalisieren von Zeilenumbrüchen und Escaping in multipart/formdata. Dies entspricht der aktualisierten Spezifikation und dem Verhalten anderer Browser-Implementierungen. ([Firefox-Bug 1686765](https://bugzil.la/1686765)).
- Firefox setzt jetzt die {{Glossary("intrinsic_size", "intrinsische Größe")}} und Auflösung eines Bildes basierend auf {{Glossary("EXIF", "EXIF")}}-Informationen (falls vorhanden und konsistent). Dies ermöglicht es einem Server beispielsweise, ein niedrigauflösendes Platzhalterbild zu senden, um das Laden zu beschleunigen. Dies ermöglicht auch [eine Reihe anderer Anwendungsfälle](https://github.com/eeeps/exif-intrinsic-sizing-explainer) ([Firefox-Bug 1680387](https://bugzil.la/1680387)).

### CSS

- `-webkit-image-set()` wurde als Alias für die standardisierte {{cssxref("image/image-set", "image/image-set()")}}-Funktion implementiert ([Firefox-Bug 1709415](https://bugzil.la/1709415)).

### JavaScript

- [Private statische und Instanzfelder sowie Methoden in Klassen](/de/docs/Web/JavaScript/Reference/Classes/Private_properties) werden jetzt standardmäßig unterstützt ([Firefox-Bug 1708235](https://bugzil.la/1708235) und [Firefox-Bug 1708236](https://bugzil.la/1708236)).
- Der [`in`](/de/docs/Web/JavaScript/Reference/Operators/in)-Operator kann jetzt verwendet werden, um [zu überprüfen, ob eine private Klassenmethode oder ein Feld definiert wurde](/de/docs/Web/JavaScript/Reference/Operators/in#using_the_in_operator_to_implement_branded_checks). Dies bietet einen kompakteren Ansatz für den Umgang mit möglicherweise undefinierten Funktionen, im Gegensatz zum Einwickeln von Code in `try/catch`-Blöcken ([Firefox-Bug 1648090](https://bugzil.la/1648090)).
- Benutzerdefinierte Datums-/Uhrzeitformate, die als Optionen an den [`Intl.DateTimeFormat()`-Konstruktor](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat) übergeben werden, können jetzt `dayPeriod` enthalten – einen Wert, der angibt, dass die ungefähre Tageszeit (z.B. "am Morgen", "nachts" usw.) als `narrow`, `short` oder `long` Zeichenkette enthalten sein soll ([Firefox-Bug 1645115](https://bugzil.la/1645115)).
- Die relative Indexierungsmethode `at()` wurde zu den globalen Objekten [`Array`](/de/docs/Web/JavaScript/Reference/Global_Objects/Array), [`String`](/de/docs/Web/JavaScript/Reference/Global_Objects/String) und [`TypedArray`](/de/docs/Web/JavaScript/Reference/Global_Objects/TypedArray) hinzugefügt ([Firefox-Bug 1681371](https://bugzil.la/1681371)).

### HTTP

- Die HTTP {{Glossary("Fetch_metadata_request_header", "Fetch-Metadaten-Anforderungs-Header")}} (`Sec-Fetch-*`) werden jetzt unterstützt. Diese Header bieten Servern zusätzliche Informationen über Anfragen, einschließlich ob sie same-origin, cross-origin, same-site oder benutzerinitiiert sind und wo/wie die angeforderten Daten verwendet werden sollen. Dies ermöglicht es Servern, gegen mehrere Arten von Cross-Origin-Angriffen vorzugehen ([Firefox-Bug 1695911](https://bugzil.la/1695911)).

#### Entfernungen

- FTP wurde nun aus Firefox entfernt ([Firefox-Bug 1574475](https://bugzil.la/1574475)). Dies folgt auf die [Abwertung in Firefox 88](/de/docs/Mozilla/Firefox/Releases/88#http). Beachten Sie, dass Web-Erweiterungen sich weiterhin als [FTP-Protokoll-Handler](/de/docs/Mozilla/Add-ons/WebExtensions/manifest.json/protocol_handlers) registrieren können.

### APIs

#### DOM

- Unterstützung wurde für die veralteten [`WheelEvent`](/de/docs/Web/API/WheelEvent)-Eigenschaften hinzugefügt: `WheelEvent.wheelDelta`, `WheelEvent.wheelDeltaX` und `WheelEvent.wheelDeltaY`. Dies ermöglicht es Firefox, mit einem kleinen Teil von Seiten zu arbeiten, die durch kürzliche Kompatibilitätsverbesserungen von `WheelEvent` beeinträchtigt wurden ([Firefox-Bug 1708829](https://bugzil.la/1708829)).
- Die [`CanvasRenderingContext2D`](/de/docs/Web/API/CanvasRenderingContext2D)-Schnittstelle der [Canvas API](/de/docs/Web/API/Canvas_API) bietet jetzt eine [`createConicGradient()`](/de/docs/Web/API/CanvasRenderingContext2D/createConicGradient)-Methode. Diese gibt ein [`CanvasGradient`](/de/docs/Web/API/CanvasGradient) zurück, ähnlich wie die bestehenden [`linear`](/de/docs/Web/API/CanvasRenderingContext2D/createLinearGradient)- und [`radial`](/de/docs/Web/API/CanvasRenderingContext2D/createRadialGradient)-Gradienten, ermöglicht jedoch, dass ein Gradient um einen durch Koordinaten definierten Punkt bewegt werden kann. Weitere Details siehe [Firefox-Bug 1627014](https://bugzil.la/1627014).
- Unterstützung für das `matrix`-Protokoll wurde hinzugefügt und kann nun als gültiges Schema an die [`Navigator.registerProtocolHandler()`](/de/docs/Web/API/Navigator/registerProtocolHandler)-Methode übergeben werden.

### WebDriver-Konformität (Marionette)

- Marionette beschränkt sich jetzt auf eine einzige aktive WebDriver-Sitzung ([Firefox-Bug 1691047](https://bugzil.la/1691047)).
- Unterstützung für neue Benutzer-Prompt-Typen in Firefox hinzugefügt ([Firefox-Bug 1686741](https://bugzil.la/1686741))
- Fenster-Handles verwenden jetzt eine eindeutige ID und ändern sich nicht bei Prozesswechseln, wie sie durch [Cross-Group-Navigationen](https://firefox-source-docs.mozilla.org/dom/navigation/nav_replace.html#cross-group-navigations) verursacht werden ([Firefox-Bug 1680479](https://bugzil.la/1680479)).
- Problem bei der unpassenden Beendigung des aktuellen WebDriver-Befehls behoben, wenn ein neues Benutzer-Prompt in einem Hintergrund-Tab geöffnet wurde ([Firefox-Bug 1701686](https://bugzil.la/1701686)).
- Der `WebDriver:GetWindowHandles`-Befehl wurde korrigiert, um nun korrekt mit nicht geladenen Tabs umzugehen ([Firefox-Bug 1682062](https://bugzil.la/1682062)).
- Der `WebDriver:NewSession`-Befehl wurde korrigiert, um immer die `proxy`-Fähigkeit zurückzugeben, selbst wenn diese leer ist ([Firefox-Bug 1710935](https://bugzil.la/1710935)).

#### Entfernungen

- Mit der [Entfernung der FTP-Unterstützung in Firefox 90](#removals_http) wird die `ftpProxy`-Fähigkeit nicht mehr ausgewertet und bei Verwendung wird ein `invalid argument`-Fehler ausgelöst ([Firefox-Bug 1703805](https://bugzil.la/1703805)).

## Änderungen für Add-on-Entwickler

- Das `matrix`-URI-Schema wird jetzt unterstützt und kann als Protokoll innerhalb des [`protocol_handlers`](/de/docs/Mozilla/Add-ons/WebExtensions/manifest.json/protocol_handlers)-Schlüssels in einer Erweiterungs-`manifest.json` definiert werden.
- Ab dieser Version kann die [Cache API](/de/docs/Web/API/Cache) in den Erweiterungsseiten und Worker-Globals verwendet werden. Für weitere Details siehe ([Firefox-Bug 1575625](https://bugzil.la/1575625)).

## Ältere Versionen

{{Firefox_for_developers}}
