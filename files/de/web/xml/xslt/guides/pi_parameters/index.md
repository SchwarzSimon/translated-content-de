---
title: PI-Parameter
slug: Web/XML/XSLT/Guides/PI_Parameters
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

XSLT unterstützt das Konzept, Parameter an ein Stylesheet zu übergeben, wenn dieses ausgeführt wird. Dies war schon seit einiger Zeit möglich, wenn der [`XSLTProcessor`](/de/docs/Web/API/XSLTProcessor) in JavaScript verwendet wird. Bei der Verwendung einer `<?xml-stylesheet?>` Verarbeitungshinweis (PI) gab es jedoch bisher keine Möglichkeit, Parameter bereitzustellen.

Um dieses Problem zu lösen, wurden in [Firefox 2](/de/docs/Mozilla/Firefox/Releases/2) zwei neue PIs implementiert (siehe unten [Unterstützte Versionen](#mögliche_zukünftige_entwicklungen) für Details), `<?xslt-param?>` und `<?xslt-param-namespace?>`. Beide PIs können "Pseudo-Attribute" enthalten, ähnlich wie der `xml-stylesheet` PI.

Das folgende Dokument übergibt die beiden Parameter "color" und "size" an das Stylesheet "style.xsl".

```xml
<?xslt-param name="color" value="blue"?>
<?xslt-param name="size" select="2"?>
<?xml-stylesheet type="text/xsl" href="style.xsl"?>
```

Beachten Sie, dass diese PIs keinen Effekt haben, wenn die Transformation mithilfe des `XSLTProcessor`-Objekts in JavaScript durchgeführt wird.

### Verarbeitungshinweise

Die Attribute in den `xslt-param` und `xslt-param-namespace` PIs werden unter Verwendung der Regeln aus [xml-stylesheet](https://www.w3.org/TR/xml-stylesheet/) ausgewertet. Alle nicht erkannten Attribute müssen ignoriert werden. Das Parsen eines Attributs darf nicht aufgrund eines nicht erkannten Attributs fehlschlagen, solange dieses Attribut der Syntax in `xml-stylesheet` folgt.

Sowohl die `xslt-param`- als auch die `xslt-param-namespace`-PIs müssen im Prolog des Dokuments erscheinen, d.h. vor dem ersten Element-Tag. Alle PIs im Prolog müssen beachtet werden, sowohl die, die vor als auch die, die nach den `xml-stylesheet` PIs auftreten.

Wenn es mehrere `xml-stylesheet` PIs gibt, gelten die Parameter für alle Stylesheets, da gemäß der XSLT-Spezifikation alle Stylesheets in ein einziges Stylesheet importiert werden. Beachten Sie, dass mehrere `xml-stylesheet` XSLT PIs derzeit in Firefox nicht unterstützt werden.

#### xslt-param

Der `xslt-param` PI unterstützt 4 Attribute:

- `name`
  - : Der lokale Namensanteil des Parameternamens. Es wird keine Syntaxprüfung auf das Attribut durchgeführt; wenn es jedoch kein gültiger [NCName](https://www.w3.org/TR/REC-xml-names/#NT-NCName) ist, wird es nie mit einem Parameter im Stylesheet übereinstimmen.
- `namespace`
  - : Der Namensraum des Parameternamens. Es wird keine Syntaxprüfung auf das Attribut durchgeführt.
- `value`
  - : Enthält den Zeichenfolgenwert für den Parameter. Der Wert des Attributs wird als Wert für den Parameter verwendet. Der Datentyp ist immer _string_.
- `select`
  - : Ein [XPath](/de/docs/Web/XML/XPath)-Ausdruck für den Parameter. Der Wert des Attributs wird als XPath-Ausdruck geparst. Das Ergebnis der Auswertung des Ausdrucks wird als Wert für den Parameter verwendet.

Wenn das `name`-Attribut fehlt oder leer ist, wird der PI ignoriert.

Wenn das `namespace`-Attribut fehlt oder leer ist, wird der leere Namensraum verwendet.

Es ist kein Fehler, einen Parameternamen anzugeben, der im Stylesheet nicht existiert (oder der im Stylesheet eine Variable ist). Der PI wird ignoriert.

Wenn sowohl `value` als auch `select` vorhanden sind oder wenn weder `value` noch `select` vorhanden sind, wird der PI ignoriert.

Beachten Sie, dass `value="..."` nicht streng gleich `select="'...'"` ist, da der Wert sowohl Apostroph als auch Anführungszeichen enthalten kann.

##### Beispiele

Setzen Sie den Parameter 'color' auf die Zeichenkette 'red':

```xml
<?xslt-param name="color" value="red"?>
```

Setzen Sie den Parameter 'columns' auf die Zahl 2:

```xml
<?xslt-param name="columns" select="2"?>
```

Setzen Sie den Parameter 'books' auf eine Knotenmengen, die alle `<book>`-Elemente im leeren Namensraum enthält:

```xml
<?xslt-param name="books" select="//book"?>
```

Setzen Sie den Parameter 'show-toc' auf den booleschen Wert `true`:

```xml
<?xslt-param name="show-toc" select="true()"?>
```

##### Der Kontext des select-Attributs

Der folgende Kontext wird verwendet, um den Ausdruck im **select**-Attribut zu parsen und auszuwerten.

- Der Kontextknoten ist der Knoten, der als initialer aktueller Knoten verwendet wird, wenn das Stylesheet ausgeführt wird.
- Die Kontextposition ist die Position des Kontextknotens in der initialen aktuellen Knotenliste, die beim Ausführen des Stylesheets verwendet wird.
- Die Kontextgröße ist die Größe der initialen aktuellen Knotenliste, die beim Ausführen des Stylesheets verwendet wird.
- Es sind keine Variablen verfügbar.
- Die Funktionsbibliothek ist die Standard-XPath-Funktionsbibliothek.
- Die Namensraumdeklarationen werden durch die `xslt-param-namespace` PIs bestimmt, siehe unten.

Wenn das **select**-Attribut nicht geparst oder ausgeführt werden kann, wird der PI ignoriert (insbesondere erfolgt kein Fallback auf das **value**-Attribut).

#### xslt-param-namespace

Der `xslt-param-namespace` verwendet zwei Attribute:

- prefix
  - : Das Präfix, das abgebildet wird.
- namespace
  - : Der Namensraum, auf den das Präfix abgebildet wird.

Ein `xslt-param-namespace` PI beeinflusst den Ausdruck im **select**-Attribut für alle `xslt-param`s, die dem PI folgen. Dies gilt auch, wenn es andere Knoten wie Kommentare oder andere PIs zwischen dem `xslt-param-namespace` und den `xslt-param` PIs gibt.

Es ist kein Fehler, dass mehrere PIs dasselbe Präfix verwenden, jeder neue PI ändert nur, auf welchen Namensraum das Präfix abgebildet wird.

Wenn **prefix** fehlt, leer ist oder einem ungültigen NCName entspricht, wird der PI ignoriert.

Wenn **namespace** fehlt, wird der PI ignoriert. Wenn **namespace** leer ist, wird die Präfix-Abbildung entfernt.

##### Beispiele

Setzen Sie den Parameter 'books' auf eine Knotenmengen, die alle `<book>`-Elemente im Namensraum `http://www.example.org/myNamespace` enthält:

```xml
<?xslt-param-namespace prefix="my" namespace="http://www.example.org/myNamespace"?>
<?xslt-param name="books" select="//my:book"?>
```

### Unterstützte Versionen

Unterstützt seit Firefox 2.0.0.1. Das **value**-Attribut wird in Firefox 2 unterstützt, aber das **select**-Attribut führt in der 2.0-Version bei einigen Ausdrücken zu Abstürzen.

### Mögliche zukünftige Entwicklungen

Sollten wir erlauben, dass in Ausdrücken beliebige XSLT-Funktionen verwendet werden? `document()` scheint nützlich zu sein, aber es scheint schwierig, die Invariante aufrechtzuerhalten, dass `generate-id()` für dasselbe Dokument denselben String erzeugen sollte.

Wie wäre es, URL-Parameter im XSLT-Stylesheet abzufragen? Z.B. sie an bestimmte \<xsl:param>-Elemente zu übergeben.
