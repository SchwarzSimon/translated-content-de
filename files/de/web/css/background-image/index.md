---
title: background-image
slug: Web/CSS/background-image
l10n:
  sourceCommit: b64538dc77e9a6181b882bd54bdbb307c1430ba8
---

{{CSSRef}}

Die **`background-image`**-Eigenschaft von [CSS](/de/docs/Web/CSS) legt ein oder mehrere Hintergrundbilder für ein Element fest.

{{EmbedInteractiveExample("pages/css/background-image.html")}}

Die Hintergrundbilder werden auf Stapelkontextebenen gezeichnet, die übereinander liegen. Die zuerst angegebene Ebene wird so gezeichnet, als läge sie am nächsten zur Benutzerin oder zum Benutzer.

Die [Ränder](/de/docs/Web/CSS/border) des Elements werden dann darüber gezeichnet, und die {{cssxref("background-color")}} wird darunter gezeichnet. Wie die Bilder relativ zum Kasten und seinen Rändern gezeichnet werden, wird durch die CSS-Eigenschaften {{cssxref("background-clip")}} und {{cssxref("background-origin")}} definiert.

Wenn ein angegebenes Bild nicht gezeichnet werden kann (z. B. wenn die Datei, die durch die angegebene URI bezeichnet wird, nicht geladen werden kann), behandeln Browser es, als hätte es den Wert `none`.

> [!NOTE]
> Selbst wenn die Bilder undurchsichtig sind und die Farbe unter normalen Umständen nicht angezeigt wird, sollten Webentwicklerinnen und Webentwickler immer eine {{cssxref("background-color")}} angeben. Wenn die Bilder nicht geladen werden können – beispielsweise wenn das Netzwerk nicht verfügbar ist –, wird die Hintergrundfarbe als Fallback verwendet.

## Syntax

```css
/* single image */
background-image: linear-gradient(black, white);
background-image: url("cat-front.png");

/* multiple images */
background-image: radial-gradient(circle, #0000 45%, #000f 48%),
  radial-gradient(ellipse farthest-corner, #fc1c14 20%, #cf15cf 80%);

/* Global values */
background-image: inherit;
background-image: initial;
background-image: revert;
background-image: revert-layer;
background-image: unset;
```

Jedes Hintergrundbild wird entweder als Schlüsselwort `none` oder als {{cssxref("&lt;image&gt;")}}-Wert angegeben.

Um mehrere Hintergrundbilder anzugeben, geben Sie mehrere Werte an, die durch ein Komma getrennt sind.

### Werte

- `none`
  - : Ist ein Schlüsselwort, das das Fehlen von Bildern bezeichnet.
- `<image>`
  - : Ist ein {{cssxref("&lt;image&gt;")}}, das das anzuzeigende Bild bezeichnet. Es können mehrere durch Kommas getrennt werden, da [mehrere Hintergründe](/de/docs/Web/CSS/CSS_backgrounds_and_borders/Using_multiple_backgrounds) unterstützt werden.

## Barrierefreiheit

Browser bieten Assistenztechnologien keine besonderen Informationen zu Hintergrundbildern. Dies ist vor allem für Bildschirmlesegeräte wichtig, da diese das Vorhandensein eines Hintergrundbildes nicht ankündigen und somit nichts an die Benutzerin oder den Benutzer weitergeben. Wenn das Bild Informationen enthält, die entscheidend für das Verständnis des Zwecks der Seite sind, ist es besser, dies semantisch im Dokument zu beschreiben.

