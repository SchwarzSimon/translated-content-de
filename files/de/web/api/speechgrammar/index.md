---
title: SpeechGrammar
slug: Web/API/SpeechGrammar
l10n:
  sourceCommit: 706cbf21987296c604cc96b7f95095ed7aba6bb8
---

{{APIRef("Web Speech API")}}{{deprecated_header}}{{non-standard_header}}

Das **`SpeechGrammar`** Interface der [Web Speech API](/de/docs/Web/API/Web_Speech_API) repräsentiert eine Menge von Wörtern oder Wortmustern, die wir möchten, dass der Erkennungsdienst erkennt.

Grammatik wird mit dem [JSpeech Grammar Format](https://www.w3.org/TR/jsgf/) (**JSGF**) definiert. Andere Formate könnten in der Zukunft ebenfalls unterstützt werden.

## Konstruktor

- [`SpeechGrammar()`](/de/docs/Web/API/SpeechGrammar/SpeechGrammar) {{Non-standard_Inline}} {{deprecated_inline}}
  - : Erstellt ein neues `SpeechGrammar` Objekt.

## Instanz-Eigenschaften

- [`SpeechGrammar.src`](/de/docs/Web/API/SpeechGrammar/src) {{deprecated_inline}}
  - : Setzt und gibt einen String zurück, der die Grammatik enthält, innerhalb der `SpeechGrammar` Objektinstanz.
- [`SpeechGrammar.weight`](/de/docs/Web/API/SpeechGrammar/weight) {{Optional_Inline}} {{deprecated_inline}}
  - : Setzt und gibt das Gewicht des `SpeechGrammar` Objekts zurück.

## Beispiele

```js
const grammar =
  "#JSGF V1.0; grammar colors; public <color> = aqua | azure | beige | bisque | black | blue | brown | chocolate | coral | crimson | cyan | fuchsia | ghostwhite | gold | goldenrod | gray | green | indigo | ivory | khaki | lavender | lime | linen | magenta | maroon | moccasin | navy | olive | orange | orchid | peru | pink | plum | purple | red | salmon | sienna | silver | snow | tan | teal | thistle | tomato | turquoise | violet | white | yellow ;";
const recognition = new SpeechRecognition();
const speechRecognitionList = new SpeechGrammarList();
speechRecognitionList.addFromString(grammar, 1);
recognition.grammars = speechRecognitionList;

console.log(speechRecognitionList[0].src); // should return the same as the contents of the grammar variable
console.log(speechRecognitionList[0].weight); // should return 1 - the same as the weight set in addFromString.
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Web Speech API](/de/docs/Web/API/Web_Speech_API)
