---
title: webNavigation.onCreatedNavigationTarget
slug: Mozilla/Add-ons/WebExtensions/API/webNavigation/onCreatedNavigationTarget
l10n:
  sourceCommit: 5c5ee35d66ac24bc6513c14f120750c74d779d20
---

{{AddonSidebar}}

Wird ausgelöst, wenn ein neues Fenster oder ein neuer Tab in einem vorhandenen Fenster erstellt wird, um das Ziel einer Navigation zu hosten. Zum Beispiel wird dieses Ereignis gesendet, wenn:

- der Benutzer einen Link in einem neuen Tab oder Fenster öffnet
- eine Webseite eine Ressource in einem neuen Tab oder Fenster mit [`window.open()`](/de/docs/Web/API/Window/open) lädt (beachten Sie jedoch, dass das Ereignis nicht gesendet wird, wenn der Popup-Blocker des Browsers das Laden blockiert).

Das Ereignis wird nicht gesendet, wenn ein Tab oder Fenster ohne ein Navigation Target erstellt wird (zum Beispiel, wenn der Benutzer einen neuen Tab durch Drücken von <kbd>Strg+T</kbd> öffnet).

Wenn dieses Ereignis ausgelöst wird, wird es vor {{WebExtAPIRef("webNavigation.onBeforeNavigate")}} ausgelöst.

## Syntax

```js-nolint
browser.webNavigation.onCreatedNavigationTarget.addListener(
  listener,                   // function
  filter                      // optional object
)
browser.webNavigation.onCreatedNavigationTarget.removeListener(listener)
browser.webNavigation.onCreatedNavigationTarget.hasListener(listener)
```

Ereignisse haben drei Funktionen:

- `addListener(listener)`
  - : Fügt diesem Ereignis einen Listener hinzu.
- `removeListener(listener)`
  - : Beendet das Zuhören für dieses Ereignis. Das Argument `listener` ist der zu entfernende Listener.
- `hasListener(listener)`
  - : Überprüft, ob `listener` für dieses Ereignis registriert ist. Gibt `true` zurück, wenn es zuhört, andernfalls `false`.

## addListener-Syntax

### Parameter

- `listener`

  - : Die Funktion, die aufgerufen wird, wenn dieses Ereignis auftritt. Der Funktion wird dieses Argument übergeben:

    - `details`
      - : `object`. Details über das Navigationsereignis. Weitere Informationen finden Sie im Abschnitt [details](#details).

- `filter` {{optional_inline}}
  - : `object`. Ein Objekt, das eine einzelne Eigenschaft `url` enthält, die ein `Array` von {{WebExtAPIRef("events.UrlFilter")}} Objekten ist. Wenn Sie diesen Parameter einschließen, wird das Ereignis nur für Übergänge zu URLs ausgelöst, die mit mindestens einem `UrlFilter` im Array übereinstimmen. Wenn Sie diesen Parameter weglassen, wird das Ereignis für alle Übergänge ausgelöst. Beachten Sie, dass `filter` in Firefox nicht unterstützt wird.

## Zusätzliche Objekte

### details

- `sourceFrameId`
  - : `integer`. ID des Frames, von dem aus die Navigation initiiert wird. `0` zeigt an, dass der Frame der obere Browsing-Kontext des Tabs ist, nicht ein verschachteltes {{HTMLElement("iframe")}}. Ein positiver Wert zeigt, dass die Navigation von einem verschachtelten iframe aus initiiert wird. Frame-IDs sind eindeutig für einen gegebenen Tab und Prozess.
- `processId` {{optional_inline}} {{deprecated_inline}}
  - : `integer`. Dieser Wert wird in modernen Browsern nicht gesetzt. Als er gesetzt wurde, repräsentierte er die ID des Prozesses, von dem die Navigation ausging.
- `sourceTabId`
  - : `integer`. Die ID des Tabs, von dem aus die Navigation initiiert wird. Zum Beispiel, wenn der Benutzer einen Link in einem neuen Tab öffnet, ist dies die ID des Tabs, der den Link enthält.
- `tabId`
  - : `integer`. Die ID des neu erstellten Tabs.
- `timeStamp`
  - : `number`. Der Zeitpunkt, zu dem der Browser das Navigation Target erstellt hat, in [Millisekunden seit der Epoche](https://de.wikipedia.org/wiki/Unixzeit).
- `url`
  - : `string`. Die URL, die im neuen Tab geladen wird.
- `windowId`
  - : `number`. Die ID des Fensters, in dem der neue Tab erstellt wird.

## Browser-Kompatibilität

{{Compat}}

## Beispiele

Protokolliert die Ziel-URL, die Quell-Tab-ID und die Quell-Frame-ID für `onCreatedNavigationTarget`, wenn der Hostname des Ziels "example.com" enthält oder mit "developer" beginnt.

```js
const filter = {
  url: [{ hostContains: "example.com" }, { hostPrefix: "developer" }],
};

function logOnCreatedNavigationTarget(details) {
  console.log(`onCreatedNavigationTarget: ${details.url}`);
  console.log(details.sourceTabId);
  console.log(details.sourceFrameId);
}

browser.webNavigation.onCreatedNavigationTarget.addListener(
  logOnCreatedNavigationTarget,
  filter,
);
```

{{WebExtExamples}}

> [!NOTE]
> Diese API basiert auf Chromiums [`chrome.webNavigation`](https://developer.chrome.com/docs/extensions/reference/api/webNavigation#event-onBeforeNavigate) API. Diese Dokumentation basiert auf [`web_navigation.json`](https://chromium.googlesource.com/chromium/src/+/master/chrome/common/extensions/api/web_navigation.json) im Chromium-Code.

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
