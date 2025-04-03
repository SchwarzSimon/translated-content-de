---
title: "@import"
slug: Web/CSS/@import
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{CSSRef}}

Die **`@import`** [CSS](/de/docs/Web/CSS) [At-Regel](/de/docs/Web/CSS/CSS_syntax/At-rule) wird verwendet, um Stilregeln aus anderen gültigen Stylesheets zu importieren. Eine `@import`-Regel _muss_ am Anfang des Stylesheets definiert werden, vor jeder anderen At-Regel (außer [@charset](/de/docs/Web/CSS/@charset) und [@layer](/de/docs/Web/CSS/@layer)) und Stilangaben, sonst wird sie ignoriert.

## Syntax

```css
@import url;
@import url layer;
@import url layer(layer-name);
@import url layer(layer-name) supports(supports-condition);
@import url layer(layer-name) supports(supports-condition) list-of-media-queries;
@import url layer(layer-name) list-of-media-queries;
@import url supports(supports-condition);
@import url supports(supports-condition) list-of-media-queries;
@import url list-of-media-queries;
```

wo:

- _url_
  - : Ist ein {{CSSxRef("string")}} oder ein {{cssxref("url_value", "&lt;url&gt;")}}-Typ, der den Speicherort der zu importierenden Ressource darstellt. Die URL kann absolut oder relativ sein.
- _list-of-media-queries_
  - : Ist eine durch Kommas getrennte Liste von [Media Queries](/de/docs/Web/CSS/CSS_media_queries/Using_media_queries), die die medienspezifischen Bedingungen für die Anwendung der in der verknüpften URL definierten CSS-Regeln spezifizieren. Wenn der Browser keine dieser Abfragen unterstützt, lädt er die verknüpfte Ressource nicht.
- _layer-name_
  - : Ist der Name einer [Kaskadenschicht](/de/docs/Web/CSS/@layer), in die die Inhalte der verknüpften Ressource importiert werden.
- _supports-condition_
  - : Gibt die Funktion(en) an, die der Browser unterstützen muss, damit das Stylesheet importiert wird. Wenn der Browser nicht den in der _supports-condition_ angegebenen Bedingungen entspricht, kann es sein, dass er das verknüpfte Stylesheet nicht abruft, und selbst wenn es über einen anderen Pfad heruntergeladen wird, wird es nicht geladen. Die Syntax von `supports()` ist nahezu identisch mit der, die in {{CSSxRef("@supports")}} beschrieben ist, und dieses Thema kann als umfassendere Referenz verwendet werden.

Verwenden Sie `@import` zusammen mit dem Schlüsselwort `layer` oder der Funktion `layer()`, um externe Stylesheets (von Frameworks, Widget-Stylesheets, Bibliotheken usw.) in Schichten zu importieren.

## Beschreibung

Importierte Regeln müssen vor allen anderen Regeltypen kommen, außer {{CSSxRef("@charset")}}-Regeln und Schichtenerstellenden [`@layer`](/de/docs/Web/CSS/@layer)-Anweisungen.

```css example-bad
* {
  margin: 0;
  padding: 0;
}
/* more styles */
@import url("my-imported-styles.css");
```

Da die `@import`-At-Regel nach den Stilen deklariert ist, ist sie ungültig und wird daher ignoriert.

```css example-good
@import url("my-imported-styles.css");
* {
  margin: 0;
  padding: 0;
}
/* more styles */
```