- [MDN Understanding WCAG, Leitfaden 1.1 Erklärungen](/de/docs/Web/Accessibility/Understanding_WCAG/Perceivable#guideline_1.1_—_providing_text_alternatives_for_non-text_content)
- [Understanding Success Criterion 1.1.1 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/2016/NOTE-UNDERSTANDING-WCAG20-20161007/text-equiv-all.html)

Es ist außerdem wichtig sicherzustellen, dass das Kontrastverhältnis zwischen dem Hintergrundbild und dem Vordergrundtext hoch genug ist, damit Personen mit eingeschränktem Sehvermögen den Inhalt der Seite lesen können.

Das Farbkontrastverhältnis wird bestimmt, indem die Leuchtdichte der Text- und Hintergrundfarbwerte verglichen wird. Um die [Richtlinien für barrierefreie Webinhalte (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/) zu erfüllen, ist ein Verhältnis von 4,5:1 für Fließtext und 3:1 für größere Texte wie Überschriften erforderlich. Große Texte sind definiert als 24px oder größer oder [fett gedruckt](/de/docs/Web/CSS/font-weight) mit 18,66px oder größer.

- [WebAIM: Color Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Understanding WCAG, Leitfaden 1.4 Erklärung](/de/docs/Web/Accessibility/Understanding_WCAG/Perceivable#guideline_1.4_make_it_easier_for_users_to_see_and_hear_content_including_separating_foreground_from_background)
- [Understanding Success Criterion 1.4.3 | Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html), W3C (2023)

## Formale Definition

{{cssinfo}}

## Formale Syntax

{{csssyntax}}

## Beispiele

### Hintergrundbilder schichten

Beachten Sie, dass das Sternbild teilweise transparent ist und über dem Katzenbild geschichtet wird.

#### HTML

```html
<div>
  <p class="cats-and-stars">This paragraph is full of cats<br />and stars.</p>
  <p>This paragraph is not.</p>
  <p class="cats-and-stars">Here are more cats for you.<br />Look at them!</p>
  <p>And no more.</p>
</div>
```

#### CSS

```css
p {
  font-weight: bold;
  font-size: 1.5em;
  color: white;
  text-shadow: 0.07em 0.07em 0.05em black;
  background-image: none;
  background-color: transparent;
}

div {
  background-image: url("mdn_logo_only_color.png");
}

.cats-and-stars {
  background-image: url("star-transparent.gif"), url("cat-front.png");
  background-color: transparent;
}
```

#### Ergebnis

{{EmbedLiveSample('Layering_background_images')}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{HTMLElement("img")}}
- Bildbezogene Funktionen:
  - {{cssxref("gradient/linear-gradient", "linear-gradient()")}}
  - {{cssxref("gradient/radial-gradient", "radial-gradient()")}}
  - {{cssxref("gradient/conic-gradient", "conic-gradient()")}}
  - {{cssxref("gradient/repeating-linear-gradient", "repeating-linear-gradient()")}}
  - {{cssxref("gradient/repeating-radial-gradient", "repeating-radial-gradient()")}}
  - {{cssxref("gradient/repeating-conic-gradient", "repeating-conic-gradient()")}}
  - {{cssxref("url_value", "&lt;url&gt;")}}
- [CSS-Gradients verwenden](/de/docs/Web/CSS/CSS_images/Using_CSS_gradients)
- [Bild-Sprites mit CSS umsetzen](/de/docs/Web/CSS/CSS_images/Implementing_image_sprites_in_CSS)
- [CSS-Bilder](/de/docs/Web/CSS/CSS_images) Modul

- Hintergrundeigenschaften
  - {{cssxref("background-attachment")}}
  - {{cssxref("background-clip")}}
  - {{cssxref("background-color")}}
  - {{cssxref("background-origin")}}
  - {{cssxref("background-position")}}
  - {{cssxref("background-repeat")}}
  - {{cssxref("background-size")}}
  - {{cssxref("background")}} Kurzform
- [Lernen: Hintergründe und Rahmen](/de/docs/Learn_web_development/Core/Styling_basics/Backgrounds_and_borders)
- [Mehrere Hintergründe verwenden](/de/docs/Web/CSS/CSS_backgrounds_and_borders/Using_multiple_backgrounds)
- [Hintergrundbilder skalieren](/de/docs/Web/CSS/CSS_backgrounds_and_borders/Resizing_background_images)
- [CSS Hintergründe und Rahmen](/de/docs/Web/CSS/CSS_backgrounds_and_borders) Modul
