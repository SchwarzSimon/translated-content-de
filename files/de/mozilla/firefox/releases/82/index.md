---
title: Firefox 82 für Entwickler
slug: Mozilla/Firefox/Releases/82
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{FirefoxSidebar}}

Dieser Artikel bietet Informationen über die Änderungen in Firefox 82, die Entwickler betreffen werden. Firefox 82 wurde am 20. Oktober 2020 veröffentlicht.

> [!NOTE]
> Siehe auch [Coming through with Firefox 82](https://hacks.mozilla.org/2020/10/coming-through-with-firefox-82/) auf Mozilla Hacks.

## Änderungen für Web-Entwickler

### Entwicklerwerkzeuge

- Sie können jetzt [Server-sent Events inspizieren](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/inspecting_server-sent_events/index.html), indem Sie den [Network Monitor](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/index.html) nutzen ([Firefox-Bug 1640857](https://bugzil.la/1640857)).
- Das _Message_-Panel des Network Monitors wurde nun mit dem _Response_-Panel zusammengeführt — Nachrichten (z.B. von WebSockets oder server-sent Events) können jetzt direkt unterhalb der Antwortliste angezeigt werden ([Firefox-Bug 1636421](https://bugzil.la/1636421)).

### HTML

- Der Farbwähler, der für [`<input type="color">`](/de/docs/Web/HTML/Reference/Elements/input/color) verwendet wird, ist jetzt auf Windows über die Tastatur zugänglich ([Firefox-Bug 1526820](https://bugzil.la/1526820)).
- Das `allow-downloads`-Flag für das [`<iframe sandbox>`](/de/docs/Web/HTML/Reference/Elements/iframe)-Attribut wird jetzt unterstützt ([Firefox-Bug 1656212](https://bugzil.la/1656212)).

### CSS

- Unterstützung für das neue {{CSSxRef("::file-selector-button", "::file-selector-button")}} Pseudoelement wurde hinzugefügt. Dieses Pseudoelement repräsentiert den Dateiauswahl-Button innerhalb eines [`<input type="file">`](/de/docs/Web/HTML/Reference/Elements/input/file)-Elements ([Firefox-Bug 1635675](https://bugzil.la/1635675), [Firefox-Bug 1662478](https://bugzil.la/1662478)).
- Wir haben die Fehlerbehandlung für die Pseudoklassen {{CSSxRef(":is", ":is()")}} und {{CSSxRef(":where", ":where()")}} verbessert. Diese Pseudoklassen akzeptieren nun eine großzügige Selektorliste, bei der ein ungültiger Selektor in der Liste die gesamte Liste nicht ungültig macht ([Firefox-Bug 1664718](https://bugzil.la/1664718)).
- `appearance: button` gilt jetzt nur noch für Buttons; der `button`-Wert von {{CSSxRef("appearance")}} verhält sich ansonsten wie `auto` ([Firefox-Bug 1662703](https://bugzil.la/1662703)).

#### Entfernungen

- Wir haben die propriatäre [`:-moz-user-disabled`](/de/docs/Web/CSS/:-moz-user-disabled) Pseudoklasse entfernt ([Firefox-Bug 1664432](https://bugzil.la/1664432)).

### HTTP

- Die `inline`-Direktive des [`Content-Disposition`](/de/docs/Web/HTTP/Reference/Headers/Content-Disposition)-Headers wird jetzt ignoriert, wenn das `download`-Attribut des HTML [`<a>`](/de/docs/Web/HTML/Reference/Elements/a)-Elements angegeben ist (für [gleich-origin URLs](/de/docs/Web/Security/Same-origin_policy)). Beachten Sie, dass, falls angegeben, der `filename` des `Content-Disposition`-Headers bevorzugt gegenüber einem im `download`-Attribut angegebenen Dateinamen verwendet wird ([Firefox-Bug 1658877](https://bugzil.la/1658877)).

### APIs

#### Neue APIs

- Die [Media Session API](/de/docs/Web/API/Media_Session_API) ist jetzt standardmäßig aktiviert ([Firefox-Bug 1665496](https://bugzil.la/1665496)).

#### DOM

- [`Document.execCommand()`](/de/docs/Web/API/Document/execCommand) wird nicht mehr für verschachtelte/rekursive Aufrufe unterstützt, die jetzt `false` zurückgeben ([Firefox-Bug 1634262](https://bugzil.la/1634262)).
- [`Element.setPointerCapture()`](/de/docs/Web/API/Element/setPointerCapture) wirft die `NotFoundError`-Ausnahme, wenn die Zeiger-`id` ungültig ist, gemäß der [Spezifikation](https://w3c.github.io/pointerevents/#setting-pointer-capture) ([Firefox-Bug 1662124](https://bugzil.la/1662124)). Zuvor wurde fälschlicherweise eine `InvalidPointerId`-Ausnahme geworfen.
- Die [`window.name`](/de/docs/Web/API/Window/name)-Eigenschaft wird auf einen leeren String zurückgesetzt, wenn ein Tab eine Seite von einer anderen Domain lädt und wiederhergestellt, wenn die ursprüngliche Seite erneut geladen wird (z.B. über die "Zurück"-Schaltfläche). Dies verhindert, dass eine nicht vertrauenswürdige Seite auf Informationen zugreift, die die vorherige Seite möglicherweise in der Variablen gespeichert hat. Diese Änderung kann Frameworks beeinflussen, die `window.name` für Cross-Domain-Messaging verwenden ([Firefox-Bug 444222](https://bugzil.la/444222)).

### WebDriver-Konformität (Marionette)

- Um eine realistischere Benutzernavigation zu simulieren, wurden alle unterstützten Navigationsbefehle in den übergeordneten Prozess verschoben ([Firefox-Bug 1612831](https://bugzil.la/1612831)).
- Wir haben die Überprüfungen für den aktuellen oder obersten Browsing-Kontext für alle Befehle aktualisiert, um die Übereinstimmung mit der WebDriver-Spezifikation zu verbessern ([Firefox-Bug 1493108](https://bugzil.la/1493108)).
- Ein Fehler in `WebDriver:ElementClick` wurde behoben, der manchmal dazu führte, dass der Befehl zurückgegeben wurde, bevor das Klickereignis tatsächlich synthetisiert wurde ([Firefox-Bug 1394354](https://bugzil.la/1394354)).

## Änderungen für Add-on-Entwickler

- Die Methoden [`tabs.captureTab()`](/de/docs/Mozilla/Add-ons/WebExtensions/API/tabs/captureTab) und [`tabs.captureVisibleTab()`](/de/docs/Mozilla/Add-ons/WebExtensions/API/tabs/captureVisibleTab) erfassen jetzt einen Bereich des Inhalts des relevanten Tabs, der durch die `rect`-Eigenschaft des angegebenen [`options`](/de/docs/Mozilla/Add-ons/WebExtensions/API/extensionTypes/ImageDetails)-Objekts spezifiziert wird, oder den sichtbaren Bereich des Tabs, wenn diese Eigenschaft nicht angegeben wird ([Firefox-Bug 1636508](https://bugzil.la/1636508)). Zuvor war die `rect`-Eigenschaft nicht verfügbar, und diese Methoden erfassten immer den sichtbaren Bereich des relevanten Tabs.
- Der Schreibschutz-Zugriff auf `cookieStoreId` erfordert nicht mehr die `"cookies"` [Berechtigung](/de/docs/Mozilla/Add-ons/WebExtensions/manifest.json/permissions) ([Firefox-Bug 1662329](https://bugzil.la/1662329)).

## Ältere Versionen

{{Firefox_for_developers}}
