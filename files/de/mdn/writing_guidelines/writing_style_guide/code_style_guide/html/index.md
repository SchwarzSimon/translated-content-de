---
title: Richtlinien für das Schreiben von HTML-Beispielcode
slug: MDN/Writing_guidelines/Writing_style_guide/Code_style_guide/HTML
l10n:
  sourceCommit: 673746e15e5052c4fe39944f3d93d2e2d3227b3f
---

Die folgenden Richtlinien beschreiben, wie HTML-Beispielcode für MDN Web Docs verfasst werden sollte.

## Allgemeine Richtlinien für HTML-Beispiele

### Format wählen

Meinungen zur richtigen Einrückung, zu Leerzeichen und Zeilenlängen sind seit jeher umstritten. Diskussionen über diese Themen lenken von der Erstellung und Wartung von Inhalten ab.

Auf den MDN Web Docs verwenden wir [Prettier](https://prettier.io/) als Code-Formatter, um den Code-Stil konsistent zu halten (und um Off-Topic-Diskussionen zu vermeiden). Sie können unsere [Konfigurationsdatei](https://github.com/mdn/content/blob/main/.prettierrc.json) konsultieren, um mehr über die aktuellen Regeln zu erfahren, und die [Prettier-Dokumentation](https://prettier.io/docs/index.html) lesen.

Prettier formatiert den gesamten Code und hält den Stil konsistent. Nichtsdestotrotz gibt es ein paar zusätzliche Regeln, die Sie beachten müssen.

## Vollständiges HTML-Dokument

> [!NOTE]
> Die Richtlinien in diesem Abschnitt gelten nur, wenn Sie ein vollständiges HTML-Dokument zeigen müssen. Ein Ausschnitt reicht normalerweise aus, um ein Feature zu demonstrieren. Bei Verwendung des [EmbedLiveSample-Makros](/de/docs/MDN/Writing_guidelines/Page_structures/Code_examples#live_samples) fügen Sie einfach den HTML-Ausschnitt ein; er wird beim Anzeigen automatisch in ein vollständiges HTML-Dokument eingefügt.

### Doctype

Sie sollten den HTML5-Doctype verwenden. Er ist kurz, leicht zu merken und rückwärtskompatibel.

```html example-good
<!doctype html>
```

### Dokumentensprache

Stellen Sie die Dokumentensprache ein, indem Sie das [`lang`](/de/docs/Web/HTML/Global_attributes/lang)-Attribut an Ihrem {{htmlelement("html")}}-Element verwenden:

```html example-good
<html lang="en-US"></html>
```

Dies ist gut für Barrierefreiheit und Suchmaschinen, erleichtert die Lokalisierung von Inhalten und erinnert die Menschen daran, bewährte Praktiken zu verwenden.

### Zeichensatz des Dokuments

Sie sollten auch den Zeichensatz Ihres Dokuments wie folgt definieren:

```html example-good
<meta charset="utf-8" />
```

Verwenden Sie UTF-8, es sei denn, Sie haben einen sehr guten Grund, dies nicht zu tun; es deckt alle Zeichensatzanforderungen ab, unabhängig von der Sprache, die Sie in Ihrem Dokument verwenden.

### Viewport-Meta-Tag

Schließlich sollten Sie immer das Viewport-Meta-Tag in Ihren HTML-{{HTMLElement("head")}} einfügen, um dem Codebeispiel eine bessere Chance zu geben, auf mobilen Geräten zu funktionieren. Sie sollten mindestens das Folgende in Ihr Dokument aufnehmen, das je nach Bedarf später geändert werden kann:

```html example-good
<meta name="viewport" content="width=device-width" />
```

Weitere Details finden Sie unter [Verwenden des Viewport-Meta-Tags zur Steuerung des Layouts auf mobilen Browsern](/de/docs/Web/HTML/Viewport_meta_tag).

## Attribute

Sie sollten alle Attributwerte in doppelte Anführungszeichen setzen. Es ist verlockend, Anführungszeichen wegzulassen, da HTML5 dies erlaubt, aber das Markup ist sauberer und leichter lesbar, wenn Sie sie einschließen. Zum Beispiel ist dies besser:

```html example-good
<img src="images/logo.jpg" alt="A circular globe icon" class="no-border" />
```

… als dies:

```html-nolint example-bad
<img src=images/logo.jpg alt=A circular globe icon class=no-border>
```

Das Weglassen von Anführungszeichen kann auch Probleme verursachen. Im obigen Beispiel wird das `alt`-Attribut als mehrere Attribute interpretiert, da es keine Anführungszeichen gibt, die angeben, dass „A circular globe icon“ ein einzelner Attributwert ist.

## Boolean-Attribute

Geben Sie keine Werte für Boolean-Attribute an (aber geben Sie Werte für {{Glossary("enumerated", "aufgezählte")}} Attribute an); Sie können einfach den Attributnamen schreiben, um ihn festzulegen. Zum Beispiel können Sie schreiben:

```html example-good
<input required />
```

Dies ist perfekt verständlich und funktioniert einwandfrei. Wenn ein Boolean-HTML-Attribut vorhanden ist, ist der Wert true. Während das Hinzufügen eines Wertes funktionieren würde, ist es nicht notwendig und nicht korrekt:

```html example-bad
<input required="required" />
```

## Groß- und Kleinschreibung

Verwenden Sie für alle Element- und Attributnamen/-werte Kleinbuchstaben, da dies ordentlicher aussieht und Sie schneller Markup schreiben können. Zum Beispiel:

```html example-good
<p class="nice">This looks nice and neat</p>
```

```html-nolint example-bad
<P CLASS="WHOA-THERE">Why is my markup shouting?</P>
```

## Klassen- und ID-Namen

Verwenden Sie semantische Klassen-/ID-Namen und trennen Sie mehrere Wörter mit Bindestrichen ({{Glossary("kebab_case", "kebab case")}}). Verwenden Sie nicht {{Glossary("camel_case", "camel case")}}. Zum Beispiel:

```html example-good
<p class="editorial-summary">Blah blah blah</p>
```

```html example-bad
<p class="bigRedBox">Blah blah blah</p>
```

## Zeichenreferenzen

Verwenden Sie keine {{Glossary("character_reference", "Zeichenreferenzen")}} unnötig – verwenden Sie das tatsächliche Zeichen, wo immer möglich (Sie müssen immer noch Zeichen wie spitze Klammern und Anführungszeichen maskieren).

Zum Beispiel könnten Sie einfach schreiben:

```html example-good
<p>© 2018 Me</p>
```

Anstatt:

```html example-bad
<p>&copy; 2018 Me</p>
```

## HTML-Elemente

Es gibt einige Regeln für das Schreiben über HTML-Elemente auf den MDN Web Docs. Die Einhaltung dieser Regeln sorgt für konsistente Beschreibungen der Elemente und ihrer Komponenten und gewährleistet auch die richtige Verlinkung zu detaillierter Dokumentation.

- **Elementnamen**: Verwenden Sie das [`HTMLElement`](https://github.com/mdn/rari/blob/main/crates/rari-doc/src/templ/templs/links/htmlxref.rs)-Makro, das einen Link zur MDN Web Docs-Seite für dieses Element erstellt. Zum Beispiel erzeugt das Schreiben von `\{{HTMLElement("title")}}` "{{HTMLElement("title")}}".
  Wenn Sie keinen Link erstellen möchten, **umschließen Sie den Namen in spitzen Klammern** und verwenden Sie den "Inline Code"-Stil (z. B. `<title>`).
- **Attributnamen**: Verwenden Sie den "Inline Code"-Stil, um Attributnamen im `Code-Schriftart` zu setzen.
  Zusätzlich setzen Sie sie in **`fett`**, wenn das Attribut zusammen mit einer Erklärung, was es bewirkt, erwähnt wird oder wenn es zum ersten Mal auf der Seite verwendet wird.
- **Attributwerte**: Verwenden Sie den "Inline Code"-Stil, um `<code>` auf Attributwerte anzuwenden, und verwenden Sie keine Anführungszeichen um Zeichenfolgenwerte, es sei denn, sie werden durch die Syntax eines Codebeispiels benötigt. Zum Beispiel: "Wenn das `type`-Attribut eines `<input>`-Elements auf `email` oder `tel` gesetzt ist ...".
