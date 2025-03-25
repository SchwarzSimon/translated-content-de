---
title: runtime.onMessage
slug: Mozilla/Add-ons/WebExtensions/API/runtime/onMessage
l10n:
  sourceCommit: c4c42a1573a65a808f085999a4d8d97199e142d1
---

{{AddonSidebar}}

Verwenden Sie dieses Ereignis, um Nachrichten von einem anderen Teil Ihrer Erweiterung zu empfangen.

Einige Anwendungsbeispiele sind:

- **in einem [Inhalts-Skript](/de/docs/Mozilla/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#content_scripts)**, um Nachrichten von einem [Hintergrund-Skript](/de/docs/Mozilla/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#background_scripts) zu empfangen.
- **in einem Hintergrund-Skript**, um Nachrichten von einem Inhalts-Skript zu empfangen.
- **in einem [Optionenseite oder Popup](/de/docs/Mozilla/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#sidebars_popups_and_options_pages) Skript**, um Nachrichten von einem Hintergrund-Skript zu empfangen.
- **in einem Hintergrund-Skript**, um Nachrichten von einer Optionenseite oder einem Popup-Skript zu empfangen.

Um eine Nachricht zu senden, die vom `onMessage()`-Listener empfangen wird, verwenden Sie {{WebExtAPIRef("runtime.sendMessage()")}} oder (um eine Nachricht an ein Inhalts-Skript zu senden) {{WebExtAPIRef("tabs.sendMessage()")}}.

> [!NOTE]
> Vermeiden Sie das Erstellen mehrerer `onMessage()`-Listener für den gleichen Nachrichtentyp, da die Reihenfolge, in der mehrere Listener ausgelöst werden, nicht garantiert ist.
>
> Wenn Sie die Zustellung einer Nachricht an einen bestimmten Endpunkt garantieren möchten, verwenden Sie den [verbindungsbasierten Ansatz zum Nachrichtenaustausch](/de/docs/Mozilla/Add-ons/WebExtensions/Content_scripts#connection-based_messaging).

Zusammen mit der Nachricht selbst wird dem Listener Folgendes übergeben:

- ein `sender`-Objekt mit Details über den Nachrichtenabsender.
- eine `sendResponse()`-Funktion, die verwendet werden kann, um eine Antwort an den Absender zu senden.

Sie können eine synchronisierte Antwort auf die Nachricht senden, indem Sie die `sendResponse()`-Funktion innerhalb Ihres Listeners aufrufen. Siehe das [Beispiel zum Senden einer synchronen Antwort](#senden_einer_synchronen_antwort).

Um eine asynchrone Antwort zu senden, gibt es zwei Möglichkeiten:

- Geben Sie `true` vom Ereignis-Listener zurück. Dies hält die `sendResponse()`-Funktion gültig, nachdem der Listener zurückkehrt, sodass Sie sie später aufrufen können. Siehe das [Beispiel zum Senden einer asynchronen Antwort mit `sendResponse`](#senden_einer_asynchronen_antwort_mithilfe_von_sendresponse).
  > [!WARNING]
  > Präpendieren Sie nicht `async` zur Funktion. Das Präpendieren von `async` ändert die Bedeutung in das [Senden einer asynchronen Antwort mit einem Versprechen (Promise)](#senden_einer_asynchronen_antwort_mit_einem_promise), was faktisch dasselbe ist wie `sendResponse(true)`.
- Geben Sie ein `Promise` vom Ereignis-Listener zurück und lösen Sie es auf, wenn Sie die Antwort haben (oder lehnen Sie es im Falle eines Fehlers ab). [Siehe das [Beispiel zum Senden einer asynchronen Antwort mit einem Promise](#senden_einer_asynchronen_antwort_mit_einem_promise).

> [!NOTE]
> Sie können auch einen [verbindungsbasierten Ansatz zum Nachrichtenaustausch](/de/docs/Mozilla/Add-ons/WebExtensions/Content_scripts#connection-based_messaging) verwenden.

## Syntax

```js-nolint
browser.runtime.onMessage.addListener(listener)
browser.runtime.onMessage.removeListener(listener)
browser.runtime.onMessage.hasListener(listener)
```

Ereignisse haben drei Funktionen:

- `addListener(listener)`
  - : Fügt diesem Ereignis einen Listener hinzu.
- `removeListener(listener)`
  - : Stoppt das Hören dieses Ereignisses. Das `listener`-Argument ist der zu entfernende Listener.
- `hasListener(listener)`
  - : Überprüft, ob mindestens ein Listener für dieses Ereignis registriert ist. Gibt `true` zurück, wenn es zuhört, andernfalls `false`.

## addListener Syntax

### Parameter

- `listener`

  - : Die Funktion, die aufgerufen wird, wenn dieses Ereignis eintritt. Die Funktion erhält folgende Argumente:

    - `message`
      - : `object`. Die Nachricht. Dies ist ein serialisierbares Objekt (siehe [Datenklon-Algorithmus](/de/docs/Mozilla/Add-ons/WebExtensions/Chrome_incompatibilities#data_cloning_algorithm)).
    - `sender`
      - : Ein {{WebExtAPIRef('runtime.MessageSender')}}-Objekt, das den Absender der Nachricht repräsentiert.
    - `sendResponse`

      - : Eine Funktion, die höchstens einmal aufgerufen wird, um eine Antwort auf die `message` zu senden. Die Funktion nimmt ein Argument: jedes serialisierbare Objekt (siehe [Datenklon-Algorithmus](/de/docs/Mozilla/Add-ons/WebExtensions/Chrome_incompatibilities#data_cloning_algorithm)). Dieses Argument wird an den Nachrichtenabsender zurückgegeben.

        Wenn Sie mehr als einen `onMessage()`-Listener im selben Dokument haben, kann nur einer eine Antwort senden.

        Um eine Antwort synchron zu senden, rufen Sie `sendResponse()` auf, bevor die Listener-Funktion zurückkehrt.

        Um eine Antwort asynchron zu senden, verwenden Sie eine dieser Optionen:

        - Geben Sie ein {{jsxref("Promise")}} von der Listener-Funktion zurück und lösen Sie das Promise auf, wenn die Antwort bereit ist. Dies ist der bevorzugte Ansatz.
        - Behalten Sie eine Referenz auf das `sendResponse()`-Argument und geben Sie `true` von der Listener-Funktion zurück. Sie rufen dann `sendResponse()` auf, nachdem die Listener-Funktion zurückgekehrt ist.

          > [!NOTE]
          > Promise als Rückgabewert wird in Chrome erst unterstützt, wenn [Chrome Fehler 1185241](https://crbug.com/1185241) behoben ist. Alternativ [return true and use sendResponse](#senden_einer_asynchronen_antwort_mithilfe_von_sendresponse).

    Die `listener`-Funktion kann entweder ein Boolean oder ein {{jsxref("Promise")}} zurückgeben.

    > [!NOTE]
    > Wenn Sie eine asynchrone Funktion an `addListener()` übergeben, gibt der Listener für jede empfangene Nachricht ein Promise zurück, wodurch andere Listener am Antworten gehindert werden:
    >
    > ```js example-bad
    > // tun Sie dies nicht
    > browser.runtime.onMessage.addListener(async (data, sender) => {
    >   if (data.type === "handle_me") {
    >     return "done";
    >   }
    > });
    > ```
    >
    > Angenommen, Sie möchten, dass der Listener nur auf Nachrichten eines bestimmten Typs antwortet. In diesem Fall müssen Sie den Listener als nicht-asychrone Funktion definieren und nur für die Nachrichten, auf die der Listener antworten soll, ein Promise zurückgeben — und andernfalls false oder undefined zurückgeben:
    >
    > ```js example-good
    > browser.runtime.onMessage.addListener((data, sender) => {
    >   if (data.type === "handle_me") {
    >     return Promise.resolve("done");
    >   }
    >   return false;
    > });
    > ```

## Beispiele

### Einfaches Beispiel

Dieses Inhalts-Skript hört auf Klick-Ereignisse auf der Webseite. Wenn der Klick auf einen Link erfolgt, sendet es eine Nachricht mit der Ziel-URL an die Hintergrund-Seite:

```js
// content-script.js

window.addEventListener("click", notifyExtension);

function notifyExtension(e) {
  if (e.target.tagName !== "A") {
    return;
  }
  browser.runtime.sendMessage({ url: e.target.href });
}
```

Das Hintergrund-Skript hört auf diese Nachrichten und zeigt eine Benachrichtigung mithilfe der [`notifications`](/de/docs/Mozilla/Add-ons/WebExtensions/API/notifications)-API an:

```js
// background-script.js

browser.runtime.onMessage.addListener(notify);

function notify(message) {
  browser.notifications.create({
    type: "basic",
    iconUrl: browser.extension.getURL("link.png"),
    title: "You clicked a link!",
    message: message.url,
  });
}
```

### Senden einer synchronen Antwort

Dieses Inhalts-Skript sendet eine Nachricht an das Hintergrund-Skript, wenn der Benutzer auf die Seite klickt. Es protokolliert auch jede Antwort, die vom Hintergrund-Skript gesendet wird:

```js
// content-script.js

function handleResponse(message) {
  console.log(`background script sent a response: ${message.response}`);
}

function handleError(error) {
  console.log(`Error: ${error}`);
}

function sendMessage(e) {
  const sending = browser.runtime.sendMessage({
    content: "message from the content script",
  });
  sending.then(handleResponse, handleError);
}

window.addEventListener("click", sendMessage);
```

Hier ist eine Version des entsprechenden Hintergrund-Skripts, das eine Antwort synchron aus dem Listener sendet:

```js
// background-script.js

function handleMessage(request, sender, sendResponse) {
  console.log(`content script sent a message: ${request.content}`);
  sendResponse({ response: "response from background script" });
}

browser.runtime.onMessage.addListener(handleMessage);
```

Und hier ist eine weitere Version, die {{jsxref("Promise.resolve()")}} verwendet:

```js
// background-script.js

function handleMessage(request, sender, sendResponse) {
  console.log(`content script sent a message: ${request.content}`);
  return Promise.resolve({ response: "response from background script" });
}

browser.runtime.onMessage.addListener(handleMessage);
```

### Senden einer asynchronen Antwort mithilfe von sendResponse

Hier ist eine alternative Version des Hintergrund-Skripts aus dem vorherigen Beispiel. Es sendet eine Antwort asynchron, nachdem der Listener zurückkehrt. Beachten Sie `return true;` im Listener: Dies teilt dem Browser mit, dass Sie beabsichtigen, das `sendResponse`-Argument nach der Rückkehr des Listeners zu verwenden.

```js
// background-script.js

function handleMessage(request, sender, sendResponse) {
  console.log(`content script sent a message: ${request.content}`);
  setTimeout(() => {
    sendResponse({ response: "async response from background script" });
  }, 1000);
  return true;
}

browser.runtime.onMessage.addListener(handleMessage);
```

> [!WARNING]
> Präpendieren Sie nicht `async` zur Funktion. Das Präpendieren von `async` ändert die Bedeutung in das [Senden einer asynchronen Antwort mit einem Versprechen (Promise)](#senden_einer_asynchronen_antwort_mit_einem_promise), was faktisch dasselbe ist wie `sendResponse(true)`.

### Senden einer asynchronen Antwort mit einem Promise

> [!NOTE]
> Promise als Rückgabewert wird in Chrome erst unterstützt, wenn [Chrome Fehler 1185241](https://crbug.com/1185241) behoben ist. Alternativ [return true und verwenden Sie `sendResponse`](#senden_einer_asynchronen_antwort_mithilfe_von_sendresponse).

Dieses Inhalts-Skript erfasst den ersten `<a>`-Link auf der Seite und sendet eine Nachricht, um zu fragen, ob der Standort des Links als Lesezeichen gespeichert ist. Es erwartet eine boolesche Antwort (`true`, wenn der Standort als Lesezeichen gespeichert ist, `false` andernfalls):

```js
// content-script.js

const firstLink = document.querySelector("a");

function handleResponse(isBookmarked) {
  if (isBookmarked) {
    firstLink.classList.add("bookmarked");
  }
}

browser.runtime
  .sendMessage({
    url: firstLink.href,
  })
  .then(handleResponse);
```

Hier ist das Hintergrund-Skript. Es verwendet `{{WebExtAPIRef("bookmarks.search()")}}`, um zu überprüfen, ob der Link als Lesezeichen gespeichert ist, was ein {{jsxref("Promise")}} zurückgibt:

```js
// background-script.js

function isBookmarked(message, sender, response) {
  return browser.bookmarks
    .search({
      url: message.url,
    })
    .then((results) => results.length > 0);
}

browser.runtime.onMessage.addListener(isBookmarked);
```

Wenn der asynchrone Handler kein Promise zurückgibt, können Sie explizit ein Promise konstruieren. Dieses eher konstruierte Beispiel sendet eine Antwort nach einer Verzögerung von 1 Sekunde, unter Verwendung von [`setTimeout()`](/de/docs/Web/API/Window/setTimeout):

```js
// background-script.js

function handleMessage(request, sender, sendResponse) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({ response: "async response from background script" });
    }, 1000);
  });
}

browser.runtime.onMessage.addListener(handleMessage);
```

{{WebExtExamples}}

## Browser-Kompatibilität

{{Compat}}

> [!NOTE]
> Diese API basiert auf der [`chrome.runtime`](https://developer.chrome.com/docs/extensions/reference/api/runtime#event-onMessage)-API von Chromium. Diese Dokumentation ist abgeleitet von [`runtime.json`](https://chromium.googlesource.com/chromium/src/+/master/extensions/common/api/runtime.json) im Chromium-Code.

<!--
// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
-->
