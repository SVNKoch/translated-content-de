---
title: Die MDN Content Kitchensink
slug: MDN/Kitchensink
l10n:
  sourceCommit: 41a27d6c0f8e44f1b9a3dabddd9315655b367b77
---

> [!WARNING]
> Löschen Sie diese Seite nicht. Sie wird von [mdn/yari](https://github.com/mdn/yari) für deren Automatisierung verwendet.

## Über diese Seite

Der **kitchensink** ist eine Seite, die _versucht_, jedes mögliche Inhaltselement und Yari-Makro zu integrieren.

Diese Seite versucht, der komplette Schnittpunkt jeder anderen Seite zu sein. Nicht in Bezug auf den Text, sondern in Bezug auf die Stile und Makros.
Lassen Sie uns mit einigen Anmerkungen beginnen...

Text, der das `<kbd>`-Tag verwendet: <kbd>Umschalt</kbd>

> [!NOTE]
> Hier ist eine Blockanzeige-Notiz.

> [!WARNING]
> Hier ist eine Blockanzeige-Warnung.

## Vorherige/Nächste-Schaltflächen

{{PreviousMenuNext("Games/Techniques/Control_mechanisms/Desktop_with_mouse_and_keyboard", "Games/Techniques/Control_mechanisms/Other", "Games/Techniques/Control_mechanisms")}}

### Ein weiteres Beispiel…

{{PreviousNext("Games/Workflows/2D_Breakout_game_Phaser/Extra_lives", "Games/Workflows/2D_Breakout_game_Phaser/Buttons")}}

## Code-Beispiele

### Klartext

```plain
  ___________________________
< I'm an expert in my field. >
  ---------------------------
         \   ^__^
          \  (oo)\_______
             (__)\       )\/\
                 ||----w |
                 ||     ||
```

### HTML

```html
<pre></pre>
```

### JavaScript

```js
const f = () => {
  return Math.random();
};
```

### CSS

```css
:root {
  --first-color: #488cff;
  --second-color: #ffff8c;
}

#firstParagraph {
  background-color: var(--first-color);
  color: var(--second-color);
}
```

### WebAssembly

```wasm
(func (param i32) (param f32) (local f64)
  local.get 0
  local.get 1
  local.get 2)
```

### Rust

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }
}
```

### Python

```python
class BookListView(generic.ListView):
    model = Book
    # your own name for the list as a template variable
    context_object_name = 'my_book_list'
    queryset = Book.objects.filter(title__icontains='war')[:5]
    template_name = 'books/my_arbitrary_template_name_list.html'
