---
title: "HTMLInputElement: capture-Eigenschaft"
short-title: capture
slug: Web/API/HTMLInputElement/capture
l10n:
  sourceCommit: e9b6cd1b7fa8612257b72b2a85a96dd7d45c0200
---

{{ApiRef("HTML DOM")}}

Die **`capture`**-Eigenschaft der [`HTMLInputElement`](/de/docs/Web/API/HTMLInputElement)-Schnittstelle spiegelt das [`capture`](/de/docs/Web/HTML/Reference/Attributes/capture)-Attribut des {{HTMLElement("input")}}-Elements wider. Sie ist nur für [`<input>` vom Typ `file`](/de/docs/Web/HTML/Reference/Elements/input/file) relevant und gibt an, ob eine neue Datei von einer benutzerseitigen (`user`) oder einer nach außen gerichteten (`environment`) Kamera oder einem Mikrofon erfasst werden soll. Der Dateityp wird durch das [`accept`](/de/docs/Web/HTML/Reference/Attributes/accept)-Attribut definiert. Wenn das Attribut nicht explizit gesetzt ist, ist die `capture`-Eigenschaft ein leerer String.

## Wert

Ein String; normalerweise entweder `user` oder `environment`, oder ein leerer String (`""`).

## Beispiel

```js
const inputElement = document.querySelector("avatar");
console.log(inputElement.capture); // the current value of the capture attribute
inputElement.capture = "user"; // sets the capture value
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`HTMLInputElement.type`](/de/docs/Web/API/HTMLInputElement/type)
- [`HTMLInputElement.multiple`](/de/docs/Web/API/HTMLInputElement/multiple)
- [`HTMLInputElement.accept`](/de/docs/Web/API/HTMLInputElement/accept)
- [`HTMLInputElement.files`](/de/docs/Web/API/HTMLInputElement/files)
- [Dateityp-Spezifizierer](/de/docs/Web/HTML/Reference/Elements/input/file#unique_file_type_specifiers)
- [Verwendung von Dateien aus Webanwendungen](/de/docs/Web/API/File_API/Using_files_from_web_applications)
- [File API](/de/docs/Web/API/File_API)
