---
title: "HTMLSourceElement: type-Eigenschaft"
short-title: type
slug: Web/API/HTMLSourceElement/type
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{APIRef("HTML DOM")}}

Die **`type`**-Eigenschaft des [`HTMLSourceElement`](/de/docs/Web/API/HTMLSourceElement)-Interfaces ist ein String, der den {{Glossary("MIME_type", "MIME-Typ")}} der Medienressource darstellt.

Sie spiegelt das `type`-Attribut des {{HTMLElement("source")}}-Elements wider.

## Wert

Ein String.

## Beispiele

```html
<source
  id="el"
  src="large.webp"
  type="video/webp"
  media="screen and (min-width: 600px)" />
```

```js
const el = document.getElementById("el");
console.log(el.type); // Output: "video/webp"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`HTMLSourceElement.src`](/de/docs/Web/API/HTMLSourceElement/src)
- [`HTMLSourceElement.srcset`](/de/docs/Web/API/HTMLSourceElement/srcset)
- [`HTMLSourceElement.media`](/de/docs/Web/API/HTMLSourceElement/media)
- [`HTMLSourceElement.sizes`](/de/docs/Web/API/HTMLSourceElement/sizes)
- {{htmlelement("source")}}
- {{htmlelement("picture")}}
- {{htmlelement("audio")}}
- {{htmlelement("video")}}
- [Medientypen im Web](/de/docs/Web/Media/Guides/Formats)
- [Wichtige MIME-Typen für Webentwickler](/de/docs/Web/HTTP/Guides/MIME_types#important_mime_types_for_web_developers)
- [Media Capabilities API](/de/docs/Web/API/Media_Capabilities_API)
