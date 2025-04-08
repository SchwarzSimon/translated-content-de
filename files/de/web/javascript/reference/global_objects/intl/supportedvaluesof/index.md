---
title: Intl.supportedValuesOf()
slug: Web/JavaScript/Reference/Global_Objects/Intl/supportedValuesOf
l10n:
  sourceCommit: c74f900e48b1f9b0a65af3c35335d9e08adf92b7
---

{{JSRef}}

Die statische Methode **`Intl.supportedValuesOf()`** gibt ein Array zurück, das die von der Implementierung unterstützten Kalender-, Sortier-, Währungs-, Zahlensystem- oder Einheit-Werte enthält.

Duplikate werden weggelassen und das Array wird in aufsteigender lexikografischer Reihenfolge sortiert (genauer gesagt, mit {{jsxref("Array/sort", "Array.prototype.sort()")}} und einer `undefined` Vergleichsfunktion).

Die Methode kann verwendet werden, um zu testen, ob Werte in einer bestimmten Implementierung unterstützt werden, und bei Bedarf nur dann ein Polyfill herunterzuladen. Sie kann auch verwendet werden, um Benutzeroberflächen zu erstellen, die es den Nutzern ermöglichen, ihre bevorzugten lokalisierten Werte auszuwählen, beispielsweise wenn die Benutzeroberfläche mit WebGL oder serverseitig erstellt wird.

Diese Methode ist ortsunabhängig: Es ist möglich, dass bestimmte Bezeichner nur in bestimmten Gebietsschemen unterstützt oder bevorzugt werden. Wenn Sie die bevorzugten Werte für ein bestimmtes Gebietsschema ermitteln möchten, sollten Sie das Objekt {{jsxref("Intl.Locale")}} verwenden, wie z.B. {{jsxref("Intl/Locale/getCalendars", "Intl.Locale.prototype.getCalendars()")}}.

{{InteractiveExample("JavaScript Demo: Intl.supportedValuesOf()", "taller")}}

```js interactive-example
console.log(Intl.supportedValuesOf("calendar"));
console.log(Intl.supportedValuesOf("collation"));
console.log(Intl.supportedValuesOf("currency"));
console.log(Intl.supportedValuesOf("numberingSystem"));
console.log(Intl.supportedValuesOf("timeZone"));
console.log(Intl.supportedValuesOf("unit"));
// Expected output: Array ['key'] (for each key)

try {
  Intl.supportedValuesOf("someInvalidKey");
} catch (err) {
  console.log(err.toString());
  // Expected output: RangeError: invalid key: "someInvalidKey"
}
```

## Syntax

```js-nolint
Intl.supportedValuesOf(key)
```

### Parameter

