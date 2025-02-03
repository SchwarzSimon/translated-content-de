---
title: "RTCSessionDescription: sdp-Eigenschaft"
short-title: sdp
slug: Web/API/RTCSessionDescription/sdp
l10n:
  sourceCommit: d0e6d8d712a33b9d3c7a9fb9a8ba85d4dd1b7002
---

{{APIRef("WebRTC")}}

Die Eigenschaft **`RTCSessionDescription.sdp`** ist ein schreibgeschützter
String, der die {{Glossary("SDP", "SDP")}} enthält, die die Sitzung beschreibt.

## Wert

Der Wert ist ein String, der eine SDP-Nachricht enthält, ähnlich dieser:

```plain
v=0
o=alice 2890844526 2890844526 IN IP4 host.anywhere.com
s=
c=IN IP4 host.anywhere.com
t=0 0
m=audio 49170 RTP/AVP 0
a=rtpmap:0 PCMU/8000
m=video 51372 RTP/AVP 31
a=rtpmap:31 H261/90000
m=video 53000 RTP/AVP 32
a=rtpmap:32 MPV/90000
```

## Beispiel

```js
// The remote description has been set previously on pc, an RTCPeerConnection

alert(pc.remoteDescription.sdp);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [WebRTC](/de/docs/Web/API/WebRTC_API)
- Der Standard für die Verwendung von SDP in einem Offer/Answer-Protokoll {{rfc("3264")}}.
