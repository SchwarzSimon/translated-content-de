---
title: "<img>: Das Bildelement"
slug: Web/HTML/Element/img
l10n:
  sourceCommit: 27bceead8e9b1fe9c92df0fa5e418f81bd5b9fdf
---

{{HTMLSidebar}}

Das **`<img>`** [HTML](/de/docs/Web/HTML)-Element bettet ein Bild in das Dokument ein.

{{EmbedInteractiveExample("pages/tabbed/img.html", "tabbed-standard")}}

Das obige Beispiel zeigt die Verwendung des `<img>`-Elements:

- Das `src`-Attribut ist **erforderlich** und enthält den Pfad zu dem Bild, das Sie einbetten möchten.
- Das `alt`-Attribut enthält einen textlichen Ersatz für das Bild, der obligatorisch und **ungemein nützlich** für die Zugänglichkeit ist — Screenreader lesen den Attributwert ihren Nutzern vor, damit sie verstehen, was das Bild bedeutet. Alternativtext wird auch auf der Seite angezeigt, wenn das Bild aus irgendeinem Grund nicht geladen werden kann: beispielsweise bei Netzwerkfehlern, Inhaltsblockierungen oder Linkverfall.

Es gibt viele weitere Attribute, um verschiedene Zwecke zu erreichen:

