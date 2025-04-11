---
title: Firefox 89 für Entwickler
slug: Mozilla/Firefox/Releases/89
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{FirefoxSidebar}}

Dieser Artikel enthält Informationen über die Änderungen in Firefox 89, die Entwickler betreffen werden. Firefox 89 wurde am 1. Juni 2021 veröffentlicht.

> [!NOTE]
> Siehe auch [Looking fine with Firefox 89](https://hacks.mozilla.org/2021/06/looking-fine-with-firefox-89/) auf Mozilla Hacks.

## Änderungen für Webentwickler

### Entwicklertools

_Keine Änderungen._

### HTML

_Keine Änderungen._

### CSS

- Das {{cssxref("@media/forced-colors","forced-colors")}} Media-Feature wurde implementiert ([Firefox-Bug 1659511](https://bugzil.la/1659511)).
- Die `@font-face` Deskriptoren {{cssxref("@font-face/ascent-override", "ascent-override")}}, {{cssxref("@font-face/descent-override", "descent-override")}}, und {{cssxref("@font-face/line-gap-override", "line-gap-override")}} wurden implementiert ([Firefox-Bug 1681691](https://bugzil.la/1681691) und [Firefox-Bug 1704494](https://bugzil.la/1704494)).
- Die `type()` Funktion für {{cssxref("image/image-set")}} wurde implementiert ([Firefox-Bug 1695404](https://bugzil.la/1695404)).
- Die CSS-Eigenschaft {{cssxref("aspect-ratio")}} wird nun unterstützt ([Firefox-Bug 1672073](https://bugzil.la/1672073)).

### JavaScript

- `Top-level await` ist nun standardmäßig aktiviert ([Firefox-Bug 1681046](https://bugzil.la/1681046)).
- [ArrayBuffer](/de/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) können jetzt mit einer Länge größer als 2GB-1 (bis zu 8GB) auf 64-Bit-Systemen erstellt werden ([Firefox-Bug 1703505](https://bugzil.la/1703505)).

### HTTP

_Keine Änderungen._

### APIs

#### DOM

- [`PerformanceEventTiming`](/de/docs/Web/API/PerformanceEventTiming) ist nun standardmäßig aktiviert ([Firefox-Bug 1701029](https://bugzil.la/1701029)).
- Der Inhalt von {{htmlelement("input")}} und {{htmlelement("textarea")}} Elementen kann nun standardmäßig mit [`Document.execCommand()`](/de/docs/Web/API/Document/execCommand) Befehlen manipuliert werden, wobei die Bearbeitungshistorie erhalten bleibt. Dies bietet Parität mit anderen Browsern, ohne dass [`contentEditable`](/de/docs/Web/HTML/Reference/Global_attributes/contenteditable) oder umfangreiche Umgehungslösungen erforderlich sind ([Firefox-Bug 1220696](https://bugzil.la/1220696)).

#### Entfernungen

- Die folgenden Sensorevents und ihre zugehörigen Handler wurden entfernt (hauptsächlich für eine bessere Kompatibilität mit anderen großen Browser-Engines und zur Lösung von Bedenken hinsichtlich Datenschutzlecks):

  - `DeviceProximityEvent` und sein Event-Handler `window.ondeviceproximity` ([Firefox-Bug 1699707](https://bugzil.la/1699707)).
  - `UserProximityEvent` und sein Event-Handler `window.onuserproximity` ([Firefox-Bug 1699707](https://bugzil.la/1699707)).
  - `DeviceLightEvent` und sein Event-Handler `window.ondevicelight` ([Firefox-Bug 1701824](https://bugzil.la/1701824)).

### WebDriver-Konformität (Marionette)

#### Entfernungen

- Die `rotatable` Fähigkeit, die nicht Teil der WebDriver-Spezifikation ist, wird nicht mehr verwendet ([Firefox-Bug 1697630](https://bugzil.la/1697630)).

## Änderungen für Add-on-Entwickler

- [Dynamische JS-Modulimporte](/de/docs/Web/JavaScript/Guide/Modules#dynamic_module_loading) funktionieren nun in WebExtension-Content-Skripten ([Firefox-Bug 1536094](https://bugzil.la/1536094)).
- Erweiterungsressourcen, die in [web_accessible_resources](/de/docs/Mozilla/Add-ons/WebExtensions/manifest.json/web_accessible_resources) aufgeführt sind, können unabhängig vom CORS-Modus der Anfrage geladen werden ([Firefox-Bug 1694679](https://bugzil.la/1694679)).
- Das UI von Firefox wurde neu gestaltet, was sich auf die Nutzung der {{WebExtAPIRef("theme")}} API auswirkt. Die Eigenschaften `tab_background_separator` und `toolbar_field_separator` werden nicht mehr unterstützt. Die Eigenschaften `tab_line` und `toolbar_vertical_separator` werden anders funktionieren. Weitere Informationen finden Sie unter [Änderungen an themengestaltbaren Bereichen von Firefox in Version 89](https://blog.mozilla.org/addons/2021/04/19/changes-to-themeable-areas-of-firefox-in-version-89/).
- Die {{WebExtAPIRef("pageAction")}} Schaltfläche kann nicht mehr an die Adressleiste angeheftet oder von dieser gelöst werden, da das Drei-Punkte-Menü standardmäßig nicht mehr sichtbar ist ([Firefox-Bug 1691454](https://bugzil.la/1691454)). Daher hat die `pinned` Eigenschaft des [`page_action`](/de/docs/Mozilla/Add-ons/WebExtensions/manifest.json/page_action) Manifest-Schlüssels keine Wirkung mehr ([Firefox-Bug 1703537](https://bugzil.la/1703537)).
- Der Kontextmenüeintrag "Remove from Address Bar" wurde von der {{WebExtAPIRef("pageAction")}} Schaltfläche entfernt ([Firefox-Bug 1704474](https://bugzil.la/1704474)). Für Alternativen zu dieser Funktionalität siehe [Firefox-Bug 1712556](https://bugzil.la/1712556).

## Ältere Versionen

{{Firefox_for_developers}}
