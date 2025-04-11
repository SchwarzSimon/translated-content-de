---
title: "AudioBufferSourceNode: loopEnd-Eigenschaft"
short-title: loopEnd
slug: Web/API/AudioBufferSourceNode/loopEnd
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{ APIRef("Web Audio API") }}

Die `loopEnd`-Eigenschaft der [`AudioBufferSourceNode`](/de/docs/Web/API/AudioBufferSourceNode)-Schnittstelle ist eine Fließkommazahl, die in Sekunden angibt, bei welchem Offset innerhalb der Wiedergabe des [`AudioBuffer`](/de/docs/Web/API/AudioBuffer) die Wiedergabe zum durch die [`loopStart`](/de/docs/Web/API/AudioBufferSourceNode/loopStart)-Eigenschaft angegebenen Zeitpunkt zurückspringen soll. Dies wird nur verwendet, wenn die [`loop`](/de/docs/Web/API/AudioBufferSourceNode/loop)-Eigenschaft auf `true` gesetzt ist.

## Wert

Eine Fließkommazahl, die das Offset in Sekunden innerhalb des Audiobuffers angibt, zu dem jede Schleife zurück zum Anfang der Schleife springt (das heißt, die aktuelle Spielzeit wird auf [`AudioBufferSourceNode.loopStart`](/de/docs/Web/API/AudioBufferSourceNode/loopStart) zurückgesetzt). Diese Eigenschaft wird nur verwendet, wenn die [`loop`](/de/docs/Web/API/AudioBufferSourceNode/loop)-Eigenschaft auf `true` gesetzt ist.

Der Standardwert ist 0.

## Beispiele

### `loopEnd` setzen

In diesem Beispiel wird beim Drücken von "Play" ein Audiotrack geladen, dekodiert und in einen [`AudioBufferSourceNode`](/de/docs/Web/API/AudioBufferSourceNode) eingefügt.

Das Beispiel setzt dann die `loop`-Eigenschaft auf `true`, sodass der Track in einer Schleife abgespielt wird, und spielt den Track ab.

Der Benutzer kann die Eigenschaften `loopStart` und `loopEnd` mittels [Range-Controls](/de/docs/Web/HTML/Reference/Elements/input/range) einstellen.

> [!NOTE]
> Sie können [das vollständige Beispiel live ausführen](https://mdn.github.io/webaudio-examples/audio-buffer-source-node/loop/) (oder [den Quellcode ansehen](https://github.com/mdn/webaudio-examples/tree/main/audio-buffer-source-node/loop).)

```js
let audioCtx;
let buffer;
let source;

const play = document.getElementById("play");
const stop = document.getElementById("stop");

const loopstartControl = document.getElementById("loopstart-control");
const loopstartValue = document.getElementById("loopstart-value");

const loopendControl = document.getElementById("loopend-control");
const loopendValue = document.getElementById("loopend-value");

async function loadAudio() {
  try {
    // Load an audio file
    const response = await fetch("rnb-lofi-melody-loop.wav");
    // Decode it
    buffer = await audioCtx.decodeAudioData(await response.arrayBuffer());
    const max = Math.floor(buffer.duration);
    loopstartControl.setAttribute("max", max);
    loopendControl.setAttribute("max", max);
  } catch (err) {
    console.error(`Unable to fetch the audio file. Error: ${err.message}`);
  }
}

play.addEventListener("click", async () => {
  if (!audioCtx) {
    audioCtx = new AudioContext();
    await loadAudio();
  }
  source = audioCtx.createBufferSource();
  source.buffer = buffer;
  source.connect(audioCtx.destination);
  source.loop = true;
  source.loopStart = loopstartControl.value;
  source.loopEnd = loopendControl.value;
  source.start();
  play.disabled = true;
  stop.disabled = false;
  loopstartControl.disabled = false;
  loopendControl.disabled = false;
});

stop.addEventListener("click", () => {
  source.stop();
  play.disabled = false;
  stop.disabled = true;
  loopstartControl.disabled = true;
  loopendControl.disabled = true;
});

loopstartControl.addEventListener("input", () => {
  source.loopStart = loopstartControl.value;
  loopstartValue.textContent = loopstartControl.value;
});

loopendControl.addEventListener("input", () => {
  source.loopEnd = loopendControl.value;
  loopendValue.textContent = loopendControl.value;
});
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Verwendung der Web Audio API](/de/docs/Web/API/Web_Audio_API/Using_Web_Audio_API)
- [Web Audio API](/de/docs/Web/API/Web_Audio_API)