Die `@import`-Regel ist keine [verschachtelte Anweisung](/de/docs/Web/CSS/CSS_syntax/Syntax#nested_statements). Daher kann sie nicht innerhalb von [bedingten Gruppen-At-Regeln](/de/docs/Web/CSS/CSS_conditional_rules#at-rules) verwendet werden.

Damit {{Glossary("user_agent", "Benutzeragenten")}} das Abrufen von Ressourcen für nicht unterstützte Medientypen vermeiden können, können Autoren medienabhängige Importbedingungen spezifizieren. Diese bedingten Importe spezifizieren durch Kommas getrennte [Media Queries](/de/docs/Web/CSS/CSS_media_queries/Using_media_queries) nach der URL. In Abwesenheit einer Media Query ist der Import nicht an das verwendete Medium gebunden. Die Angabe von `all` für die `list-of-media-queries` hat denselben Effekt.

Ebenso können Benutzeragenten die `supports()`-Funktion in einer `@import`-At-Regel verwenden, um Ressourcen nur dann abzurufen, wenn ein bestimmter Funktionssatz (oder nicht) unterstützt wird. Dies ermöglicht es Autoren, von neu eingeführten CSS-Funktionen zu profitieren, während sie gleichzeitig anmutige Rückfallebenen für ältere Browserversionen bieten. Beachten Sie, dass die Bedingungen in der `supports()`-Funktion einer `@import`-At-Regel in JavaScript unter Verwendung von [`CSSImportRule.supportsText`](/de/docs/Web/API/CSSImportRule/supportsText) abgerufen werden können.

Die `@import`-Regel kann auch verwendet werden, um eine [Kaskadenschicht](/de/docs/Web/CSS/@layer) zu erstellen, indem Regeln aus einer verknüpften Ressource importiert werden. Regeln können auch in eine vorhandene Kaskadenschicht importiert werden. Das Schlüsselwort `layer` oder die Funktion `layer()` wird für diesen Zweck mit `@import` verwendet. Deklarationen in Stilregeln aus importierten Stylesheets interagieren mit der Kaskade, als wären sie wörtlich an der Stelle des Imports in das Stylesheet geschrieben.

## Formale Syntax

{{csssyntax}}

## Beispiele

### Importieren von CSS-Regeln

```css
@import "custom.css";
@import url("chrome://communicator/skin/");
```

Die beiden obigen Beispiele zeigen, wie der _url_ als `<string>` und als `url()`-Funktion angegeben wird.

### Importieren von CSS-Regeln, abhängig von Media Queries

```css
@import url("fine-print.css") print;
@import url("bluish.css") print, screen;
@import "common.css" screen;
@import url("landscape.css") screen and (orientation: landscape);
```

Die `@import`-Regeln in den obigen Beispielen zeigen medienspezifische Bedingungen, die erfüllt sein müssen, bevor die verknüpften CSS-Regeln angewendet werden. Zum Beispiel wird die letzte `@import`-Regel das Stylesheet `landscape.css` nur auf einem Bildschirmgerät im Querformat laden.

### Importieren von CSS-Regeln, abhängig von der Feature-Unterstützung

```css
@import url("gridy.css") supports(display: grid) screen and (max-width: 400px);
@import url("flexy.css") supports((not (display: grid)) and (display: flex))
  screen and (max-width: 400px);
```

Die obigen `@import`-Regeln veranschaulichen, wie Sie ein Layout importieren könnten, das ein Raster verwenden, wenn `display: grid` unterstützt wird, und ansonsten CSS importieren, das `display: flex` verwendet. Während Sie nur eine `supports()`-Anweisung haben können, können Sie jede Anzahl von Feature-Checks mit `not`, `and` und `or` kombinieren. Sie müssen jedoch Klammern verwenden, um die Priorität zu definieren, wenn Sie sie mischen, z.B. `supports((..) or (..) and not (..))` ist ungültig, aber `supports((..) or ((..) and (not (..))))` ist gültig. Beachten Sie, dass, wenn Sie nur eine einzelne Deklaration haben, Sie sie nicht in zusätzliche Klammern einschließen müssen: Dies wird im ersten obigen Beispiel gezeigt.

Die obigen Beispiele zeigen Unterstützungsbedingungen unter Verwendung der grundlegenden Deklarationssyntax. Sie können auch CSS-Funktionen in `supports()` angeben, und es wird zu `true` ausgewertet, wenn sie unterstützt werden und im Benutzeragenten ausgewertet werden können. Zum Beispiel zeigt der folgende Code eine `@import`, die von [Kindkombinatoren](/de/docs/Web/CSS/Child_combinator) (`selector()`) und der `font-tech()`-Funktion abhängig ist:

```css
@import url("whatever.css")
supports((selector(h2 > p)) and (font-tech(color-COLRv1)));
```

### Importieren von CSS-Regeln in eine Kaskadenschicht

```css
@import "theme.css" layer(utilities);
```

Im obigen Beispiel wird eine Kaskadenschicht namens `utilities` erstellt, und sie wird Regeln aus dem importierten Stylesheet `theme` enthalten.

```css
@import url(headings.css) layer(default);
@import url(links.css) layer(default);

@layer default {
  audio[controls] {
    display: block;
  }
}
```

Im obigen Beispiel kaskadieren die Regeln in den Stylesheets `headings.css` und `links.css` innerhalb derselben Schicht wie die `audio[controls]`-Regel.

```css
@import "theme.css" layer();
@import "style.css" layer;
```

Dies ist ein Beispiel für die Erstellung von zwei separaten unbenannten Kaskadenschichten und das Importieren der verknüpften Regeln in jede einzeln. Eine ohne Namen deklarierte Kaskadenschicht ist eine unbenannte Kaskadenschicht. Unbenannte Kaskadenschichten werden beim Erstellen finalisiert: Sie bieten keine Mittel zum Neuordnen oder Hinzufügen von Stilen und können von außen nicht referenziert werden.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{CSSxRef("@media")}}
- {{CSSxRef("@supports")}}
- [CSS-Kaskadierung und Vererbung](/de/docs/Web/CSS/CSS_cascade) Modul
- [CSS-At-Regel-Funktionen](/de/docs/Web/CSS/CSS_syntax/At-rule_functions)
