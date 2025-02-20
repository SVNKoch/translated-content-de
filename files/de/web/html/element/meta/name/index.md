---
title: Standard-Metadaten-Namen
slug: Web/HTML/Element/meta/name
l10n:
  sourceCommit: 24d8a34da576f86b10923e426f66df48ab6201b9
---

{{HTMLSidebar}}

Das {{htmlelement("meta")}}-Element kann verwendet werden, um Dokumentmetadaten in Form von Name-Wert-Paaren bereitzustellen, wobei das [`name`](/de/docs/Web/HTML/Element/meta#name)-Attribut den Metadaten-Namen und das [`content`](/de/docs/Web/HTML/Element/meta#content)-Attribut den Wert angibt.

### Standard-Metadaten-Namen, die in der HTML-Spezifikation definiert sind

Die HTML-Spezifikation definiert die folgende Reihe von Standard-Metadaten-Namen:

- `application-name`: der Name der Anwendung, die auf der Webseite ausgeführt wird.

  > [!NOTE]
  >
  > - Browser verwenden dies möglicherweise zur Identifizierung der Anwendung. Dies unterscheidet sich vom {{HTMLElement("title")}}-Element, das normalerweise den Anwendungsnamen enthält, aber auch Informationen wie den Dokumentnamen oder einen Status enthalten kann.
  > - Einfache Webseiten sollten keinen application-name definieren.

- `author`: der Name des Autors des Dokuments.
- `description`: eine kurze und genaue Zusammenfassung des Seiteninhalts. Suchmaschinen wie [Google](https://developers.google.com/search/docs/appearance/snippet#meta-descriptions) können dieses Feld verwenden, um das Erscheinungsbild der Webseite in den Suchergebnissen zu steuern.
- `generator`: die Kennung der Software, die die Seite generiert hat.
- `keywords`: Schlüsselwörter, die durch Kommata getrennt sind und für den Seiteninhalt relevant sind.
- `referrer`: steuert den HTTP {{httpheader("Referer")}}-Header von Anfragen, die vom Dokument gesendet werden:

  <table class="standard-table">
    <caption>
      Werte für das
      <code>content</code>
      Attribut von
      <code>&#x3C;meta name="referrer"></code>
    </caption>
    <tbody>
      <tr>
        <td><code>no-referrer</code></td>
        <td>Keinen HTTP {{httpheader("Referer")}}-Header senden.</td>
      </tr>
      <tr>
        <td><code>origin</code></td>
        <td>Den {{Glossary("origin", "Ursprung")}} des Dokuments senden.</td>
      </tr>
      <tr>
        <td><code>no-referrer-when-downgrade</code></td>
        <td>
          Die vollständige URL senden, wenn das Ziel mindestens so sicher ist wie
          die aktuelle Seite (HTTP(S)→HTTPS), aber keinen Referrer senden, wenn es weniger sicher ist
          (HTTPS→HTTP). Dies ist das Standardverhalten.
        </td>
      </tr>
      <tr>
        <td><code>origin-when-cross-origin</code></td>
        <td>
          Die vollständige URL (ohne Parameter) für gleichartige Anfragen senden, aber
          nur den Ursprung in anderen Fällen.
        </td>
      </tr>
      <tr>
        <td><code>same-origin</code></td>
        <td>
          Die vollständige URL (ohne Parameter) für gleichartige Anfragen senden.
          Anfragen über unterschiedliche Ursprünge enthalten keinen Referrer-Header.
        </td>
      </tr>
      <tr>
        <td><code>strict-origin</code></td>
        <td>
          Den Ursprung senden, wenn das Ziel mindestens so sicher ist wie
          die aktuelle Seite (HTTP(S)→HTTPS), aber keinen Referrer senden, wenn es weniger sicher ist
          (HTTPS→HTTP).
        </td>
      </tr>
      <tr>
        <td><code>strict-origin-when-cross-origin</code></td>
        <td>
          Die vollständige URL (ohne Parameter) für gleichartige Anfragen senden.
          Den Ursprung senden, wenn das Ziel mindestens so sicher ist wie
          die aktuelle Seite (HTTP(S)→HTTPS). Andernfalls keinen Referrer senden.
        </td>
      </tr>
      <tr>
        <td><code>unsafe-URL</code></td>
        <td>
          Die vollständige URL (ohne Parameter) für gleichartige oder
          Anfragen über unterschiedliche Ursprünge senden.
        </td>
      </tr>
    </tbody>
  </table>

  > [!NOTE]
  >
  > - Das dynamische Einfügen von `<meta name="referrer">` (mit [`document.write()`](/de/docs/Web/API/Document/write) oder [`appendChild()`](/de/docs/Web/API/Node/appendChild)) macht das Referrer-Verhalten unvorhersehbar.
  > - Wenn mehrere widersprüchliche Richtlinien definiert sind, wird die `no-referrer`-Richtlinie angewendet.

- [`theme-color`](/de/docs/Web/HTML/Element/meta/name/theme-color): gibt eine vorgeschlagene Farbe an, die Benutzeragenten verwenden sollten, um die Anzeige der Seite oder der umgebenden Benutzeroberfläche anzupassen. Das `content`-Attribut enthält einen gültigen CSS {{cssxref("&lt;color&gt;")}}. Das `media`-Attribut mit einer gültigen Medienabfrage-Liste kann eingeschlossen werden, um das Medium festzulegen, für das die Theme-Farbe gilt.
- <a id="color-scheme" href="#color-scheme">`color-scheme`</a>: gibt ein oder mehrere Farbschemata an, mit denen das Dokument kompatibel ist.

  Der Browser verwendet diese Informationen zusammen mit den Einstellungen des Benutzers im Browser oder auf seinem Gerät, um zu bestimmen, welche Farben für alles von Hintergrund- und Vordergrundtexten bis hin zu Formularelementen und Scrollleisten verwendet werden sollen. Der Hauptzweck von `<meta name="color-scheme">` besteht darin, die Kompatibilität mit und die Präferenzreihenfolge für helle und dunkle Farbmodi anzugeben.

  Der Wert der [`content`](/de/docs/Web/HTML/Element/meta#content)-Eigenschaft von `color-scheme` kann einer der folgenden sein:

  - `normal`
    - : Das Dokument ist sich der Farbschemata nicht bewusst und sollte mit der Standardfarbpalette gerendert werden.
  - `light`, `dark`, `light dark`, `dark light`
    - : Ein oder mehrere vom Dokument unterstützte Farbschemata. Die mehrfache Angabe desselben Farbschemas hat denselben Effekt wie die einmalige Angabe. Die Angabe mehrerer Farbschemata bedeutet, dass das erste Schema vom Dokument bevorzugt wird, das zweite jedoch akzeptabel ist, wenn der Benutzer es vorzieht.
  - `only light`
    - : Gibt an, dass das Dokument _nur_ den hellen Modus unterstützt, mit einem hellen Hintergrund und dunklen Vordergrundfarben. Laut Spezifikation ist `only dark` _nicht gültig_, da das Erzwingen des Renderns eines Dokuments im dunklen Modus, wenn es nicht wirklich kompatibel ist, zu unlesbaren Inhalten führen kann; alle großen Browser wechseln standardmäßig in den hellen Modus, wenn nicht anders konfiguriert.

  Zum Beispiel, um anzuzeigen, dass ein Dokument den dunklen Modus bevorzugt, aber auch im hellen Modus funktional ist:

  ```html
  <meta name="color-scheme" content="dark light" />
  ```

  Dies funktioniert auf Dokumentebene in derselben Weise, wie die CSS-Eigenschaft {{cssxref("color-scheme")}} es einzelnen Elementen ermöglicht, ihre bevorzugten und akzeptierten Farbschemata anzugeben. Ihre Stile können sich an das aktuelle Farbschema mithilfe des CSS-Medienmerkmals {{cssxref("@media/prefers-color-scheme", "prefers-color-scheme")}} anpassen.

### Standard-Metadaten-Namen, die in anderen Spezifikationen definiert sind

Die CSS Device Adaptation-Spezifikation definiert den folgenden Metadaten-Namen:

- `viewport`: gibt Hinweise auf die Größe des anfänglichen {{Glossary("viewport", "viewports")}}.

  <table class="fullwidth-table">
    <caption>
      Werte für den Inhalt von
      <code>&#x3C;meta name="viewport"></code>
    </caption>
    <thead>
      <tr>
        <th scope="col">Wert</th>
        <th scope="col">Mögliche Unterwerte</th>
        <th scope="col">Beschreibung</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>width</code></td>
        <td>Eine positive ganze Zahl oder der Text <code>device-width</code></td>
        <td>
          Definiert die Pixelbreite des Viewports, in der die Website
          gerendert werden soll.
        </td>
      </tr>
      <tr>
        <td><code>height</code></td>
        <td>Eine positive ganze Zahl oder der Text <code>device-height</code></td>
        <td>Definiert die Höhe des Viewports. Wird von keinem Browser verwendet.</td>
      </tr>
      <tr>
        <td><code>initial-scale</code></td>
        <td>Eine positive Zahl zwischen <code>0.0</code> und <code>10.0</code></td>
        <td>
          Definiert das Verhältnis zwischen der Gerätebreite (<code>device-width</code>
          im Hochformat oder <code>device-height</code> im Querformat) und der
          Viewport-Größe.
        </td>
      </tr>
      <tr>
        <td><code>maximum-scale</code></td>
        <td>Eine positive Zahl zwischen <code>0.0</code> und <code>10.0</code></td>
        <td>
          Definiert den maximalen Zoomfaktor. Er muss größer oder gleich dem
          <code>minimum-scale</code> sein, sonst ist das Verhalten nicht definiert.
          Browsereinstellungen können diese Regel ignorieren, und iOS10+ ignoriert sie standardmäßig.
        </td>
      </tr>
      <tr>
        <td><code>minimum-scale</code></td>
        <td>Eine positive Zahl zwischen <code>0.0</code> und <code>10.0</code></td>
        <td>
          Definiert die minimale Zoomstufe. Er muss kleiner oder gleich dem
          <code>maximum-scale</code> sein, sonst ist das Verhalten nicht definiert.
          Browsereinstellungen können diese Regel ignorieren, und iOS10+ ignoriert sie standardmäßig.
        </td>
      </tr>
      <tr>
        <td><code>user-scalable</code></td>
        <td><code>yes</code> oder <code>no</code></td>
        <td>
          Wenn auf <code>no</code> gesetzt, kann der Benutzer die Webseite
          nicht vergrößern. Der Standardwert ist <code>yes</code>. Browsereinstellungen
          können diese Regel ignorieren, und iOS10+ ignoriert sie standardmäßig.
        </td>
      </tr>
      <tr>
        <td><code>viewport-fit</code></td>
        <td><code>auto</code>, <code>contain</code> oder <code>cover</code></td>
        <td>
          <p>
            Der <code>auto</code>-Wert beeinflusst das anfängliche Layout
            des Viewports nicht, und die gesamte Webseite ist sichtbar.
          </p>
          <p>
            Der <code>contain</code>-Wert bedeutet, dass der Viewport so skaliert wird,
            dass das größte eingetragene Rechteck innerhalb des Displays passt.
          </p>
          <p>
            Der <code>cover</code>-Wert bedeutet, dass der Viewport so skaliert wird, dass er
            das Gerätedisplay ausfüllt. Es wird dringend empfohlen, die
            <a href="/de/docs/Web/CSS/env">sicheren Bereichs-Variablen</a> zu
            verwenden, um sicherzustellen, dass wichtige Inhalte nicht außerhalb des Displays landen.
          </p>
        </td>
      </tr>
    </tbody>
  </table>

  > [!WARNING]
  >
  > Das Deaktivieren von Zoom-Funktionen, indem `user-scalable` auf `no` gesetzt wird, verhindert, dass Personen mit Sehschwäche in der Lage sind, die Seiteninhalte zu lesen und zu verstehen.
  >
  > - [MDN Understanding WCAG, Guideline 1.4 explanations](/de/docs/Web/Accessibility/Understanding_WCAG/Perceivable#guideline_1.4_make_it_easier_for_users_to_see_and_hear_content_including_separating_foreground_from_background)
  > - [Understanding Success Criterion 1.4.4 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html)

### Weitere Metadaten-Namen

Die [WHATWG Wiki MetaExtensions-Seite](https://wiki.whatwg.org/wiki/MetaExtensions) enthält eine große Menge nicht standardisierter Metadaten-Namen, die noch nicht formal akzeptiert wurden; jedoch werden einige der dort enthaltenen Namen bereits häufig in der Praxis verwendet, darunter die folgenden:

- `creator`: der Name des Erstellers des Dokuments, wie z.B. eine Organisation oder Institution. Wenn es mehrere gibt, sollten mehrere {{HTMLElement("meta")}}-Elemente verwendet werden.
- `googlebot`, ein Synonym für `robots`, wird nur von Googlebot (dem Indexierungs-Crawler von Google) befolgt.
- `publisher`: der Name des Verlegers des Dokuments.
- `robots`: das Verhalten, das kooperative Crawler oder "Robots" mit der Seite verwenden sollen. Es ist eine kommaseparierte Liste der folgenden Werte:

  | Wert           | Beschreibung                                                                              | Verwendet von                                                                                                                                                                                                                                            |
  | -------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | `index`        | Erlaubt dem Robot das Indexieren der Seite (Standard).                                    | Alle                                                                                                                                                                                                                                                     |
  | `noindex`      | Fordert den Robot auf, die Seite nicht zu indexieren.                                     | Alle                                                                                                                                                                                                                                                     |
  | `follow`       | Erlaubt dem Roboter, den Links auf der Seite zu folgen (Standard).                        | Alle                                                                                                                                                                                                                                                     |
  | `nofollow`     | Fordert den Roboter auf, den Links auf der Seite nicht zu folgen.                         | Alle                                                                                                                                                                                                                                                     |
  | `all`          | Entspricht `index, follow`                                                                | [Google](https://developers.google.com/search/docs/crawling-indexing/special-tags?visit_id=637855965067987211-415685194&rd=1)                                                                                                                            |
  | `none`         | Entspricht `noindex, nofollow`                                                            | [Google](https://developers.google.com/search/docs/crawling-indexing/special-tags?visit_id=637855965074074862-574753619&rd=1)                                                                                                                            |
  | `noarchive`    | Fordert die Suchmaschine auf, den Seiteninhalt nicht im Cache zu speichern.               | [Google](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag), [Yahoo](https://help.yahoo.com/kb/search-for-desktop/SLN2213.html), [Bing](https://www.bing.com/webmasters/help/which-robots-metatags-does-bing-support-5198d240) |
  | `nosnippet`    | Verhindert die Anzeige jeglicher Beschreibung der Seite in Suchergebnissen.               | [Google](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag), [Bing](https://www.bing.com/webmasters/help/which-robots-metatags-does-bing-support-5198d240)                                                                     |
  | `noimageindex` | Fordert, dass diese Seite nicht als verweisende Seite für ein indiziertes Bild erscheint. | [Google](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag)                                                                                                                                                                    |
  | `nocache`      | Synonym für `noarchive`.                                                                  | [Bing](https://www.bing.com/webmasters/help/which-robots-metatags-does-bing-support-5198d240)                                                                                                                                                            |

  > [!NOTE]
  >
  > - Nur kooperative Robots befolgen diese Regeln. Erwarten Sie nicht, E-Mail-Erntemaschinen damit zu verhindern.
  > - Der Robot muss dennoch auf die Seite zugreifen, um diese Regeln zu lesen. Um den Bandbreitenverbrauch zu verhindern, überlegen Sie, ob die Verwendung einer _{{Glossary("robots.txt", "robots.txt")}}_-Datei geeigneter ist.
  > - Das `<meta name="robots">`-Element und die `robots.txt`-Datei dienen unterschiedlichen Zwecken: `robots.txt` steuert das Crawlen der Seiten und beeinflusst nicht das Indexieren oder andere vom `robots`-Meta gesteuerte Verhaltensweisen. Eine Seite, die nicht gecrawlt werden kann, kann dennoch indexiert werden, wenn sie von einem anderen Dokument referenziert wird.
  > - Wenn Sie eine Seite entfernen möchten, funktioniert `noindex`, aber nur, nachdem der Robot die Seite erneut besucht hat. Stellen Sie sicher, dass die `robots.txt`-Datei erneute Besuche nicht verhindert.
  > - Einige Werte schließen sich gegenseitig aus, wie `index` und `noindex`, oder `follow` und `nofollow`. In diesen Fällen ist das Verhalten des Robots undefiniert und kann zwischen ihnen variieren.
  > - Einige Crawler-Robots, wie Google, Yahoo und Bing, unterstützen dieselben Werte für den HTTP-Header {{HTTPHeader("X-Robots-Tag")}}; dies ermöglicht es nicht-HTML-Dokumenten wie Bildern, diese Regeln zu verwenden.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Viewport `<meta>`-Tag](/de/docs/Web/HTML/Viewport_meta_tag)
- [Metadaten: das `<meta>`-Element](/de/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML#metadata_the_meta_element) in [Was ist im Kopf? Metadaten in HTML](/de/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)