```

## Interaktive Beispiele

{{EmbedInteractiveExample("pages/tabbed/abbr.html", "tabbed-shorter")}} {{EmbedInteractiveExample("pages/css/order.html")}} {{EmbedInteractiveExample("pages/js/regexp-assertions.html", "taller")}}

## Tabellen

### Markdown-Tabelle

| Konstanter Name              | Wert   | Beschreibung                                                                                       |
| ---------------------------- | ------ | -------------------------------------------------------------------------------------------------- |
| `QUERY_COUNTER_BITS_EXT`     | 0x8864 | Die Anzahl der Bits, die verwendet werden, um das Abfrageergebnis für das gegebene Ziel zu halten. |
| `CURRENT_QUERY_EXT`          | 0x8865 | Die derzeit aktive Abfrage.                                                                        |
| `QUERY_RESULT_EXT`           | 0x8866 | Das Abfrageergebnis.                                                                               |
| `QUERY_RESULT_AVAILABLE_EXT` | 0x8867 | Ein Boolean, der anzeigt, ob ein Abfrageergebnis verfügbar ist.                                    |
| `TIME_ELAPSED_EXT`           | 0x88BF | Verstrichene Zeit (in Nanosekunden).                                                               |
| `TIMESTAMP_EXT`              | 0x8E28 | Die aktuelle Zeit.                                                                                 |
| `GPU_DISJOINT_EXT`           | 0x8FBB | Ein Boolean, der anzeigt, ob die GPU eine unzusammenhängende Operation ausgeführt hat.             |

### HTML-Tabelle

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">
        <a href="/de/docs/Web/HTML/Content_categories">Inhaltskategorien</a>
      </th>
      <td>
        <a href="/de/docs/Web/HTML/Content_categories#flow_content">Flussinhalt</a>,
        <a href="/de/docs/Web/HTML/Content_categories#phrasing_content">Phrasierungsinhalt</a>, fühlbarer Inhalt.
      </td>
    </tr>
    <tr>
      <th scope="row">Erlaubter Inhalt</th>
      <td>
        <a href="/de/docs/Web/HTML/Content_categories#phrasing_content">Phrasierungsinhalt</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Tag-Auslassung</th>
      <td>Keine, sowohl das Start- als auch das End-Tag sind obligatorisch.</td>
    </tr>
    <tr>
      <th scope="row">Erlaubte Eltern</th>
      <td>
        Jedes Element, das <a href="/de/docs/Web/HTML/Content_categories#phrasing_content">Phrasierungsinhalt</a> akzeptiert.
      </td>
    </tr>
    <tr>
      <th scope="row">Implizierte ARIA-Rolle</th>
      <td>
        <a href="https://www.w3.org/TR/html-aria/#dfn-no-corresponding-role">Keine entsprechende Rolle</a>
      </td>
    </tr>
    <tr>
      <th scope="row">Erlaubte ARIA-Rollen</th>
      <td>Beliebige</td>
    </tr>
    <tr>
      <th scope="row">DOM-Schnittstelle</th>
      <td>[`HTMLElement`](/de/docs/Web/API/HTMLElement)</td>
    </tr>
  </tbody>
</table>

<table class="fullwidth-table">
  <caption>
    Werte für den Inhalt von <code>&#x3C;meta name="viewport"></code>
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
        Definiert die Pixelbreite des Viewports, bei der Sie möchten, dass die Webseite gerendert wird.
      </td>
    </tr>
    <tr>
      <td><code>user-scalable</code> {{ReadOnlyInline}}</td>
      <td><code>yes</code> oder <code>no</code></td>
      <td>
        Wenn auf <code>no</code> gesetzt, kann der Benutzer nicht in die Webseite hineinzoomen.
        Der Standardwert ist <code>yes</code>. Browsereinstellungen können diese Regel ignorieren und iOS10+ ignoriert sie standardmäßig.
      </td>
    </tr>
    <tr>
      <td><code>viewport-fit</code></td>
      <td><code>auto</code>, <code>contain</code> oder <code>cover</code></td>
      <td>
        <p>
          Der Wert <code>auto</code> beeinflusst das anfängliche Layout-Viewport nicht, und die gesamte Webseite ist sichtbar.
        </p>
        <p>
          Der Wert <code>contain</code> bedeutet, dass der Viewport so skaliert wird, dass er das größte Rechteck im Display vergrößert.
        </p>
        <p>
          Der Wert <code>cover</code> bedeutet, dass der Viewport so skaliert wird, dass er das Gerätedisplay ausfüllt.
          Es wird dringend empfohlen, die <a href="/de/docs/Web/CSS/env">sicheren Bereichsvariablen</a> zu verwenden, um sicherzustellen, dass wichtiger Inhalt nicht außerhalb des Displays landet.
        </p>
      </td>
    </tr>
  </tbody>
</table>

## Jedes Makro unter der Sonne

**Nun ja, fast jedes Makro. Hoffentlich nur die, die aktiv verwendet werden.**

Ein {{Glossary("HTTP", "HTTP")}}-Fehlercode, der "Bad Gateway" bedeutet.

Ein {{Glossary("Server", "Server")}} kann als Gateway oder Proxy (Zwischenschritt) zwischen einem Client (wie Ihrem Webbrowser) und einem anderen, übergeordneten Server fungieren.
Wenn Sie anfordern, auf eine {{Glossary("URL", "URL")}} zuzugreifen, kann der Gateway-Server Ihre Anfrage an den übergeordneten Server weiterleiten.
"502" bedeutet, dass der übergeordnete Server eine ungültige Antwort zurückgegeben hat.

- JavaScript {{jsxref("Array")}} auf MDN

Das Lauschen auf Mausbewegungen ist sogar noch einfacher als das Lauschen auf Tastendrücke: alles, was wir brauchen, ist das Event für das [`mousemove`](/de/docs/Web/API/Element/mousemove_event)-Ereignis.

## Browser-Kompatibilität

{{Compat}}

## Achsen-ausgerichtete Begrenzungsbox

Eine der einfacheren Formen der Kollisionserkennung ist die zwischen zwei Rechtecken, die achsen-ausgerichtet sind — das bedeutet keine Drehung.
Der Algorithmus funktioniert, indem sichergestellt wird, dass es keine Lücke zwischen den 4 Seiten der Rechtecke gibt.
Jede Lücke bedeutet, dass keine Kollision besteht.

```js
var rect1 = { x: 5, y: 5, width: 50, height: 50 };
var rect2 = { x: 20, y: 10, width: 10, height: 10 };

if (
  rect1.x < rect2.x + rect2.width &&
  rect1.x + rect1.width > rect2.x &&
  rect1.y < rect2.y + rect2.height &&
  rect1.y + rect1.height > rect2.y
) {
  // collision detected!
}

// filling in the values =>

if (5 < 30 && 55 > 20 && 5 < 20 && 55 > 10) {
  // collision detected!
}
```

### Rechteckcode

```html
<div id="cr-stage"></div>
<p>
  Move the rectangle with arrow keys. Green means collision, blue means no
  collision.
</p>
<script
  type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/crafty/0.5.4/crafty-min.js"></script>
```

```js
Crafty.init(200, 200);

var dim1 = {x: 5, y: 5, w: 50, h: 50}
var dim2 = {x: 20, y: 10, w: 60, h: 40}

var rect1 = Crafty.e("2D, Canvas, Color").attr(dim1).color("red");