- `key`
  - : Ein Schlüsselstring, der die Kategorie der zurückzugebenden Werte angibt. Dies ist einer von:
    - `"calendar"`: siehe [unterstützte Kalendertypen](#unterstützte_kalendertypen)
    - `"collation"`: siehe [unterstützte Sortiertypen](#unterstützte_sortiertypen)
    - `"currency"`: siehe [unterstützte Währungskennungen](#unterstützte_währungskennungen)
    - `"numberingSystem"`: siehe [unterstützte Zahlensystemtypen](#unterstützte_zahlensystemtypen)
    - `"timeZone"`: siehe [unterstützte Zeitzonenkennungen](#unterstützte_zeitzonenkennungen)
    - `"unit"`: siehe [unterstützte Einheitenkennungen](#unterstützte_einheitenkennungen)

### Rückgabewert

Ein sortiertes Array von eindeutigen Stringwerten, die die Werte anzeigen, die von der Implementierung für den gegebenen Schlüssel unterstützt werden. Die möglicherweise zurückgegebenen Werte sind unten aufgelistet.

#### Unterstützte Kalendertypen

Nachfolgend sind alle Werte aufgeführt, die in Browsern allgemein für den Schlüssel `calendar` unterstützt werden. Diese Werte können für die `calendar`-Option oder den `ca`- [Unicode-Erweiterungsschlüssel](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl#locales_argument) verwendet werden, wenn Objekte wie {{jsxref("Intl.DateTimeFormat")}} erstellt werden, sowie zum Erstellen von {{jsxref("Temporal")}}-Datumsobjekten.

| Wert               | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `buddhist`         | Thailändischer buddhistischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                 |
| `chinese`          | Traditioneller chinesischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                   |
| `coptic`           | Koptischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `dangi`            | Traditioneller koreanischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                   |
| `ethioaa`          | Äthiopischer Kalender, Amete Alem, Variante mit einer Ära (Epoche ca. 5493 v. Chr.)                                                                                                                                                                                                                                                                                                                                                    |
| `ethiopic`         | Äthiopischer Kalender, Amete Mihret, Variante mit zwei Ären (Epoche ca. 8 n. Chr., Amete Alem für Jahre vor Amete Mihret)                                                                                                                                                                                                                                                                                                              |
| `gregory`          | Gregorianischer Kalender (proleptisch, _kein_ Julianisch-Hybrid)                                                                                                                                                                                                                                                                                                                                                                       |
| `hebrew`           | Traditioneller hebräischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                    |
| `indian`           | Indischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `islamic`          | Hijri-Kalender, unbestimmter Algorithmus. **Hinweis:** Ab April 2025 ist dies eine astronomische Simulation, deren Parameter undokumentiert sind und von der nicht bekannt ist, dass sie mit einer bestimmten Hijri-Kalender-Variante aus nicht-softwaremäßigen Kontexten übereinstimmt. Für gut spezifizierte Ergebnisse verwenden Sie eine der drei spezifischen Varianten: `islamic-umalqura`, `islamic-tbla` oder `islamic-civil`. |
| `islamic-umalqura` | Hijri-Kalender, Umm al-Qura (verwendet KACST-berechnete Monate vom Beginn 1300 AH bis Ende 1600 AH und fällt außerhalb dieses Bereichs auf `islamic-civil` zurück)                                                                                                                                                                                                                                                                     |
| `islamic-tbla`     | Hijri-Kalender, tabellarisch/regelbasiert mit Schaltjahrregel II (Schaltjahre 2,5,7,10,13,16,18,21,24,26,29 im 30-jährigen Zyklus (nummeriert ab 1)) und Donnerstag/astronomische Epoche (15. Juli 622 Julian / 0622-07-18 ISO)                                                                                                                                                                                                        |
| `islamic-civil`    | Hijri-Kalender, tabellarisch/regelbasiert mit Schaltjahrregel II (Schaltjahre 2,5,7,10,13,16,18,21,24,26,29 im 30-jährigen Zyklus (nummeriert ab 1)) und Freitag/epoche (16. Juli 622 Julian / 0622-07-19 ISO)                                                                                                                                                                                                                         |
| `iso8601`          | ISO-Kalender (Variante des gregorianischen Kalenders mit wochenregel- und formatierungsunabhängigen Parametern)                                                                                                                                                                                                                                                                                                                        |
| `japanese`         | Japanischer Kaiserlicher Kalender (fügt für jeden neuen Kaiser eine Ära hinzu, sodass das Ausgabejahr und die Ära für ein zukünftiges Datum möglicherweise nicht zum Eingabejahr und zur Ära passen, wenn Ihr Code in einer zukünftigen Engine-Version ausgeführt wird)                                                                                                                                                                |
| `persian`          | Persischer Kalender                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `roc`              | Kalender der Republik China                                                                                                                                                                                                                                                                                                                                                                                                            |

Die unten angegebenen Typen sind in CLDR angegeben, haben aber keine Implementierungen, die sich von den oben genannten Kalendern in Browsern unterscheiden.

| Wert                             | Beschreibung                                   | Anmerkungen                                                                                                                                                                                                                                                            |
| -------------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `islamicc` {{deprecated_inline}} | Ziviler (algorithmischer) Arabischer Kalender. | Dies ist ein Alias für `islamic-civil` und wird daher nicht von `supportedValuesOf()` zurückgegeben. Verwenden Sie stattdessen `islamic-civil`.                                                                                                                        |
| `islamic-rgsa`                   | Hijri-Kalender, Sichtung in Saudi-Arabien      | Browser haben keine historischen Sichtungsdaten und zukünftige Sichtungen haben noch nicht stattgefunden. Ab April 2025 führt dieser Kalender zu demselben Verhalten wie `islamic`. Verwenden Sie `islamic-umalqura` für eine Mekka-basierte astronomische Berechnung. |

Referenzen:

- [CLDR Kalendertyp-Schlüssel](https://github.com/unicode-org/cldr/blob/main/common/bcp47/calendar.xml)
- [UTS 35, Datumsangaben](https://unicode.org/reports/tr35/tr35-dates.html)
- [Islamische Kalendertypen](https://cldr.unicode.org/development/development-process/design-proposals/islamic-calendar-types) (CLDR Designvorschlag)

#### Unterstützte Sortiertypen

Nachfolgend sind alle Werte aufgeführt, die in Browsern allgemein für den Schlüssel `collation` unterstützt werden. Diese Werte können für die `collation`-Option oder den `co`- [Unicode-Erweiterungsschlüssel](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl#locales_argument) verwendet werden, wenn Objekte wie {{jsxref("Intl.Collator")}} erstellt werden.

| Wert       | Beschreibung                                                                                                                                                                                                                           |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `compat`   | Eine vorherige Version der Reihenfolge für die Kompatibilität (für Arabisch)                                                                                                                                                           |
| `dict`     | Wörterbuchähnliche Sortierreihenfolge (wie in Singhalesisch). Wird auch als `dictionary` erkannt.                                                                                                                                      |
| `emoji`    | Empfohlene Sortierreihenfolge für Emoji-Zeichen                                                                                                                                                                                        |
| `eor`      | Europäische Sortierreihenfolge                                                                                                                                                                                                         |
| `phonebk`  | Telefonbuchartige Sortierreihenfolge (wie in Deutsch). Wird auch als `phonebook` erkannt.                                                                                                                                              |
| `phonetic` | Phonetische Sortierreihenfolge (Sortierung basierend auf der Aussprache; für Lingala)                                                                                                                                                  |
| `pinyin`   | Pinyin-Sortierreihenfolge für Latein und für CJK-Zeichen (wird im Chinesischen verwendet)                                                                                                                                              |
| `searchjl` | Spezieller Sortiertyp für die Suche nach initialem Konsonanten in Koreanisch. **Warnung:** Dieser Sortiertyp ist nicht zum Sortieren gedacht, obwohl Sie ihn nur mit {{jsxref("Intl.Collator")}} mit `usage: "sort"` verwenden können. |
| `stroke`   | Pinyin-Sortierreihenfolge für Latein, Strichreihenfolge für CJK-Zeichen (wird im Chinesischen verwendet)                                                                                                                               |
| `trad`     | Traditionelle Art der Sortierung (wie in Spanisch). Wird auch als `traditional` erkannt.                                                                                                                                               |
| `unihan`   | Pinyin-Sortierreihenfolge für Latein, Unihan Radikal-Strich-Sortierreihenfolge für CJK-Zeichen (wird im Chinesischen verwendet)                                                                                                        |
| `zhuyin`   | Pinyin-Sortierreihenfolge für Latein, Zhuyin-Reihenfolge für Bopomofo und CJK-Zeichen (wird im Chinesischen verwendet)                                                                                                                 |

Die unten angegebenen Typen sind in CLDR-Daten spezifiziert, sind jedoch veraltet, sind von der expliziten Verwendung abgeraten und/oder werden möglicherweise nicht von Browsern als unterstützt angezeigt. Vermeiden Sie die Verwendung dieser:

| Wert                             | Beschreibung                                                                                                                                        | Anmerkungen                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `big5han` {{deprecated_inline}}  | Pinyin-Sortierreihenfolge für Latein, Big5-Zeichensatz-Sortierreihenfolge für CJK-Zeichen (wird im Chinesischen verwendet)                          | Veraltet.                                                                                                                                                                                                                                                                                                                                                      |
| `direct` {{deprecated_inline}}   | Binäre Sortierreihenfolge der Codepunkte (wird im Hindi verwendet)                                                                                  | Veraltet.                                                                                                                                                                                                                                                                                                                                                      |
| `ducet`                          | Die Standard-Reihenfolge der Unicode-Sortierungselementetabelle                                                                                     | Der `ducet`-Sortiertyp ist im Web nicht verfügbar.                                                                                                                                                                                                                                                                                                             |
| `gb2312` {{deprecated_inline}}   | Pinyin-Sortierreihenfolge für Latein, GB2312HAN-Zeichensatz-Sortierreihenfolge für CJK-Zeichen (für Chinesisch). Wird auch als `gb2312han` erkannt. | Veraltet.                                                                                                                                                                                                                                                                                                                                                      |
| `reformed` {{deprecated_inline}} | Reformierte Sortierreihenfolge (wie in Schwedisch)                                                                                                  | Veraltet. Dies ist der alte Name für die Standard-Sortierreihenfolge für Schwedisch [deren Sortierbenennung sich von anderen Sprachen unterschied](https://unicode-org.atlassian.net/browse/CLDR-15603). Da dies der Standard war, fordern Sie `sv` an, anstatt `sv-u-co-reformed` anzufordern.                                                                |
| `search`                         | Spezieller Sortiertyp zur Stringsuchen                                                                                                              | Verwenden Sie diesen nicht als Sortiertyp, da in {{jsxref("Intl.Collator")}} dieser Sortiertyp über die Option `usage: "search"` aktiviert wird. Derzeit gibt es keine API für die Substringsuche, sodass dies derzeit nur gut für das Filtern einer Liste von Zeichenfolgen ist, indem ein vollständigerer Vergleich gegen jedes Listenelement versucht wird. |
| `standard`                       | Standardsortierung für jede Sprache, außer Chinesisch (und ehemals Schwedisch)                                                                      | Verwenden Sie dies nicht explizit. Im Allgemeinen ist es unnötig, dies explizit anzugeben, und dies für Schwedisch anzugeben ist problematisch aufgrund der unterschiedlichen Bedeutung für Schwedisch in der Vergangenheit.                                                                                                                                   |

Referenzen:

- [CLDR Sortiertyp-Schlüssel](https://github.com/unicode-org/cldr/blob/main/common/bcp47/collation.xml)
- [UTS 35, Sortierung](https://unicode.org/reports/tr35/tr35-collation.html)

#### Unterstützte Währungskennungen

Währungskennungen sind drei Buchstaben lange Großbuchstabencodes, die in ISO 4217 definiert sind. Diese Werte können für die `currency`-Option verwendet werden, wenn Objekte wie {{jsxref("Intl.NumberFormat")}} erstellt werden, sowie für {{jsxref("Intl/DisplayNames/of", "Intl.DisplayNames.prototype.of()")}}. Es gibt über 300 Kennungen, die häufig verwendet werden, weshalb wir sie nicht alle auflisten. Für eine vollständige Liste der möglichen Kennungen siehe den [Wikipedia-Artikel](https://en.wikipedia.org/wiki/ISO_4217#List_of_ISO_4217_currency_codes).

Referenzen:

- [CLDR Währungstyp-Schlüssel](https://github.com/unicode-org/cldr/blob/main/common/bcp47/currency.xml)
- [ISO 4217 Währungscodes](https://www.iso.org/iso-4217-currency-codes.html)
- [UTS 35, Währungen](https://unicode.org/reports/tr35/tr35-numbers.html#Currencies)

#### Unterstützte Zahlensystemtypen

Nachfolgend sind alle Werte aufgeführt, die üblicherweise von Browsern für den Schlüssel `numberingSystem` unterstützt werden. Diese Werte können für die `numberingSystem`-Option oder den `nu`- [Unicode-Erweiterungsschlüssel](/de/docs/Web/JavaScript/Reference/Global_Objects/Intl#locales_argument) verwendet werden, wenn Objekte wie {{jsxref("Intl.NumberFormat")}} erstellt werden. Für die Zeilen mit "Ziffernzeichen" übersetzt die Laufzeit die Ziffern einzeln ohne zusätzliche Aktionen. Die anderen, die als "algorithmisch" gekennzeichnet sind, benötigen zusätzliche Algorithmen, um die Ziffern zu übersetzen. Je höher der Unicode-Codepunkt ist, desto neuer ist das Zahlensystem und desto wahrscheinlicher wird es nicht von allen Browsern unterstützt.

| Wert       | Beschreibung                                                                         | Ziffernzeichen                                                                                          |
| ---------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| `adlm`     | Adlam-Ziffern                                                                        | `𞥐𞥑𞥒𞥓𞥔𞥕𞥖𞥗𞥘𞥙` (U+1E950 bis U+1E959)                                                                      |
| `ahom`     | Ahom-Ziffern                                                                         | `𑜰𑜱𑜲𑜳𑜴𑜵𑜶𑜷𑜸𑜹` (U+11730 bis U+11739)                                                                      |
| `arab`     | Arabisch-indische Ziffern                                                            | `٠١٢٣٤٥٦٧٨٩` (U+0660 bis U+0669)                                                                        |
| `arabext`  | Erweitert arabisch-indische Ziffern                                                  | `۰۰۱۲۳۴۵۶۷۸۹` (U+06F0 bis U+06F9)                                                                       |
| `armn`     | Armenische Großbuchstabenziffern                                                     | algorithmisch                                                                                           |
| `armnlow`  | Armenische Kleinbuchstabenziffern                                                    | algorithmisch                                                                                           |
| `bali`     | Balinesische Ziffern                                                                 | `᭐᭑᭒᭓᭔᭕᭖᭗᭘᭙` (U+1B50 bis U+1B59)                                                                        |
| `beng`     | Bengalische Ziffern                                                                  | `০১২৩৪৫৬৭৮৯` (U+09E6 bis U+09EF)                                                                        |
| `bhks`     | Bhiksuki-Ziffern                                                                     | `𑱐𑱑𑱒𑱓𑱔𑱕𑱖𑱗𑱘𑱙` (U+11C50 bis U+11C59)                                                                      |
| `brah`     | Brahmi-Ziffern                                                                       | `𑁦𑁧𑁨𑁩𑁪𑁫𑁬𑁭𑁮𑁯` (U+11066 bis U+1106F)                                                                      |
| `cakm`     | Chakma-Ziffern                                                                       | `𑄶𑄷𑄸𑄹𑄺𑄻𑄼𑄽𑄾𑄿` (U+11136 bis U+1113F)                                                                      |
| `cham`     | Cham-Ziffern                                                                         | `꩐꩑꩒꩓꩔꩕꩖꩗꩘꩙` (U+AA50 bis U+AA59)                                                                        |
| `cyrl`     | Kyrillische Ziffern                                                                  | algorithmisch                                                                                           |
| `deva`     | Devanagari-Ziffern                                                                   | `०१२३४५६७८९` (U+0966 bis U+096F)                                                                        |
| `diak`     | Dives Akuru-Ziffern                                                                  | `𑥐𑥑𑥒𑥓𑥔𑥕𑥖𑥗𑥘𑥙` (U+11950 bis U+11959)                                                                      |
| `ethi`     | Äthiopische Ziffern                                                                  | algorithmisch                                                                                           |
| `fullwide` | Volle-Weite-Ziffern                                                                  | `０１２３４５６７８９` (U+FF10 bis U+FF19)                                                              |
| `gara`     | Garay-Ziffern                                                                        | `𐵀𐵁𐵂𐵃𐵄𐵅𐵆𐵇𐵈𐵉` (U+10D40 bis U+10D49)                                                                      |
| `geor`     | Georgische Ziffern                                                                   | algorithmisch                                                                                           |
| `gong`     | Gunzala Gondi-Ziffern                                                                | `𑶠𑶡𑶢𑶣𑶤𑶥𑶦𑶧𑶨𑶩` (U+11DA0 bis U+11DA9)                                                                      |
| `gonm`     | Masaram Gondi-Ziffern                                                                | `𑵐𑵑𑵒𑵓𑵔𑵕𑵖𑵗𑵘𑵙` (U+11D50 bis U+11D59)                                                                      |
| `grek`     | Griechische Großbuchstabenziffern                                                    | algorithmisch                                                                                           |
| `greklow`  | Griechische Kleinbuchstabenziffern                                                   | algorithmisch                                                                                           |
| `gujr`     | Gujarati-Ziffern                                                                     | `૦૧૨૩૪૫૬૭૮૯` (U+0AE6 bis U+0AEF)                                                                        |
| `gukh`     | Gurung Khema-Ziffern                                                                 | `𖄰𖄱𖄲𖄳𖄴𖄵𖄶𖄷𖄸𖄹` (U+16130 bis U+16139)                                                                      |
| `guru`     | Gurmukhi-Ziffern                                                                     | `੦੧੨੩੪੫੬੭੮੯` (U+0A66 bis U+0A6F)                                                                        |
| `hanidays` | Han-Zeichen für Tag-zu-Monat-Zählung in Mond- oder anderen traditionellen Kalendern  |                                                                                                         |
| `hanidec`  | Positionelles Dezimalsystem, das chinesische Zahlenideografien als Ziffern verwendet | `〇一二三四五六七八九` (U+3007, U+4E00, U+4E8C, U+4E09, U+56DB, U+4E94, U+516D, U+4E03, U+516B, U+4E5D) |
| `hans`     | Vereinfachte chinesische Ziffern                                                     | algorithmisch                                                                                           |
| `hansfin`  | Vereinfachte chinesische Finanzziffern                                               | algorithmisch                                                                                           |
| `hant`     | Traditionelle chinesische Ziffern                                                    | algorithmisch                                                                                           |
| `hantfin`  | Traditionelle chinesische Finanzziffern                                              | algorithmisch                                                                                           |
| `hebr`     | Hebräische Ziffern                                                                   | algorithmisch                                                                                           |
| `hmng`     | Pahawh Hmong-Ziffern                                                                 | `𖭕𖭑𖭒𖭓𖭔𖭕𖭖𖭗𖭘𖭙` (U+16B50 bis U+16B59)                                                                      |
| `hmnp`     | Nyiakeng Puachue Hmong-Ziffern                                                       | `𞅀𞅁𞅂𞅃𞅄𞅅𞅆𞅇𞅈𞅉` (U+1E140 bis U+1E149)                                                                      |
| `java`     | Javanesische Ziffern                                                                 | `꧐꧑꧒꧓꧔꧕꧖꧗꧘꧙` (U+A9D0 bis U+A9D9)                                                                        |
| `jpan`     | Japanische Ziffern                                                                   | algorithmisch                                                                                           |
| `jpanfin`  | Japanische Finanzziffern                                                             | algorithmisch                                                                                           |
| `jpanyear` | Japanische Gannen-Jahreszählung für japanischen Kalender                             | algorithmisch                                                                                           |
| `kali`     | Kayah Li-Ziffern                                                                     | `꤀꤁꤂꤃꤄꤅꤆꤇꤈꤉` (U+A900 bis U+A909)                                                                        |
| `kawi`     | Kawi-Ziffern                                                                         | `𑽐𑽑𑽒𑽓𑽔𑽕𑽖𑽗𑽘𑽙` (U+11F50 bis U+11F59)                                                                      |
| `khmr`     | Khmer-Ziffern                                                                        | `០១២៣៤៥៦៧៨៩` (U+17E0 bis U+17E9)                                                                        |
| `knda`     | Kannada-Ziffern                                                                      | `೦೧೨೩೪೫೬೭೮೯` (U+0CE6 bis U+0CEF)                                                                        |
| `krai`     | Kirat Rai-Ziffern                                                                    | `𖵰𖵱𖵲𖵳𖵴𖵵𖵶𖵷𖵸𖵹` (U+16D70 bis U+16D79)                                                                      |
| `lana`     | Tai Tham Hora (säkular) Ziffern                                                      | `᪀᪁᪂᪃᪄᪅᪆᪇᪈᪉` (U+1A80 bis U+1A89)                                                                        |
| `lanatham` | Tai Tham (kirchlich) Ziffern                                                         | `᪐᪑᪒᪓᪔᪕᪖᪗᪘᪙` (U+1A90 bis U+1A99)                                                                        |
| `laoo`     | Lao-Ziffern                                                                          | `໐໑໒໓໔໕໖໗໘໙` (U+0ED0 bis U+0ED9)                                                                        |
| `latn`     | Lateinische Ziffern                                                                  | `0123456789` (U+0030 bis U+0039)                                                                        |
| `lepc`     | Lepcha-Ziffern                                                                       | `᱀᱁᱂᱃᱄᱅᱆᱇᱈᱉` (U+1C40 bis U+1C49)                                                                        |
| `limb`     | Limbu-Ziffern                                                                        | `᥆᥇᥈᥉᥊᥋᥌᥍᥎᥏` (U+1946 bis U+194F)                                                                        |
| `mathbold` | Mathematische Fettziffern                                                            | `𝟎𝟏𝟐𝟑𝟒𝟓𝟔𝟕𝟖𝟗` (U+1D7CE bis U+1D7D7)                                                                      |
| `mathdbl`  | Mathematische Doppelstrichziffern                                                    | `𝟘𝟙𝟚𝟛𝟜𝟝𝟞𝟟𝟠𝟡` (U+1D7D8 bis U+1D7E1)                                                                      |
| `mathmono` | Mathematische Monospace-Ziffern                                                      | `𝟶𝟷𝟸𝟹𝟺𝟻𝟼𝟽𝟾𝟿` (U+1D7F6 bis U+1D7FF)                                                                      |
| `mathsanb` | Mathematische Sans-serif-Fettziffern                                                 | `𝟬𝟭𝟮𝟯𝟰𝟱𝟲𝟳𝟴𝟵` (U+1D7EC bis U+1D7F5)                                                                      |
| `mathsans` | Mathematische Sans-serif-Ziffern                                                     | `𝟢𝟣𝟤𝟥𝟦𝟧𝟨𝟩𝟪𝟫` (U+1D7E2 bis U+1D7EB)                                                                      |
| `mlym`     | Malaiische Ziffern                                                                   | `൦൧൨൩൪൫൬൭൮൯` (U+0D66 bis U+0D6F)                                                                        |
| `modi`     | Modi-Ziffern                                                                         | `𑙐𑙑𑙒𑙓𑙔𑙕𑙖𑙗𑙘𑙙` (U+11650 bis U+11659)                                                                      |
| `mong`     | Mongolische Ziffern                                                                  | `᠐᠑᠒᠓᠔᠕᠖᠗᠘᠙` (U+1810 bis U+1819)                                                                        |
| `mroo`     | Mro-Ziffern                                                                          | `𖩠𖩡𖩢𖩣𖩤𖩥𖩦𖩧𖩨𖩩` (U+16A60 bis U+16A69)                                                                      |
| `mtei`     | Meetei Mayek-Ziffern                                                                 | `꯰꯱꯲꯳꯴꯵꯶꯷꯸꯹` (U+ABF0 bis U+ABF9)                                                                        |
| `mymr`     | Myanmar-Ziffern                                                                      | `၀๑๒๓๔๕๖๗๘၉` (U+1040 bis U+1049)                                                                        |
| `mymrepka` | Myanmar Östliche Pwo Karen-Ziffern                                                   | `𑛚𑛛𑛜𑛝𑛞𑛟𑛠𑛡𑛢𑛣` (U+116DA bis U+116E3)                                                                      |
| `mymrpao`  | Myanmar Pao-Ziffern                                                                  | `𑛐𑛑𑛒𑛓𑛔𑛕𑛖𑛗𑛘𑛙` (U+116D0 bis U+116D9)                                                                      |
| `mymrshan` | Myanmar Shan-Ziffern                                                                 | `႐႑႒႓႔႕႖႗႘႙` (U+1090 bis U+1099)                                                                        |
| `mymrtlng` | Myanmar Tai Laing-Ziffern                                                            | `꧰꧱꧲꧳꧴꧵꧶꧷꧸꧹` (U+A9F0 bis U+A9F9)                                                                        |
| `nagm`     | Nag Mundari-Ziffern                                                                  | `𞓰𞓱𞓲𞓳𞓴𞓵𞓶𞓷𞓸𞓹` (U+1E4F0 bis U+1E4F9)                                                                      |
| `newa`     | Newa-Ziffern                                                                         | `𑑐𑑑𑑒𑑓𑑔𑑕𑑖𑑗𑑘𑑙` (U+11450 bis U+11459)                                                                      |
| `nkoo`     | N'Ko-Ziffern                                                                         | `߀߁߂߃߄߅߆߇߈߉` (U+07C0 bis U+07C9)                                                                        |
| `olck`     | Ol Chiki-Ziffern                                                                     | `᱐᱑᱒᱓᱔᱕᱖᱗᱘᱙` (U+1C50 bis U+1C59)                                                                        |
| `onao`     | Ol Onal-Ziffern                                                                      | `𞗱𞗲𞗳𞗴𞗵𞗶𞗷𞗸𞗹𞗺` (U+1E5F1 bis U+1E5FA)                                                                      |
| `orya`     | Oriya-Ziffern                                                                        | `୦୧୨୩୪୫୬୭୮୯` (U+0B66 bis U+0B6F)                                                                        |
| `osma`     | Osmanya-Ziffern                                                                      | `𐒠𐒡𐒢𐒣𐒤𐒥𐒦𐒧𐒨𐒩` (U+104A0 bis U+104A9)                                                                      |
| `outlined` | Veraltete aufgeführte Rechneziffern                                                  | `𜳰𜳱𜳲𜳳𜳴𜳵𜳶𜳷𜳸𜳹` (U+1CCF0 bis U+1CCF9)                                                                      |
| `rohg`     | Hanifi Rohingya-Ziffern                                                              | `𐴰𐴱𐴲𐴳𐴴𐴵𐴶𐴷𐴸𐴹` (U+10D30 bis U+10D39)                                                                      |
| `roman`    | Römische Großbuchstabenziffern                                                       | algorithmisch                                                                                           |
| `romanlow` | Römische Kleinbuchstabenziffern                                                      | algorithmisch                                                                                           |
| `saur`     | Saurashtra-Ziffern                                                                   | `꣐꣑꣒꣓꣔꣕꣖꣗꣘꣙` (U+A8D0 bis U+A8D9)                                                                        |
| `segment`  | Veraltete computergestützte segmentierte Ziffern                                     | `🯰🯱🯲🯳🯴🯵🯶🯷🯸🯹` (U+1FBF0 bis U+1FBF9)                                                                      |
| `shrd`     | Sharada-Ziffern                                                                      | `𑇐𑇑𑇒𑇓𑇔𑇕𑇖𑇗𑇘𑇙` (U+111D0 bis U+111D9)                                                                      |
| `sind`     | Khudawadi-Ziffern                                                                    | `𑋰𑋱𑋲𑋳𑋴𑋵𑋶𑋷𑋸𑋹` (U+112F0 bis U+112F9)                                                                      |
| `sinh`     | Singhalesische Lith-Ziffern                                                          | `෦෧෨෩෪෫෬෭෮෯` (U+0DE6 bis U+0DEF)                                                                        |
| `sora`     | Sora_Sompeng-Ziffern                                                                 | `𑃰𑃱𑃲𑃳𑃴𑃵𑃶𑃷𑃸𑃹` (U+110F0 bis U+110F9)                                                                      |
| `sund`     | Sundanesische Ziffern                                                                | `᮰᮱᮲᮳᮴᮵᮶᮷᮸᮹` (U+1BB0 bis U+1BB9)                                                                        |
| `sunu`     | Sunuwar-Ziffern                                                                      | `𑯰𑯱𑯲𑯳𑯴𑯵𑯶𑯷𑯸𑯹` (U+11BF0 bis U+11BF9)                                                                      |
| `takr`     | Takri-Ziffern                                                                        | `𑛀𑛁𑛂𑛃𑛄𑛅𑛆𑛇𑛈𑛉` (U+116C0 bis U+116C9)                                                                      |
| `talu`     | Neu Tai Lue-Ziffern                                                                  | `᧐᧑᧒᧓᧔᧕᧖᧗᧘᧙` (U+19D0 bis U+19D9)                                                                        |
| `taml`     | Tamil-Ziffern                                                                        | algorithmisch                                                                                           |
| `tamldec`  | Moderne Tamil-Dezimalziffern                                                         | `௦௧௨௩௪௫௬௭௮௯` (U+0BE6 bis U+0BEF)                                                                        |
| `telu`     | Telagu-Ziffern                                                                       | `౦౧౨౩౪౫౬౭౮౯` (U+0C66 bis U+0C6F)                                                                        |
| `thai`     | Thailändische Ziffern                                                                | `๐๑๒๓๔๕๖๗๘๙` (U+0E50 bis U+0E59)                                                                        |
| `tibt`     | Tibetische Ziffern                                                                   | `༠༡༢༣༤༥༦༧༨༩` (U+0F20 bis U+0F29)                                                                        |
| `tirh`     | Tirhuta-Ziffern                                                                      | `𑓐𑓑𑓒𑓓𑓔𑓕𑓖𑓗𑓘𑓙` (U+114D0 bis U+114D9)                                                                      |
| `tnsa`     | Tangsa-Ziffern                                                                       | `𖫀𖫁𖫂𖫃𖫄𖫅𖫆𖫇𖫈𖫉` (U+16AC0 bis U+16AC9)                                                                      |
| `vaii`     | Vai-Ziffern                                                                          | `꘠꘡꘢꘣꘤꘥꘦꘧꘨꘩` (U+A620 bis U+A629)                                                                        |
| `wara`     | Warang Citi-Ziffern                                                                  | `𑣠𑣡𑣢𑣣𑣤𑣥𑣦𑣧𑣨𑣩` (U+118E0 bis U+118E9)                                                                      |
| `wcho`     | Wancho-Ziffern                                                                       | `𞋰𞋱𞋲𞋳𞋴𞋵𞋶𞋷𞋸𞋹` (U+1E2F0 bis U+1E2F9)                                                                      |

Es gibt drei spezielle Werte: `native`, `tradition`, und `finance`, deren Bedeutungen ortsabhängig sind und je nach Gebietsschema auf das richtige System aufgelöst werden. Daher werden diese Werte nie von den Methoden `resolvedOptions()` zurückgegeben, aber `Intl.Locale.prototype.numberingSystem` wird (wenn als Eingabe bereitgestellt).

Referenzen:

- [CLDR Zahlensystemtyp-Schlüssel](https://github.com/unicode-org/cldr/blob/main/common/bcp47/number.xml)
- [CLDR Zahlensystemdefinitionen](https://github.com/unicode-org/cldr/blob/main/common/supplemental/numberingSystems.xml)
- [UTS 35, Zahlensysteme](https://unicode.org/reports/tr35/tr35-numbers.html#Numbering_Systems)

#### Unterstützte Zeitzonenkennungen

Unterstützte Zeitzonenkennungen können für die `timeZone`-Option verwendet werden, wenn Objekte wie {{jsxref("Intl.DateTimeFormat")}}, sowie beim Erstellen von {{jsxref("Temporal")}}-Datumsobjekten. Es gibt über 400 Kennungen, die häufig verwendet werden, deshalb werden wir sie nicht alle auflisten. Für eine vollständige Liste der möglichen Kennungen siehe den [Wikipedia-Artikel](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) oder die [IANA-Zeitzonendatenbank](https://www.iana.org/time-zones).

Während Sie die Liste durchsehen, beachten Sie, dass die Standardisierung von `Temporal` die Browser dazu verpflichtet, immer den primären Bezeichner in der IANA-Datenbank zurückzugeben, der sich im Laufe der Zeit ändern kann. Für weitere Informationen siehe [Zeitzonen und Offsets](/de/docs/Web/JavaScript/Reference/Global_Objects/Temporal/ZonedDateTime#time_zones_and_offsets). Zum Beispiel sollte das zurückgegebene Array "Asia/Kolkata" anstelle von "Asia/Calcutta" enthalten, da letzteres ein Alias des ersteren ist und beide Indien entsprechen; jedoch sollte es sowohl "Africa/Abidjan" als auch "Atlantic/Reykjavik" enthalten, da sie sich in verschiedenen Ländern befinden, obwohl letzteres auch ein Alias des ersteren ist.

Referenzen:

- [IANA-Zeitzonendatenbank](https://www.iana.org/time-zones)
- [UTS 35, Zeitzonenkennungen](https://unicode.org/reports/tr35/tr35-dates.html#Time_Zone_Identifiers)

#### Unterstützte Einheitenkennungen

Nachfolgend sind alle Werte aufgeführt, die in Browsern allgemein für den Schlüssel `unit` unterstützt werden. Diese Werte können für die `unit`-Option verwendet werden, wenn Objekte wie {{jsxref("Intl.NumberFormat")}} erstellt werden. Diese Liste ist ein Teil des CLDR, das explizit von der ECMA-402 Spezifikation genehmigt wurde, sodass alle Implementierungen konsistent sein sollten.

- `acre`
- `bit`
- `byte`
- `celsius`
- `centimeter`
- `day`
- `degree`
- `fahrenheit`
- `fluid-ounce`
- `foot`
- `gallon`
- `gigabit`
- `gigabyte`
- `gram`
- `hectare`
- `hour`
- `inch`
- `kilobit`
- `kilobyte`
- `kilogram`
- `kilometer`
- `liter`
- `megabit`
- `megabyte`
- `meter`
- `microsecond`
- `mile`
- `mile-scandinavian`
- `milliliter`
- `millimeter`
- `millisecond`
- `minute`
- `month`
- `nanosecond`
- `ounce`
- `percent`
- `petabyte`
- `pound`
- `second`
- `stone`
- `terabit`
- `terabyte`
- `week`
- `yard`
- `year`

Beim Spezifizieren von Einheiten können Sie auch zwei Einheiten mit dem "-per-" Separator kombinieren. Zum Beispiel `meter-per-second` oder `liter-per-megabyte`.

Referenzen:

- [ECMA-402 genehmigte Einzelgeräte](https://tc39.es/ecma402/#table-sanctioned-single-unit-identifiers)
- [CLDR Einheitlichkeitsdaten](https://github.com/unicode-org/cldr/blob/main/common/validity/unit.xml)
- [UTS 35, Einheitenkennungen](https://unicode.org/reports/tr35/tr35-general.html#Unit_Identifiers)

### Ausnahmen

- {{jsxref("RangeError")}}
  - : Wird ausgelöst, wenn ein nicht unterstützter Schlüssel als Parameter übergeben wurde.

## Beispiele

### Feature-Testen

Sie können überprüfen, ob die Methode unterstützt wird, indem Sie auf `undefined` vergleichen:

```js
if (typeof Intl.supportedValuesOf !== "undefined") {
  // method is supported
}
```

### Holen Sie sich alle Werte für Schlüssel

Um die unterstützten Werte für Kalender zu erhalten, rufen Sie die Methode mit dem Schlüssel `"calendar"` auf.
Sie können dann das zurückgegebene Array wie unten gezeigt durchlaufen:

```js
Intl.supportedValuesOf("calendar").forEach((calendar) => {
  // "buddhist", "chinese", "coptic", "dangi", etc.
});
```

Die anderen Werte werden auf die gleiche Weise erhalten:

```js
Intl.supportedValuesOf("collation").forEach((collation) => {
  // "compat", "dict", "emoji", etc.
});

Intl.supportedValuesOf("currency").forEach((currency) => {
  // "ADP", "AED", "AFA", "AFN", "ALK", "ALL", "AMD", etc.
});

Intl.supportedValuesOf("numberingSystem").forEach((numberingSystem) => {
  // "adlm", "ahom", "arab", "arabext", "bali", etc.
});

Intl.supportedValuesOf("timeZone").forEach((timeZone) => {
  // "Africa/Abidjan", "Africa/Accra", "Africa/Addis_Ababa", "Africa/Algiers", etc.
});

Intl.supportedValuesOf("unit").forEach((unit) => {
  // "acre", "bit", "byte", "celsius", "centimeter", etc.
});
```

### Ungültiger Schlüssel wirft RangeError

```js
try {
  Intl.supportedValuesOf("someInvalidKey");
} catch (err) {
  //Error: RangeError: invalid key: "someInvalidKey"
}
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Polyfill von `Intl.supportedValuesOf` in FormatJS](https://formatjs.github.io/docs/polyfills/intl-supportedvaluesof/)
- {{jsxref("Intl")}}
