---
title: Firefox 71 für Entwickler
slug: Mozilla/Firefox/Releases/71
l10n:
  sourceCommit: c263f06fa14ed56153e345006bb459c9df014b98
---

{{FirefoxSidebar}}

Dieser Artikel bietet Informationen über die Änderungen in Firefox 71, die Entwickler betreffen. Firefox 71 wurde am 3. Dezember 2019 veröffentlicht.

## Änderungen für Webentwickler

### Entwickler-Tools

[Konsole](https://firefox-source-docs.mozilla.org/devtools-user/web_console/index.html):

- Der [Mehrzeilenmodus](https://firefox-source-docs.mozilla.org/devtools-user/web_console/the_command_line_interpreter/index.html#multi-line-mode) der Konsole ist jetzt standardmäßig verfügbar.
- Die Konfigurationseinstellungen der Konsole sind jetzt in einem neuen [Werkzeugleisten-Einstellungsmenü](https://firefox-source-docs.mozilla.org/devtools-user/web_console/ui_tour/index.html#toolbar) zusammengefasst ([Firefox-Bug 1523868](https://bugzil.la/1523868)).

[JavaScript-Debugger](https://firefox-source-docs.mozilla.org/devtools-user/debugger/index.html):

- Die [Inline-Variablenvorschau](https://firefox-source-docs.mozilla.org/devtools-user/debugger/how_to/set_a_breakpoint/index.html#inline-variable-preview) wurde aktiviert ([Firefox-Bug 1576679](https://bugzil.la/1576679)).
- [Protokollierung bei Ereignissen](https://firefox-source-docs.mozilla.org/devtools-user/debugger/set_event_listener_breakpoints/index.html#logging-on-events) ist jetzt verfügbar ([Firefox-Bug 1110276](https://bugzil.la/1110276)), ebenso wie die Möglichkeit, [nach Ereignistyp zu filtern](https://firefox-source-docs.mozilla.org/devtools-user/debugger/set_event_listener_breakpoints/index.html#filter-by-event-type).
- Das neue Debugger-[Pausen-Overlay](https://firefox-source-docs.mozilla.org/devtools-user/debugger/how_to/step_through_code/index.html#pause-on-breakpoints-overlay) kann jetzt mit der Voreinstellung `devtools.debugger.features.overlay` deaktiviert werden ([Firefox-Bug 1579768](https://bugzil.la/1579768)).
- Es gibt neue [Tastenkombinationen](https://firefox-source-docs.mozilla.org/devtools-user/keyboard_shortcuts/index.html) zum Öffnen des Debuggers: `Ctrl` + `Shift` + `Z` auf Linux/Windows und `Cmd` + `Opt` + `Z` auf macOS ([Firefox-Bug 1583042](https://bugzil.la/1583042)).
- Beim Anhalten an einem [DOM-Mutation Breakpoint](https://firefox-source-docs.mozilla.org/devtools-user/debugger/break_on_dom_mutation/index.html) wird jetzt das DOM-Element erwähnt, das den Breakpoint hat, und, falls verfügbar, das Kind-Element, das hinzugefügt/entfernt wurde ([Firefox-Bug 1576145](https://bugzil.la/1576145)).
- Die Positionen in [schön gedruckten Quellen](https://firefox-source-docs.mozilla.org/devtools-user/debugger/how_to/pretty-print_a_minified_file/index.html) sind jetzt korrekt nach dem Schön-Drucken und beim Sprung zur Quelle aus dem [Event-Listener-Tooltip](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/how_to/examine_event_listeners/index.html) des Inspektors ([Firefox-Bug 1500222](https://bugzil.la/1500222)).

[Netzwerk-Monitor](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/index.html):

- Der [Websocket-Inspektor](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/inspecting_web_sockets/index.html) ist jetzt standardmäßig aktiviert ([Firefox-Bug 1573805](https://bugzil.la/1573805)).
- Sie können jetzt eine [Volltextsuche](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/request_list/index.html#search-in-requests) in den Anfragen-/Antwortkörpern, HEADERN und Cookies durchführen.
- Sie können jetzt Muster eingeben, um [bestimmte URLs zu blockieren](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/request_list/index.html#blocking-specific-urls).
- Der [Timing-Tab](https://firefox-source-docs.mozilla.org/devtools-user/network_monitor/request_details/index.html#timings) gibt jetzt Timing-Daten im {{httpheader("Server-Timing")}} Header preis ([Firefox-Bug 1403051](https://bugzil.la/1403051)).

[Seiteninspektor](https://firefox-source-docs.mozilla.org/devtools-user/page_inspector/index.html):

- Farbkleckse werden jetzt neben CSS-Variablendefinitionen angezeigt, die Farbwerte haben ([Firefox-Bug 1456167](https://bugzil.la/1456167)).
- {{cssxref(":visited")}}-Stile werden jetzt in der CSS-Stilansicht angezeigt ([Firefox-Bug 713106](https://bugzil.la/713106)).

### CSS

- Der [Subgrid-Wert](/de/docs/Web/CSS/CSS_grid_layout/Subgrid) aus CSS Grid Level 2 wurde zu {{cssxref("grid-template-columns")}} und {{cssxref("grid-template-rows")}} hinzugefügt ([Firefox-Bug 1580894](https://bugzil.la/1580894)).
- Unterstützung für die {{cssxref("column-span")}}-Eigenschaft im [Mehrspaltigen Layout](/de/docs/Web/CSS/CSS_multicol_layout) wurde hinzugefügt ([Firefox-Bug 1426010](https://bugzil.la/1426010)).
- Unterstützung für den `path()`-Wert von {{cssxref("clip-path")}} wurde hinzugefügt ([Firefox-Bug 1488530](https://bugzil.la/1488530)).
- Die `height`- und `width`-HTML-Attribute auf dem {{htmlelement("img")}}-Element wurden mit einer internen {{cssxref("aspect-ratio")}}-Eigenschaft verknüpft ([Firefox-Bug 1585637](https://bugzil.la/1585637)). [Lesen Sie den Leitfaden zu dieser Funktion auf MDN](/de/docs/Learn_web_development/Extensions/Performance/Multimedia#rendering_strategy_preventing_jank_when_loading_images).

#### Entfernungen

- CSS Radialverläufe akzeptieren keine negativen Radien mehr ([Firefox-Bug 1583736](https://bugzil.la/1583736)).

### JavaScript

- Die {{jsxref("Promise.allSettled()")}}-Methode wird jetzt unterstützt ([Firefox-Bug 1549176](https://bugzil.la/1549176)). Diese Methode ermöglicht es Ihnen, leicht zu warten, bis jedes Versprechen in einer Menge von Versprechen entweder erfüllt oder abgelehnt wird, bevor weiterer Code ausgeführt wird.

#### Entfernungen

- Die nicht standardmäßigen Array-generischen Methoden wurden in Firefox 71 entfernt ([Firefox-Bug 1222547](https://bugzil.la/1222547)). Sie wurden zuerst in Firefox 1.5 eingeführt und ab Firefox 68 als veraltet markiert. Wenn Ihr Anwendungsfall darin besteht, Array-Generika auf Array-ähnlichen Objekten zu verwenden, können Sie Ihr Objekt in ein richtiges Array umwandeln, indem Sie [`Array.from()`](/de/docs/Web/JavaScript/Reference/Global_Objects/Array/from) verwenden und dann die Standard-Array-Methoden nutzen.

### MathML

- [MathML-Elemente](/de/docs/Web/MathML/Reference/Element) verwenden jetzt ein MathML-DOM und ihre Klasse ist [`MathMLElement`](/de/docs/Web/API/MathMLElement). Mit einem ordentlichen MathML-DOM können Sie jetzt beispielsweise `mathmlEl.style` oder globale Ereignishandler verwenden. Vor dieser Änderung implementierten MathML-Elemente nur die [`Element`](/de/docs/Web/API/Element)-Klasse ([Firefox-Bug 1571487](https://bugzil.la/1571487)).

### APIs

#### Neue APIs

Die [Media Session API](/de/docs/Web/API/Media_Session_API) ist jetzt teilweise implementiert. Diese API bietet einen standardisierten Mechanismus, mit dem Ihr Inhalt dem zugrunde liegenden Betriebssystem Informationen über den Zustand der Medien, die es abspielt, mitteilen kann. Dazu gehören Metadaten wie Künstler, Album und Titelname sowie potenziell Albumcover ([Firefox-Bug 1580602](https://bugzil.la/1580602)).

Die API bietet auch eine Möglichkeit, Benachrichtigungen zu erhalten, wenn die Mediensteuerungen des Geräts (wie Wiedergabe-, Pause- und Such-Tasten) vom Benutzer aktiviert werden. Zu diesem Zweck ist die [`MediaSession`](/de/docs/Web/API/MediaSession)-Schnittstelle jetzt teilweise implementiert, mit Unterstützung zum Setzen und Abrufen der gerade abgespielten Medienmetadaten und für die Methode [`setActionHandler()`](/de/docs/Web/API/MediaSession/setActionHandler). Um auf die `MediaSession`-API zuzugreifen, verwenden Sie die [`navigator.mediaSession`](/de/docs/Web/API/Navigator/mediaSession)-Eigenschaft.

#### DOM

- Der [`StaticRange()`](/de/docs/Web/API/StaticRange/StaticRange)-Konstruktor wird jetzt unterstützt ([Firefox-Bug 1575980](https://bugzil.la/1575980)).
- Die MathML-Interface [`MathMLElement`](/de/docs/Web/API/MathMLElement) wurde implementiert ([Firefox-Bug 1571487](https://bugzil.la/1571487)).

#### Medien, Web Audio und WebRTC

- Die [`MediaRecorder`](/de/docs/Web/API/MediaRecorder)-Schnittstelle implementiert jetzt die Eigenschaften [`audioBitsPerSecond`](/de/docs/Web/API/MediaRecorder/audioBitsPerSecond) und [`videoBitsPerSecond`](/de/docs/Web/API/MediaRecorder/videoBitsPerSecond) ([Firefox-Bug 1514158](https://bugzil.la/1514158)).

#### Canvas und WebGL

- Die WebGL-Erweiterungen [`OVR_multiview2`](/de/docs/Web/API/OVR_multiview2) und [`OES_fbo_render_mipmap`](/de/docs/Web/API/OES_fbo_render_mipmap) sind jetzt standardmäßig freigeschaltet ([Firefox-Bug 1584277](https://bugzil.la/1584277), [Firefox-Bug 1583878](https://bugzil.la/1583878)).

#### Entfernungen

Die folgenden nicht standardmäßigen Mitglieder von [`DataTransfer`](/de/docs/Web/API/DataTransfer) wurden entfernt ([Firefox-Bug 1345192](https://bugzil.la/1345192)):

- `DataTransfer.mozItemCount`
- `DataTransfer.mozClearDataAt()`
- `DataTransfer.mozGetDataAt()`
- `DataTransfer.mozSetDataAt()`
- `DataTransfer.mozTypesAt()`

### WebDriver-Konformität (Marionette)

- Sowohl die Befehle `WebDriver:TakeScreenshot` als auch `WebDriver:TakeElementScreenshot` wurden aktualisiert, um die Einstellung des unaufgeforderten Prompt-Verhaltens zu respektieren ([Firefox-Bug 1584927](https://bugzil.la/1584927)).
- Der Befehl `Marionette:Quit` wurde so aktualisiert, dass jetzt auch das Beenden oder Neustarten anderer Gecko-gesteuerter Anwendungen neben Firefox möglich ist ([Firefox-Bug 1298921](https://bugzil.la/1298921)).
- Für GeckoView-basierte Browser auf Android wird der zurückgegebene `browserName` in den Sitzungsfähigkeiten jetzt immer `firefox` sein ([Firefox-Bug 1587364](https://bugzil.la/1587364)).

## Änderungen für Add-on-Entwickler

### API-Änderungen

- {{WebExtAPIRef("downloads.download")}} identifiziert und meldet jetzt die folgenden HTTP-Antwortcodes als Fehler:

  - 404 gibt `SERVER_BAD_CONTENT` zurück
  - 403 gibt `SERVER_FORBIDDEN` zurück
  - 402 und Proxy 407 geben `SERVER_UNAUTHORIZED` zurück
  - Alles andere über 400 gibt `SERVER_FAILED` zurück ([Firefox-Bug 1576333](https://bugzil.la/1576333))

- {{WebExtAPIRef("downloads.download")}} enthält jetzt die optionale `options`-Parameter-Eigenschaft `allowHttpErrors`. Wenn dieser `boolean`-Schalter auf `true` gesetzt ist, ermöglicht er, dass ein Download nach Auftreten eines HTTP-Fehlers fortgesetzt wird. Wenn er auf `false` gesetzt ist, wird ein Download bei Auftreten eines HTTP-Fehlers abgebrochen. Standardwert: `false`. ([Firefox-Bug 1578955](https://bugzil.la/1578955))

#### Entfernungen

- Die Funktionen [`proxy.register()`](/de/docs/Mozilla/Add-ons/WebExtensions/API/proxy) und [`proxy.unregister()`](/de/docs/Mozilla/Add-ons/WebExtensions/API/proxy) wurden entfernt ([Firefox-Bug 1443259](https://bugzil.la/1443259)). {{WebExtAPIRef("proxy.onRequest")}} sollte jetzt zum Handhaben der Proxy-Anfragen verwendet werden.

## Siehe auch

- Hacks-Veröffentlichungspost: [Firefox 71: A year-end arrival](https://hacks.mozilla.org/2019/12/firefox-71-a-year-end-arrival/)

## Ältere Versionen

{{Firefox_for_developers}}
