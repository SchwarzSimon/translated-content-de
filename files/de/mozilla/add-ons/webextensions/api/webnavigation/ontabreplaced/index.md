---
title: webNavigation.onTabReplaced
slug: Mozilla/Add-ons/WebExtensions/API/webNavigation/onTabReplaced
l10n:
  sourceCommit: 5c5ee35d66ac24bc6513c14f120750c74d779d20
---

{{AddonSidebar}}

Wird ausgelöst, wenn der Inhalt des Tabs durch einen anderen (in der Regel zuvor vorgerenderten) Tab ersetzt wird.

## Syntax

```js-nolint
browser.webNavigation.onTabReplaced.addListener(
  listener,                   // function
  filter                      // optional object
);
browser.webNavigation.onTabReplaced.removeListener(listener)
browser.webNavigation.onTabReplaced.hasListener(listener)
```

Ereignisse haben drei Funktionen:

- `addListener(listener)`
  - : Fügt diesem Ereignis einen Listener hinzu.
- `removeListener(listener)`
  - : Stoppt das Lauschen auf dieses Ereignis. Das Argument `listener` ist der zu entfernende Listener.
- `hasListener(listener)`
  - : Überprüft, ob `listener` für dieses Ereignis registriert ist. Gibt `true` zurück, wenn er lauscht, andernfalls `false`.

## addListener-Syntax

### Parameter

- `listener`

  - : Die Funktion, die aufgerufen wird, wenn dieses Ereignis eintritt. Der Funktion wird dieses Argument übergeben:

    - `details`
      - : `object`. Siehe den Abschnitt [details](#details) für weitere Informationen.

## Zusätzliche Objekte

### details

- `replacedTabId`
  - : `integer`. Die ID des Tabs, der ersetzt wurde.
- `tabId`
  - : `integer`. Die ID des Tabs, der den alten Tab ersetzt hat.
- `timeStamp`
  - : `number`. Die Zeit, wann der Austausch stattfand, in [Millisekunden seit der Epoche](https://en.wikipedia.org/wiki/Unix_time).

## Browser-Kompatibilität

{{Compat}}

## Beispiele

```js
function logOnTabReplaced(details) {
  console.log(`onTabReplaced ${details}`);
}

browser.webNavigation.onTabReplaced.addListener(logOnTabReplaced);
```

{{WebExtExamples}}

> [!NOTE]
> Diese API basiert auf der [`chrome.webNavigation`](https://developer.chrome.com/docs/extensions/reference/api/webNavigation#event-onTabReplaced) API von Chromium. Diese Dokumentation ist abgeleitet von [`web_navigation.json`](https://chromium.googlesource.com/chromium/src/+/master/chrome/common/extensions/api/web_navigation.json) im Chromium-Code.

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