var rect2 = Crafty.e("2D, Canvas, Color, Keyboard, Fourway").fourway(2).attr(dim2).color("blue");

rect2.bind("EnterFrame", function () {
if (rect1.x > rect2.x + rect2.w &#x26;&#x26;
rect1.x + rect1.w > rect2.x &#x26;&#x26;
rect1.y > rect2.y + rect2.h &#x26;&#x26;
rect1.h + rect1.y > rect2.y) {
// collision detected!
this.color("green");
} else {
// no collision
this.color("blue");
}
});
```

{{EmbedLiveSample('Rect_code', '700', '300') }}

{{SeeCompatTable}}

{{WebExtAPIRef("tabs.mutedInfo")}}

### Veraltete CSSOM-Schnittstellen {{deprecated_inline}}

{{InheritanceDiagram("WheelEvent")}}

{{EmbedGHLiveSample("web-tech-games/index.html", '100%', 820)}}

- [Zugängliche Ressourcen bei MDN](/de/docs/Web/Accessibility)
- [Webbarrierefreiheit](https://en.wikipedia.org/wiki/Web_accessibility) auf Wikipedia

Das [`AvailableInWorkers`](https://github.com/mdn/yari/blob/main/kumascript/macros/AvailableInWorkers.ejs)-Makro fügt ein lokalisiertes Hinweisfeld ein, das anzeigt, dass eine Funktion im Kontext eines [Webarbeiters](/de/docs/Web/API/Web_Workers_API) verfügbar ist.

{{AvailableInWorkers}}

- [`button`](/de/docs/Web/Accessibility/ARIA/Roles/button_role)
- [`checkbox`](/de/docs/Web/Accessibility/ARIA/Roles/checkbox_role)
- [`menuitem`](/de/docs/Web/Accessibility/ARIA/Roles/menuitem_role)
- [`menuitemcheckbox`](/de/docs/Web/Accessibility/ARIA/Roles/menuitemcheckbox_role)
- [`menuitemradio`](/de/docs/Web/Accessibility/ARIA/Roles/menuitemradio_role)
- [`option`](/de/docs/Web/Accessibility/ARIA/Roles/option_role)
- [`radio`](/de/docs/Web/Accessibility/ARIA/Roles/radio_role)
- [`switch`](/de/docs/Web/Accessibility/ARIA/Roles/switch_role)
- [`tab`](/de/docs/Web/Accessibility/ARIA/Roles/tab_role)
- [`treeitem`](/de/docs/Web/Accessibility/ARIA/Roles/treeitem_role)

<!---->

- Erstellen Sie ein {{htmlelement("canvas")}}-Element und setzen Sie dessen `width`- und `height`-Attribute auf die ursprüngliche, kleinere Auflösung.
- Setzen Sie dessen CSS-{{cssxref("width")}}- und {{cssxref("height")}}-Eigenschaften auf das Zwei- oder Vierfache des Werts der HTML-`width`- und `height`.
  Wenn das Canvas mit einer Breite von 128 Pixeln erstellt wurde, würden wir die CSS-`width` auf `512px` setzen, wenn wir eine 4x-Skalierung wollten.
- Setzen Sie die `image-rendering`-CSS-Eigenschaft des {{htmlelement("canvas")}}-Elements auf einen Wert, der das Bild nicht unscharf macht.
  Entweder `crisp-edges` oder `pixelated` funktioniert. Lesen Sie den Artikel zu {{cssxref("image-rendering")}}, um weitere Informationen über die Unterschiede zwischen diesen Werten und die zu verwendenden Präfixe in Abhängigkeit vom Browser zu erhalten.

<!---->

- [MDN Web Docs Glossar](/de/docs/Glossary):

  - {{Glossary("XMLHttpRequest", "XHR")}}

- [AJAX](https://en.wikipedia.org/wiki/AJAX) auf Wikipedia
- [Ajax](/de/docs/Learn/JavaScript/Client-side_web_APIs/Fetching_data)
- [`XMLHttpRequest`](/de/docs/Web/API/XMLHttpRequest)
- [`Fetch API`](/de/docs/Web/API/Fetch_API)
- [Verwendung der Fetch API](/de/docs/Web/API/Fetch_API/Using_Fetch)
- [Synchron vs. Asynchron-Kommunikation](https://peoplesofttutorial.com/difference-between-synchronous-and-asynchronous-messaging/)

<!---->

- {{SVGElement("feGaussianBlur")}}
- {{SVGAttr("keySplines")}} SVG-Attribut
- [dir](/de/docs/Web/HTML/Global_attributes#dir)
- [lang](/de/docs/Web/HTML/Global_attributes#lang)
- {{cssxref(":dir")}}
- {{cssxref("direction")}}

## Typen

- {{WebExtAPIRef("alarms.Alarm")}}
  - : Informationen zu einem bestimmten Alarm.

{{Non-standard_Header}}
{{Deprecated_Header}}
[![Iceberg pic](iceberg.jpg)](iceberg.jpg)
