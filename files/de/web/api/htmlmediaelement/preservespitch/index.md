---
title: "HTMLMediaElement: preservesPitch-Eigenschaft"
short-title: preservesPitch
slug: Web/API/HTMLMediaElement/preservesPitch
l10n:
  sourceCommit: 27bceead8e9b1fe9c92df0fa5e418f81bd5b9fdf
---

{{APIRef("HTML DOM")}}

Die **`HTMLMediaElement.preservesPitch`**-Eigenschaft legt fest, ob der Browser die Tonhöhe des Audios anpassen sollte, um Änderungen der Wiedergabegeschwindigkeit, vorgenommen durch das Setzen von [`HTMLMediaElement.playbackRate`](/de/docs/Web/API/HTMLMediaElement/playbackRate), auszugleichen.

## Wert

Ein boolescher Wert, der standardmäßig auf `true` gesetzt ist.

## Beispiele

### Festlegen der preservesPitch-Eigenschaft

In diesem Beispiel haben wir ein {{HTMLElement("audio")}}-Element, ein Bereichssteuerungselement, das die Wiedergabegeschwindigkeit anpasst, und ein Kontrollkästchen, das `preservesPitch` festlegt.

Versuchen Sie, das Audio abzuspielen, dann die Wiedergabegeschwindigkeit anzupassen und das Kontrollkästchen zu aktivieren und zu deaktivieren.

```html
<audio
  controls
  src="https://mdn.github.io/webaudio-examples/audio-basics/outfoxing.mp3"></audio>

<div>
  <label for="rate">Adjust playback rate:</label>
  <input id="rate" type="range" min="0.25" max="3" step="0.05" value="1" />
</div>

<div>
  <label for="pitch">Preserve pitch:</label>
  <input type="checkbox" id="pitch" name="pitch" checked />
</div>
```

```css hidden
div {
  margin: 0.5rem 0;
}
```

```js
const audio = document.querySelector("audio");
document.getElementById("rate").addEventListener("change", (e) => {
  audio.playbackRate = e.target.value;
});
document.getElementById("pitch").addEventListener("change", (e) => {
  audio.preservesPitch = e.target.checked;
});
```

{{EmbedLiveSample("Festlegen der preservesPitch-Eigenschaft")}}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`HTMLMediaElement.playbackRate`](/de/docs/Web/API/HTMLMediaElement/playbackRate)
- [Wiedergabegeschwindigkeit im Web Audio erklärt](/de/docs/Web/Media/Guides/Audio_and_video_delivery/WebAudio_playbackRate_explained)