- [Referrer](/de/docs/Web/HTTP/Headers/Referrer-Policy)/{{Glossary("CORS", "CORS")}}-Kontrolle für Sicherheit und Datenschutz: siehe [`crossorigin`](#crossorigin) und [`referrerpolicy`](#referrerpolicy).
- Verwenden Sie sowohl [`width`](#width) als auch [`height`](#height), um die intrinsische Größe des Bildes festzulegen, damit es vor dem Laden Platz beansprucht, um Layoutverschiebungen des Inhalts zu mindern.
- Hinweise für responsive Bilder mit [`sizes`](#sizes) und [`srcset`](#srcset) (siehe auch das {{htmlelement("picture")}}-Element und unser [Responsive images](/de/docs/Web/HTML/Responsive_images)-Tutorial).

## Unterstützte Bildformate

Der HTML-Standard legt nicht fest, welche Bildformate unterstützt werden sollen, sodass {{Glossary("user_agent", "Benutzeragenten")}} unterschiedliche Formate unterstützen können.

> [!NOTE]
> Der [Leitfaden für Bilddateiformate und -typen](/de/docs/Web/Media/Guides/Formats/Image_types) bietet umfassende Informationen zu Bildformaten und deren Unterstützung in Webbrowsern.
> Dieser Abschnitt ist nur eine Zusammenfassung!

Die Bilddateiformate, die im Web am häufigsten verwendet werden, sind:

- [APNG (Animated Portable Network Graphics)](/de/docs/Web/Media/Guides/Formats/Image_types#apng_animated_portable_network_graphics) — Gute Wahl für verlustfreie Animationssequenzen (GIF ist weniger leistungsfähig)
- [AVIF (AV1 Image File Format)](/de/docs/Web/Media/Guides/Formats/Image_types#avif_image) — Gute Wahl sowohl für Bilder als auch für animierte Bilder aufgrund der hohen Leistung.
- [GIF (Graphics Interchange Format)](/de/docs/Web/Media/Guides/Formats/Image_types#gif_graphics_interchange_format) — Gute Wahl für _einfache_ Bilder und Animationen.
- [JPEG (Joint Photographic Expert Group image)](/de/docs/Web/Media/Guides/Formats/Image_types#jpeg_joint_photographic_experts_group_image) — Gute Wahl für verlustbehaftete Komprimierung von Standbildern (derzeit am beliebtesten).
- [PNG (Portable Network Graphics)](/de/docs/Web/Media/Guides/Formats/Image_types#png_portable_network_graphics) — Gute Wahl für verlustfreie Komprimierung von Standbildern (etwas bessere Qualität als JPEG).
- [SVG (Scalable Vector Graphics)](/de/docs/Web/Media/Guides/Formats/Image_types#svg_scalable_vector_graphics) — Vektor-Bildformat. Nutzen Sie es für Bilder, die in verschiedenen Größen genau gezeichnet werden müssen.
- [WebP (Web Picture format)](/de/docs/Web/Media/Guides/Formats/Image_types#webp_image) — Ausgezeichnete Wahl sowohl für Bilder als auch für animierte Bilder.

Formate wie [WebP](/de/docs/Web/Media/Guides/Formats/Image_types#webp_image) und [AVIF](/de/docs/Web/Media/Guides/Formats/Image_types#avif_image) werden empfohlen, da sie sowohl für Stand- als auch für animierte Bilder viel besser abschneiden als PNG, JPEG und GIF.

SVG bleibt das empfohlene Format für Bilder, die in verschiedenen Größen exakt gezeichnet werden müssen.

## Bildladefehler

Wenn beim Laden oder Rendern eines Bildes ein Fehler auftritt und ein `onerror` Event-Handler für das [`error`](/de/docs/Web/API/HTMLElement/error_event)-Ereignis festgelegt wurde, wird dieser Event-Handler aufgerufen. Dies kann in mehreren Situationen passieren, unter anderem:

- Das `src`-Attribut ist leer (`""`) oder `null`.
- Die `src` {{Glossary("URL", "URL")}} ist identisch mit der URL der Seite, die der Benutzer gerade besucht.
- Das Bild ist in irgendeiner Weise beschädigt, die verhindert, dass es geladen wird.
- Die Metadaten des Bildes sind so beschädigt, dass es unmöglich ist, seine Dimensionen abzurufen, und es wurden keine Dimensionen in den Attributen des `<img>`-Elements angegeben.
- Das Bild ist in einem Format, das vom {{Glossary("user_agent", "Benutzeragenten")}} nicht unterstützt wird.

## Attribute

Dieses Element umfasst die [globalen Attribute](/de/docs/Web/HTML/Global_attributes).

- [`alt`](/de/docs/Web/API/HTMLImageElement/alt#usage_notes)

  - : Definiert Text, der das Bild auf der Seite ersetzen kann.

    > [!NOTE]
    > Browser zeigen nicht immer Bilder an. Es gibt eine Reihe von Situationen, in denen ein Browser möglicherweise keine Bilder anzeigt, wie zum Beispiel:
    >
    > - Nicht-visuelle Browser (wie solche, die von Menschen mit Sehbehinderungen verwendet werden)
    > - Der Benutzer entscheidet sich, keine Bilder anzuzeigen (um Bandbreite zu sparen, aus Datenschutzgründen)
    > - Das Bild ist ungültig oder ein [nicht unterstützter Typ](#unterstützte_bildformate)
    >
    > In diesen Fällen kann der Browser das Bild durch den Text im `alt`-Attribut des Elements ersetzen. Aus diesen und anderen Gründen sollten Sie, wann immer möglich, einen nützlichen Wert für `alt` angeben.

    Das Festlegen dieses Attributs auf einen leeren String (`alt=""`) zeigt an, dass dieses Bild _nicht_ ein wesentlicher Bestandteil des Inhalts ist (es ist Dekoration oder ein Tracking-Pixel) und dass nicht-visuelle Browser es vom {{Glossary("Engine/Rendering", "Rendering")}} auslassen können. Visuelle Browser verbergen auch das kaputte Bildsymbol, wenn das `alt`-Attribut leer ist und das Bild nicht angezeigt werden konnte.

    Dieses Attribut wird auch verwendet, wenn das Bild in Text kopiert oder beim Speichern eines verknüpften Bildes zu einem Lesezeichen verwendet wird.

- `attributionsrc` {{experimental_inline}}

  - : Gibt an, dass Sie möchten, dass der Browser einen {{httpheader("Attribution-Reporting-Eligible")}}-Header zusammen mit der Bildanfrage sendet.

    Auf der Serverseite wird dies verwendet, um das Senden eines {{httpheader("Attribution-Reporting-Register-Source")}}- oder {{httpheader("Attribution-Reporting-Register-Trigger")}}-Headers in der Antwort auszulösen, um eine bildbasierte [Attributionsquelle](/de/docs/Web/API/Attribution_Reporting_API/Registering_sources#html-based_event_sources) oder einen [Attributionstrigger](/de/docs/Web/API/Attribution_Reporting_API/Registering_triggers#html-based_attribution_triggers) zu registrieren. Welcher Antwort-Header zurückgesendet werden sollte, hängt vom Wert des `Attribution-Reporting-Eligible`-Headers ab, der die Registrierung ausgelöst hat.

    Die entsprechende Quellen- oder Triggerveranstaltung wird ausgelöst, sobald der Browser die Antwort mit der Bilddatei erhält.

    > [!NOTE]
    > Details finden Sie in der [Attribution Reporting API](/de/docs/Web/API/Attribution_Reporting_API).

    Es gibt zwei Versionen dieses Attributs, die Sie festlegen können:

    - Boolean, d.h. nur der Name `attributionsrc`. Dies gibt an, dass der {{httpheader("Attribution-Reporting-Eligible")}}-Header an denselben Server gesendet werden soll, auf den das `src`-Attribut verweist. Dies ist in Ordnung, wenn Sie die Registrierung der Attributionsquelle oder des Triggers auf demselben Server behandeln. Beim Registrieren eines Attributionstriggers ist diese Eigenschaft optional, und ein boolescher Wert wird verwendet, wenn sie ausgelassen wird.
    - Wert, der eine oder mehrere URLs enthält, zum Beispiel:

    ```html
    <img
      src="image-file.png"
      alt="My image file description"
      attributionsrc="https://a.example/register-source
                         https://b.example/register-source" />
    ```

    Dies ist nützlich in Fällen, in denen die angeforderte Ressource nicht auf einem Server liegt, den Sie kontrollieren, oder Sie die Registrierung der Attributionsquelle einfach auf einem anderen Server durchführen möchten. In diesem Fall können Sie eine oder mehrere URLs als Wert von `attributionsrc` angeben. Wenn die Ressourcenanforderung auftritt, wird der {{httpheader("Attribution-Reporting-Eligible")}}-Header an die in `attributionSrc` angegebenen URL(s) zusätzlich zum Ressourcenursprung gesendet. Diese URLs können dann mit einem {{httpheader("Attribution-Reporting-Register-Source")}}- oder {{httpheader("Attribution-Reporting-Register-Trigger")}}-Header entsprechend antworten, um die Registrierung abzuschließen.

    > [!NOTE]
    > Das Angeben mehrerer URLs bedeutet, dass mehrere Attributionsquellen für dieselbe Funktion registriert werden können. Sie könnten zum Beispiel verschiedene Kampagnen haben, deren Erfolg Sie messen möchten, was das Generieren unterschiedlicher Berichte zu unterschiedlichen Daten erfordert.

- [`crossorigin`](/de/docs/Web/HTML/Attributes/crossorigin)

  - : Gibt an, ob das Abrufen des Bildes mit einer {{Glossary("CORS", "CORS")}}-Anfrage erfolgen muss. Bilddaten von einem [CORS-fähigen Bild](/de/docs/Web/HTML/CORS_enabled_image), das über eine CORS-Anfrage zurückgegeben wird, können im {{HTMLElement("canvas")}}-Element wiederverwendet werden, ohne als "[verfälscht](/de/docs/Web/HTML/CORS_enabled_image#security_and_tainted_canvases)" markiert zu werden.

    Wenn das `crossorigin`-Attribut _nicht_ angegeben wird, wird eine Nicht-CORS-Anfrage gesendet (ohne den {{httpheader("Origin")}}-Request-Header), und der Browser markiert das Bild als verfälscht und beschränkt den Zugriff auf seine Bilddaten, was seine Nutzung in {{HTMLElement("canvas")}}-Elementen verhindert.

    Wenn das `crossorigin`-Attribut _angegeben_ wird, wird eine CORS-Anfrage gesendet (mit dem {{httpheader("Origin")}}-Request-Header); Wenn der Server jedoch nicht zustimmt, den Cross-Origin-Zugriff auf die Bilddaten von der Ursprungsseite zuzulassen (indem er keinen {{httpheader("Access-Control-Allow-Origin")}}-Response-Header sendet, oder indem er die Ursprungsseite nicht in einen {{httpheader("Access-Control-Allow-Origin")}}-Response-Header aufnimmt, den er sendet), blockiert der Browser das Laden des Bildes und protokolliert einen CORS-Fehler in der Devtools-Konsole.

    Erlaubte Werte:

    - `anonymous`
      - : Eine CORS-Anfrage wird ohne Anmeldedaten gesendet (dh. keine {{Glossary("cookie", "Cookies")}}, [X.509-Zertifikate](https://datatracker.ietf.org/doc/html/rfc5280) oder {{httpheader("Authorization")}}-Request-Header).
    - `use-credentials`
      - : Die CORS-Anfrage wird mit Anmeldedaten gesendet (d.h. Cookies, X.509-Zertifikate und der `Authorization`-Request-Header). Wenn der Server nicht einwilligt, Anmeldedaten mit der Ursprungsseite zu teilen (indem er den Header `Access-Control-Allow-Credentials: true` zurücksendet), markiert der Browser das Bild als verfälscht und beschränkt den Zugriff auf seine Bilddaten.

    Wenn das Attribut einen ungültigen Wert hat, behandeln Browser dies so, als ob der Wert `anonymous` verwendet würde. Siehe [CORS-Einstellungsattribute](/de/docs/Web/HTML/Attributes/crossorigin) für zusätzliche Informationen.

- `decoding`

  - : Dieses Attribut gibt dem Browser einen Hinweis darauf, ob er die Bilddekodierung zusammen mit dem Rendern der anderen DOM-Inhalte in einem einzigen Präsentationsschritt durchführen sollte, der "korrekter" aussieht (`sync`), oder zuerst die anderen DOM-Inhalte rendern und präsentieren und dann das Bild dekodieren und später präsentieren sollte (`async`). In der Praxis bedeutet `async`, dass der nächste Paint nicht darauf wartet, dass das Bild dekodiert wird.

    Es ist oft schwierig, einen wahrnehmbaren Effekt bei der Verwendung von `decoding` bei statischen `<img>`-Elementen zu erkennen. Sie werden wahrscheinlich zunächst als leere Bilder gerendert, während die Bilddateien abgerufen werden (entweder aus dem Netzwerk oder aus dem Cache) und dann unabhängig verarbeitet werden. Daher ist die "Synchronisierung" von Inhaltsaktualisierungen weniger offensichtlich. Das Blockieren des Renderings während der Dekodierung, auch wenn es oft ziemlich klein ist, _kann_ gemessen werden — selbst wenn es mit dem menschlichen Auge schwer zu beobachten ist. Siehe [Was macht das Bild-Dekodierungsattribut tatsächlich?](https://www.tunetheweb.com/blog/what-does-the-image-decoding-attribute-actually-do/) für eine detailliertere Analyse (tunetheweb.com, 2023).

    Die Verwendung unterschiedlicher `decoding`-Typen kann zu deutlicheren Unterschieden führen, wenn `<img>`-Elemente dynamisch über JavaScript in das DOM eingefügt werden — siehe [`HTMLImageElement.decoding`](/de/docs/Web/API/HTMLImageElement/decoding) für weitere Details.

    Erlaubte Werte:

    - `sync`
      - : Dekodiere das Bild synchron zusammen mit dem Rendern der anderen DOM-Inhalte und präsentiere alles zusammen.
    - `async`
      - : Dekodiere das Bild asynchron, nach dem Rendern und Präsentieren der anderen DOM-Inhalte.
    - `auto`
      - : Keine Präferenz für den Dekodierungsmodus; der Browser entscheidet, was das Beste für den Benutzer ist. Dies ist der Standardwert.

- [`elementtiming`](/de/docs/Web/HTML/Attributes/elementtiming)

  - : Markiert das Bild zur Beobachtung durch die API [`PerformanceElementTiming`](/de/docs/Web/API/PerformanceElementTiming). Der angegebene Wert wird zu einem Bezeichner für das beobachtete Bildelement. Siehe auch die Attributseite [`elementtiming`](/de/docs/Web/HTML/Attributes/elementtiming).

- `fetchpriority`

  - : Gibt einen Hinweis auf die relative Priorität zum Abrufen des Bildes.
    Erlaubte Werte:

    - `high`
      - : Hole das Bild mit einer hohen Priorität im Vergleich zu anderen Bildern.
    - `low`
      - : Hole das Bild mit einer niedrigen Priorität im Vergleich zu anderen Bildern.
    - `auto`
      - : Keine Präferenz für die Abrufpriorität einstellen.
        Dies ist der Standard.
        Es wird verwendet, wenn kein Wert oder ein ungültiger Wert festgelegt ist.

    Siehe [`HTMLImageElement.fetchPriority`](/de/docs/Web/API/HTMLImageElement/fetchPriority) für weitere Informationen.

- `height`

  - : Die intrinsische Höhe des Bildes in Pixel. Muss eine ganze Zahl ohne Einheit sein.

    > [!NOTE]
    > Das Einbeziehen von `height` und [`width`](#width) ermöglicht es dem Browser, das {{Glossary("aspect_ratio", "Seitenverhältnis")}} des Bildes zu berechnen, bevor das Bild geladen wird. Dieses Seitenverhältnis wird verwendet, um den benötigten Platz zur Anzeige des Bildes zu reservieren, wodurch eine Layoutverschiebung reduziert oder sogar verhindert wird, wenn das Bild heruntergeladen und auf den Bildschirm gemalt wird. Die Reduzierung der Layoutverschiebung ist ein wesentlicher Bestandteil einer guten Benutzererfahrung und Webleistung.

- `ismap`

  - : Dieses Boolesche Attribut zeigt an, dass das Bild Teil einer [Server-seitigen Karte](https://en.wikipedia.org/wiki/Image_map#Server-side) ist. Wenn dem so ist, werden die Koordinaten, auf die der Benutzer auf dem Bild geklickt hat, an den Server gesendet.

    > [!NOTE]
    > Dieses Attribut ist nur zulässig, wenn das `<img>`-Element ein Nachkomme eines {{htmlelement("a")}}-Elements mit einem gültigen [`href`](/de/docs/Web/HTML/Element/a#href)-Attribut ist. Dies gibt Benutzern ohne Zeigegeräte ein alternatives Ziel.

- `loading`

  - : Gibt an, wie der Browser das Bild laden soll:

    - `eager`
      - : Lade das Bild sofort, unabhängig davon, ob es sich derzeit im sichtbaren Viewport befindet oder nicht (dies ist der Standardwert).
    - `lazy`
      - : Verzögern Sie das Laden des Bildes, bis es eine berechnete Entfernung vom Viewport erreicht, wie vom Browser definiert. Die Absicht ist, das Netzwerk und den Speicherbedarf für das Bild zu vermeiden, bis es mit hinreichender Sicherheit erforderlich ist. Dies verbessert die Leistung der Inhalte in den meisten typischen Anwendungsfällen.

    > [!NOTE]
    > Das Laden wird nur verzögert, wenn JavaScript aktiviert ist. Dies ist eine Anti-Tracking-Maßnahme, da es, wenn ein Benutzeragent das Lazy-Loading unterstützt, wenn das Scripting deaktiviert ist, immer noch möglich wäre, die ungefähre Scrollposition eines Benutzers während einer Sitzung zu verfolgen, indem Bilder strategisch im Markup einer Seite platziert werden, sodass ein Server verfolgen kann, wie viele Bilder angefordert werden und wann.

    > [!NOTE]
    > Bilder mit `loading`, das auf `lazy` gesetzt ist, werden nie geladen, wenn sie keine sichtbaren Teile eines Elements schneiden, selbst wenn das Laden sie ändern würde, da nicht geladene Bilder eine `width` und `height` von `0` haben. Das Angeben von `width` und `height` bei lazy-geladenen Bildern behebt dieses Problem und ist eine bewährte Methode, [empfohlen durch die Spezifikation](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element). Dies trägt auch dazu bei, Layoutverschiebungen zu verhindern.

- `referrerpolicy`

  - : Ein String, der angibt, welcher Referrer beim Abrufen der Ressource verwendet werden soll:

    - `no-referrer`: Der {{HTTPHeader("Referer")}}-Header wird nicht gesendet.
    - `no-referrer-when-downgrade`: Der {{HTTPHeader("Referer")}}-Header wird nicht an {{Glossary("origin", "Ursprünge")}} ohne {{Glossary("TLS", "TLS")}} ({{Glossary("HTTPS", "HTTPS")}}) gesendet.
    - `origin`: Der gesendete Referrer wird auf den Ursprung der verweisenden Seite beschränkt: sein [Schema](/de/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_URL), {{Glossary("host", "Host")}} und {{Glossary("port", "Port")}}.
    - `origin-when-cross-origin`: Der an andere Ursprünge gesendete Referrer wird auf das Schema, den Host und den Port beschränkt. Navigationsvorgänge im selben Ursprung enthalten weiterhin den Pfad.
    - `same-origin`: Ein Referrer wird für {{Glossary("Same-origin_policy", "gleiche Ursprünge")}} gesendet, aber Anfragen an fremde Ursprünge enthalten keine Referrer-Informationen.
    - `strict-origin`: Senden Sie nur den Ursprung des Dokuments als Referrer, wenn das Protokollsicherheitsniveau gleich bleibt (HTTPS→HTTPS), senden Sie ihn jedoch nicht zu einem weniger sicheren Ziel (HTTPS→HTTP).
    - `strict-origin-when-cross-origin` (Standard): Sende eine vollständige URL bei Anfragen im selben Ursprung, sende nur den Ursprung, wenn das Protokollsicherheitsniveau gleich bleibt (HTTPS→HTTPS), und sende keinen Header zu einem weniger sicheren Ziel (HTTPS→HTTP).
    - `unsafe-url`: Der Referrer enthält den Ursprung _und_ den Pfad (jedoch nicht das [Fragment](/de/docs/Web/API/HTMLAnchorElement/hash), das [Passwort](/de/docs/Web/API/HTMLAnchorElement/password) oder den [Benutzernamen](/de/docs/Web/API/HTMLAnchorElement/username)). **Dieser Wert ist unsicher**, da er Ursprünge und Pfade von TLS-geschützten Ressourcen an unsichere Ursprünge weitergibt.

- `sizes`

  - : Eine oder mehrere durch Kommas getrennte Zeichenfolgen, die eine Reihe von Quellgrößen angeben. Jede Quellgröße besteht aus:

    1. Einer [Medienbedingung](/de/docs/Web/CSS/CSS_media_queries/Using_media_queries#syntax). Diese muss für das letzte Element in der Liste weggelassen werden.
    2. Einem Quellengrößenwert.

    Medienbedingungen beschreiben Eigenschaften des _Viewports_, nicht des _Bildes_. Zum Beispiel schlägt `(max-height: 500px) 1000px` vor, eine Quelle von 1000px Breite zu verwenden, wenn der _Viewport_ nicht höher als 500px ist.

    Quellengrößenwerte geben die beabsichtigte Anzeigegröße des Bildes an. {{Glossary("User_agent", "Benutzeragenten")}} verwenden die aktuelle Quellengröße, um eine der Quellen auszuwählen, die durch das `srcset`-Attribut bereitgestellt werden, wenn diese Quellen mit Breitenbeschreibungen (`w`) beschrieben werden. Die ausgewählte Quellgröße beeinflusst die {{Glossary("intrinsic_size", "intrinsische Größe")}} des Bildes (die Anzeigengröße des Bildes, wenn keine {{Glossary("CSS", "CSS")}}-Stilierung angewendet wird). Wenn das `srcset`-Attribut fehlt oder keine Werte mit einer Breitenbeschreibung enthält, hat das `sizes`-Attribut keine Wirkung.

- `src`
  - : Die Bild-{{Glossary("URL", "URL")}}. Pflichtfeld für das `<img>`-Element. In {{Glossary("Browser", "Browsern")}}, die `srcset` unterstützen, wird `src` wie ein Kandidatenbild mit einem Pixeldichte-Beschreiber `1x` behandelt, es sei denn, ein Bild mit diesem Pixeldichte-Beschreiber ist bereits in `srcset` definiert, oder `srcset` enthält `w`-Beschreiber.
- `srcset`

  - : Eine oder mehrere durch Kommas getrennte Zeichenfolgen, die mögliche Bildquellen für den {{Glossary("user_agent", "Benutzeragenten")}} angeben. Jede Zeichenfolge besteht aus:

    1. Einer {{Glossary("URL", "URL")}} zu einem Bild
    2. Optional, gefolgt von einem der folgenden Whitespace:

       - Einem Breitenbeschreiber (eine positive ganze Zahl direkt gefolgt von `w`). Der Breitenbeschreiber wird durch die im `sizes`-Attribut angegebene Quellengröße geteilt, um die effektive Pixeldichte zu berechnen.
       - Einem Pixeldichte-Beschreiber (eine positive Gleitkommazahl direkt gefolgt von `x`).

    Wenn kein Beschreiber angegeben ist, wird der Quelle der Standardbeschreiber `1x` zugewiesen.

    Es ist nicht korrekt, Breitenbeschreiber und Pixeldichte-Beschreiber im selben `srcset`-Attribut zu mischen. Doppelte Beschreiber (z.B. zwei Quellen im selben `srcset`, die beide mit `2x` beschrieben werden) sind ebenfalls ungültig.

    Wenn das `srcset`-Attribut Breitenbeschreiber verwendet, muss das `sizes`-Attribut ebenfalls vorhanden sein, sonst wird das `srcset` selbst ignoriert.

    Der Benutzeragent wählt nach eigenem Ermessen eine der verfügbaren Quellen aus. Dies gibt ihnen einen erheblichen Spielraum, um ihre Auswahl basierend auf Faktoren wie Benutzerpräferenzen oder {{Glossary("bandwidth", "Bandbreiten-")}}bedingungen anzupassen. Siehe unser [Responsive images](/de/docs/Web/HTML/Responsive_images)-Tutorial für ein Beispiel.

- `width`
  - : Die intrinsische Breite des Bildes in Pixel. Muss eine ganze Zahl ohne Einheit sein.
- `usemap`

  - : Die partielle {{Glossary("URL", "URL")}} (beginnend mit `#`) einer [Bildkarte](/de/docs/Web/HTML/Element/map), die mit dem Element verknüpft ist.

    > [!NOTE]
    > Sie können dieses Attribut nicht verwenden, wenn das `<img>`-Element innerhalb eines {{htmlelement("a")}} oder {{HTMLElement("button")}}-Elements ist.

### Veraltete Attribute

- `align` {{deprecated_inline}}

  - : Richtet das Bild mit seinem umgebenden Kontext aus. Verwenden Sie stattdessen die {{cssxref('float')}}- und/oder {{cssxref('vertical-align')}} {{Glossary("CSS", "CSS")}}-Eigenschaften. Erlaubte Werte:

    - `top`
      - : Entspricht `vertical-align: top` oder `vertical-align: text-top`
    - `middle`
      - : Entspricht `vertical-align: -moz-middle-with-baseline`
    - `bottom`
      - : Der Standardwert, entspricht `vertical-align: unset` oder `vertical-align: initial`
    - `left`
      - : Entspricht `float: left`
    - `right`
      - : Entspricht `float: right`

- `border` {{deprecated_inline}}
  - : Die Breite eines Randes um das Bild. Verwenden Sie die {{cssxref('border')}} {{Glossary("CSS", "CSS")}}-Eigenschaft stattdessen.
- `hspace` {{deprecated_inline}}
  - : Die Anzahl der Pixel des Weißraums links und rechts des Bildes. Verwenden Sie die {{cssxref('margin')}} CSS-Eigenschaft stattdessen.
- `longdesc` {{deprecated_inline}}

  - : Ein Link zu einer detaillierteren Beschreibung des Bildes. Mögliche Werte sind eine {{Glossary("URL", "URL")}} oder eine Element-`id`(/de/docs/Web/HTML/Global_attributes/id).

    > [!NOTE]
    > Dieses Attribut wird in der neuesten {{Glossary("W3C", "W3C")}}-Version, [HTML 5.2](https://html.spec.whatwg.org/multipage/obsolete.html#element-attrdef-img-longdesc), erwähnt, wurde jedoch aus dem {{Glossary("WHATWG", "WHATWG")}}-[HTML Living Standard](https://html.spec.whatwg.org/multipage/embedded-content.html#the-img-element) entfernt. Es hat eine ungewisse Zukunft; Autoren sollten stattdessen eine {{Glossary("WAI", "WAI")}}-{{Glossary("ARIA", "ARIA")}}-Alternative wie [`aria-describedby`](https://www.w3.org/TR/wai-aria-1.1/#aria-describedby) oder [`aria-details`](https://www.w3.org/TR/wai-aria-1.1/#aria-details) verwenden.

- `name` {{deprecated_inline}}
  - : Ein Name für das Element. Verwenden Sie das [`id`](/de/docs/Web/HTML/Global_attributes/id)-Attribut statt.
- `vspace` {{deprecated_inline}}
  - : Die Anzahl der Pixel des Weißraums über und unter dem Bild. Verwenden Sie die {{cssxref('margin')}} CSS-Eigenschaft stattdessen.

## Styling mit CSS

`<img>` ist ein [ersetztes Element](/de/docs/Web/CSS/Replaced_element); es hat einen {{cssxref("display")}}-Wert von `inline` standardmäßig, aber seine standardmäßigen Dimensionen werden durch die intrinsischen Werte des eingebetteten Bildes definiert, als wäre es `inline-block`. Sie können Eigenschaften wie {{cssxref("border")}}/{{cssxref("border-radius")}}, {{cssxref("padding")}}/{{cssxref("margin")}}, {{cssxref("width")}}, {{cssxref("height")}}, usw. auf ein Bild anwenden.

`<img>` hat keine Basislinie, sodass, wenn Bilder in einem Inline-Formatierungs-Kontext mit {{cssxref("vertical-align", "vertical-align: baseline")}} verwendet werden, der Boden des Bildes auf der Textbasislinie platziert wird.

Sie können die {{cssxref("object-position")}}-Eigenschaft verwenden, um das Bild innerhalb der Box des Elements zu positionieren, und die {{cssxref("object-fit")}}-Eigenschaft, um die Größenanpassung des Bildes innerhalb der Box zu justieren (zum Beispiel, ob das Bild die Box passend ausfüllen soll oder ob es gefüllt werden soll, auch wenn Clipping erforderlich ist).

Abhängig von seinem Typ kann ein Bild eine intrinsische Breite und Höhe haben. Bei einigen Bildtypen sind jedoch intrinsische Dimensionen nicht notwendig. {{Glossary("SVG", "SVG")}}-Bilder zum Beispiel haben keine intrinsischen Dimensionen, wenn ihr Wurzel-{{SVGElement("svg")}}-Element keine `width` oder `height` gesetzt hat.

## Barrierefreiheit

### Sinnvolle alternative Beschreibungen erstellen

Der Wert des `alt`-Attributs sollte einen klaren und präzisen Ersatztext für den Bildinhalt bieten. Er sollte das Vorhandensein des Bildes selbst oder den Dateinamen des Bildes nicht beschreiben. Wenn das `alt`-Attribut absichtlich weggelassen wird, weil das Bild kein sprachliches Äquivalent hat, sollten alternative Methoden in Betracht gezogen werden, um darzustellen, was das Bild zu kommunizieren versucht.

#### Nicht

```html example-bad
<img alt="image" src="penguin.jpg" />
```

#### Machen

```html example-good
<img alt="A Penguin on a beach." src="penguin.jpg" />
```

Ein wichtiger Barrierefreiheitstest besteht darin, den Inhalt des `alt`-Attributs zusammen mit vorhergehendem Textinhalt zu lesen, um zu sehen, ob er die gleiche Bedeutung wie das Bild vermittelt. Zum Beispiel, wenn das Bild von dem Satz "Auf meinen Reisen sah ich ein niedliches kleines Tier:" vorausgegangen wäre, könnte das _Nicht_-Beispiel von einem Screenreader als "Auf meinen Reisen sah ich ein niedliches kleines Tier: Bild" vorgelesen werden, was keinen Sinn ergibt. Das _Machen_-Beispiel könnte von einem Screenreader als "Auf meinen Reisen sah ich ein niedliches kleines Tier: Ein Pinguin am Strand." vorgelesen werden, was Sinn ergibt.

Für Bilder, die eine Aktion auslösen sollen, zum Beispiel Bilder, die in einem {{htmlelement("a")}}- oder {{htmlelement("button")}}-Element verschachtelt sind, sollten Sie in Erwägung ziehen, die ausgelöste Aktion im Wert des `alt`-Attributs zu beschreiben. Beispielsweise könnten Sie `alt="nächste Seite"` anstelle von `alt="Pfeil nach rechts"` schreiben. Sie könnten auch in Erwägung ziehen, eine optionale weitere Beschreibung in einem `title`-Attribut hinzuzufügen; dieses kann von Screenreadern auf Anfrage des Benutzers vorgelesen werden.

Wenn ein `alt`-Attribut bei einem Bild fehlt, können einige Screenreader stattdessen den Dateinamen des Bildes ankündigen. Dies kann eine verwirrende Erfahrung sein, wenn der Dateiname nicht repräsentativ für den Inhalt des Bildes ist.

- [Ein Entscheidungsbaum für Alt • Bilder • WAI Web Accessibility Tutorials](https://www.w3.org/WAI/tutorials/images/decision-tree/)
- [Alt-Texte: Der Ultimative Leitfaden — Axess Lab](https://axesslab.com/alt-texts/)
- [Anleitung zum Erstellen großartiger Alt-Texte: Eine Einführung | Deque](https://www.deque.com/blog/great-alt-text-introduction/)
- [MDN Understanding WCAG, Erläuterungen zu Richtlinie 1.1](/de/docs/Web/Accessibility/Understanding_WCAG/Perceivable#guideline_1.1_—_providing_text_alternatives_for_non-text_content)
- [Erfolgskriterium 1.1.1 verstehen | W3C Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)

### Erkennen von SVG als Bild

Aufgrund eines [Fehlers in VoiceOver](https://webkit.org/b/216364) kündigt VoiceOver SVG-Bilder nicht korrekt als Bilder an. Fügen Sie [`role="img"`](/de/docs/Web/Accessibility/ARIA/Roles/img_role) allen `<img>`-Elementen mit SVG-Quelldateien hinzu, um sicherzustellen, dass Hilfstechnologien das SVG korrekt als Bildinhalt ankündigen.

```html
<img src="mdn.svg" alt="MDN" role="img" />
```

### Das title-Attribut

Das [`title`](/de/docs/Web/HTML/Global_attributes/title)-Attribut ist kein akzeptabler Ersatz für das `alt`-Attribut. Vermeiden Sie zudem die Duplikation des Werts des `alt`-Attributs in einem auf demselben Bild deklarierten `title`-Attribut. Dies kann dazu führen, dass einige Screenreader den gleichen Text zweimal ankündigen, was eine verwirrende Erfahrung schafft.

Das `title`-Attribut sollte auch nicht als ergänzende Beschriftungsinformation verwendet werden, um die `alt`-Beschreibung eines Bildes zu begleiten. Wenn ein Bild eine Beschriftung benötigt, verwenden Sie die [`figure`](/de/docs/Web/HTML/Element/figure)- und [`figcaption`](/de/docs/Web/HTML/Element/figcaption)-Elemente.

Der Wert des `title`-Attributs wird dem Benutzer normalerweise als Tooltip präsentiert, der kurz nach dem Anhalten des Cursors über dem Bild erscheint. Obwohl dies dem Benutzer zusätzliche Informationen bieten _kann_, sollten Sie nicht davon ausgehen, dass der Benutzer es jemals sehen wird: Der Benutzer hat möglicherweise nur eine Tastatur oder einen Touchscreen. Wenn Sie Informationen haben, die für den Benutzer besonders wichtig oder wertvoll sind, präsentieren Sie sie inline mithilfe einer der oben genannten Methoden statt mit `title`.

- [Das HTML-Title-Attribut verwenden – aktualisiert | The Paciello Group](https://www.tpgi.com/using-the-html-title-attribute-updated/)

## Beispiele

### Alternativtext

Das folgende Beispiel bettet ein Bild in die Seite ein und enthält alternativen Text zur Barrierefreiheit.

```html
<img src="favicon144.png" alt="MDN" />
```

{{ EmbedLiveSample('Alternative_text', '100%', '160') }}

### Bildlink

Dieses Beispiel baut auf dem vorherigen auf und zeigt, wie das Bild zu einem Link gemacht wird. Um dies zu tun, nisten Sie das `<img>`-Tag in das {{HTMLElement("a")}} ein. Sie sollten den Alternativtext die Ressource beschreiben lassen, auf die der Link zeigt, als ob Sie stattdessen einen Textlink verwenden würden.

```html
<a href="https://developer.mozilla.org">
  <img src="favicon144.png" alt="Visit the MDN site" />
</a>
```

{{ EmbedLiveSample('Image_link', '100%', '160') }}

### Verwendung des srcset-Attributs

In diesem Beispiel fügen wir ein `srcset`-Attribut mit einem Verweis auf eine hochauflösende Version des Logos ein; diese wird anstelle des Bildes im `src`-Attribut auf hochauflösenden Geräten geladen. Das Bild, auf das im `src`-Attribut verwiesen wird, wird als `1x`-Kandidat in {{Glossary("User_agent", "Benutzeragenten")}} betrachtet, die `srcset` unterstützen.

```html
<img src="favicon72.png" alt="MDN" srcset="favicon144.png 2x" />
```

{{EmbedLiveSample("Using_the_srcset_attribute", "100%", "160")}}

### Verwendung der Attribute srcset und sizes

Das `src`-Attribut wird in {{Glossary("User_agent", "Benutzeragenten")}}, die `srcset` unterstützen, ignoriert, wenn `w`-Beschreiber enthalten sind. Wenn die Medienbedingung `(max-width: 600px)` zutrifft, wird das 200 Pixel breite Bild geladen (es ist das, das `200px` am nächsten kommt), andernfalls wird das andere Bild geladen.

```html
<img
  src="clock-demo-200px.png"
  alt="The time is 12:45."
  srcset="clock-demo-200px.png 200w, clock-demo-400px.png 400w"
  sizes="(max-width: 600px) 200px, 50vw" />
```

{{EmbedLiveSample("Using_the_srcset_and_sizes_attributes", "100%", 350)}}

> [!NOTE]
> Um die Größenanpassung in Aktion zu sehen, besuchen Sie das {{LiveSampleLink('Using_the_srcset_and_sizes_attributes', 'Beispiel auf einer separaten Seite')}}, um tatsächlich den Inhaltsbereich zu ändern.

## Sicherheits- und Datenschutzbedenken

Obwohl `<img>`-Elemente unschuldige Verwendungen haben, können sie unerwünschte Konsequenzen für die Sicherheit und den Datenschutz der Benutzer haben. Weitere Informationen und Maßnahmen finden Sie unter [Referer-Header: Datenschutz- und Sicherheitsbedenken](/de/docs/Web/Security/Referer_header:_privacy_and_security_concerns).

## Technische Zusammenfassung

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">
        <a href="/de/docs/Web/HTML/Content_categories"
          >Inhaltskategorien</a
        >
      </th>
      <td>
        <a href="/de/docs/Web/HTML/Content_categories#flow_content"
          >Flussinhalt</a
        >,
        <a href="/de/docs/Web/HTML/Content_categories#phrasing_content"
          >gewöhnlicher Inhalt</a
        >,
        <a href="/de/docs/Web/HTML/Content_categories#embedded_content"
          >eingebetteter Inhalt</a
        >,
        <a href="/de/docs/Web/HTML/Content_categories#palpable_content"
          >spürbarer Inhalt</a
        >. Wenn das Element ein <code>usemap</code>-Attribut hat, ist es auch Teil der Kategorie interaktiver Inhalt.
      </td>
    </tr>
    <tr>
      <th scope="row">Erlaubter Inhalt</th>
      <td>Keiner; es ist ein {{Glossary("void_element", "leeres Element")}}.</td>
    </tr>
    <tr>
      <th scope="row">Tag-Auslassung</th>
      <td>Muss ein Start-Tag haben und darf kein End-Tag haben.</td>
    </tr>
    <tr>
      <th scope="row">Erlaubte Eltern</th>
      <td>Jedes Element, das eingebetteten Inhalt akzeptiert.</td>
    </tr>
    <tr>
      <th scope="row">Implizite ARIA-Rolle</th>
      <td>
        <ul>
          <li>
            mit nicht leerem <code>alt</code>-Attribut oder ohne
            <code>alt</code>-Attribut:
            <code
              ><a href="/de/docs/Web/Accessibility/ARIA/Roles/img_role"
                ><code>img</code></a
              ></code
            >
          </li>
          <li>
            mit leerem <code>alt</code>-Attribut:
            <a href="/de/docs/Web/Accessibility/ARIA/Roles/presentation_role"
              ><code>präsentation</code></a
            >
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th scope="row">Erlaubte ARIA-Rollen</th>
      <td>
        <ul>
          <li>
            mit nicht leerem <code>alt</code>-Attribut:
            <ul>
              <li>
                <code
                  ><a
                    href="/de/docs/Web/Accessibility/ARIA/Roles/button_role"
                    >button</a
                  ></code
                >
              </li>
              <li>
                <code
                  ><a
                    href="/de/docs/Web/Accessibility/ARIA/Roles/checkbox_role"
                    >checkbox</a
                  ></code
                >
              </li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/link_role"><code>link</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/menuitem_role"><code>menuitem</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/menuitemcheckbox_role"><code>menuitemcheckbox</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/menuitemradio_role"><code>menuitemradio</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/option_role"><code>option</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/progressbar_role"><code>progressbar</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/scrollbar_role"><code>scrollbar</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/separator_role"><code>separator</code></a></li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/slider_role"><code>slider</code></a></li>
              <li>
                <code
                  ><a
                    href="/de/docs/Web/Accessibility/ARIA/Roles/switch_role"
                    >switch</a
                  ></code
                >
              </li>
              <li>
                <code
                  ><a href="/de/docs/Web/Accessibility/ARIA/Roles/tab_role"
                    >tab</a
                  ></code
                >
              </li>
              <li><a href="/de/docs/Web/Accessibility/ARIA/Roles/treeitem_role"><code>treeitem</code></a></li>
            </ul>
          </li>
          <li>
            mit leerem <code>alt</code>-Attribut: <a href="/de/docs/Web/Accessibility/ARIA/Roles/none_role"><code>none</code></a>
            oder <a href="/de/docs/Web/Accessibility/ARIA/Roles/presentation_role"><code>präsentation</code></a>
          </li>
          <li>
            ohne <code>alt</code>-Attribut: keine <code>rolle</code> zugelassen
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <th scope="row">DOM-Schnittstelle</th>
      <td>[`HTMLImageElement`](/de/docs/Web/API/HTMLImageElement)</td>
    </tr>
  </tbody>
</table>

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{HTMLElement("picture")}}, {{HTMLElement("object")}}, und {{HTMLElement("embed")}}-Elemente
- {{cssxref("object-fit")}}, {{cssxref("object-position")}}, {{cssxref("image-orientation")}}, {{cssxref("image-rendering")}}, und {{cssxref("image-resolution")}}: Bildbezogene CSS-Eigenschaften.
- [`HTMLImageElement`](/de/docs/Web/API/HTMLImageElement)-Schnittstelle für dieses Element
- [HTML-Bilder](/de/docs/Learn_web_development/Core/Structuring_content/HTML_images)
- [Leitfaden für Bilddateiformate und -typen](/de/docs/Web/Media/Guides/Formats/Image_types)
- [Responsive images](/de/docs/Web/HTML/Responsive_images)
