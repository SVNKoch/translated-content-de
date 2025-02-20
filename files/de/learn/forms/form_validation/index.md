---
title: Client-seitige Formularvalidierung
slug: Learn/Forms/Form_validation
l10n:
  sourceCommit: 5f76b99045f87349ed030bbd6a3c2e43badb3c22
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Forms/UI_pseudo-classes", "Learn/Forms/Sending_and_retrieving_form_data", "Learn/HTML/Forms")}}

Es ist wichtig sicherzustellen, dass alle erforderlichen Formularelemente vor dem Senden der vom Benutzer eingegebenen Formulardaten an den Server ausgefüllt und im richtigen Format sind. Diese **Client-seitige Formularvalidierung** hilft sicherzustellen, dass die eingegebenen Daten den Anforderungen entsprechen, die in den verschiedenen Formularelementen festgelegt sind.

Dieser Artikel führt Sie durch grundlegende Konzepte und Beispiele der client-seitigen Formularvalidierung.

<table>
  <tbody>
    <tr>
      <th scope="row">Voraussetzungen:</th>
      <td>
        Computer-Kenntnisse, ein angemessenes Verständnis von
        <a href="/de/docs/Learn/HTML">HTML</a>,
        <a href="/de/docs/Learn/CSS">CSS</a> und
        <a href="/de/docs/Learn/JavaScript">JavaScript</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Ziel:</th>
      <td>
        Verstehen, was client-seitige Formularvalidierung ist, warum sie wichtig ist,
        und wie man verschiedene Techniken zur Implementierung anwendet.
      </td>
    </tr>
  </tbody>
</table>

Die Client-seitige Validierung ist eine erste Überprüfung und ein wichtiges Merkmal für eine gute Benutzererfahrung; durch das Abfangen ungültiger Daten auf der Client-Seite kann der Benutzer diese sofort korrigieren.
Wenn sie zum Server gelangen und dann abgelehnt werden, entsteht eine merkliche Verzögerung durch eine Hin- und Rückreise zum Server und zurück zum Client, um den Benutzer zu informieren, dass er seine Daten korrigieren muss.

Client-seitige Validierung _sollte jedoch nicht_ als umfassende Sicherheitsmaßnahme betrachtet werden! Ihre Anwendungen sollten immer auch auf der _Server-Seite_ Validierung (einschließlich Sicherheitsprüfungen) der über Formulare eingereichten Daten durchführen, da die Client-seitige Validierung zu einfach zu umgehen ist, sodass böswillige Benutzer weiterhin problemlos schlechte Daten an Ihren Server senden können.

> [!NOTE]
> Lesen Sie [Website-Sicherheit](/de/docs/Learn/Server-side/First_steps/Website_security), um eine Vorstellung davon zu bekommen, was passieren _könnte_; die Implementierung der Server-seitigen Validierung ist etwas über den Umfang dieses Moduls hinaus, aber Sie sollten es im Hinterkopf behalten.

## Was ist Formularvalidierung?

Besuchen Sie eine bekannte Seite mit einem Registrierungsformular, und Sie werden feststellen, dass sie Feedback geben, wenn Sie Ihre Daten nicht im erwarteten Format eingeben.
Sie erhalten Nachrichten wie:

- "Dieses Feld ist erforderlich" (Dieses Feld darf nicht leer bleiben).
- "Bitte geben Sie Ihre Telefonnummer im Format xxx-xxxx ein" (Ein bestimmtes Datenformat ist erforderlich, um als gültig zu gelten).
- "Bitte geben Sie eine gültige E-Mail-Adresse ein" (Die von Ihnen eingegebenen Daten haben nicht das richtige Format).
- "Ihr Passwort muss zwischen 8 und 30 Zeichen lang sein und einen Großbuchstaben, ein Symbol und eine Zahl enthalten." (Ein sehr spezifisches Datenformat wird für Ihre Daten benötigt).

Dies nennt man **Formularvalidierung**.
Wenn Sie Daten eingeben, überprüft der Browser (und der Webserver), ob die Daten im richtigen Format sind und den vom Antrag festgelegten Einschränkungen entsprechen. Validierung, die im Browser durchgeführt wird, wird **client-seitige** Validierung genannt, während die auf dem Server durchgeführte Validierung **server-seitige** Validierung genannt wird.
In diesem Kapitel konzentrieren wir uns auf die client-seitige Validierung.

Wenn die Informationen korrekt formatiert sind, erlaubt die Anwendung, dass die Daten an den Server gesendet und (normalerweise) in einer Datenbank gespeichert werden; sind die Informationen nicht korrekt formatiert, gibt sie dem Benutzer eine Fehlermeldung, in der erklärt wird, was korrigiert werden muss, und lässt ihn es noch einmal versuchen.

Wir möchten das Ausfüllen von Webformularen so einfach wie möglich gestalten. Warum bestehen wir also darauf, unsere Formulare zu validieren?
Es gibt drei Hauptgründe:

- **Wir möchten die richtigen Daten im richtigen Format erhalten.** Unsere Anwendungen funktionieren nicht ordnungsgemäß, wenn die Benutzerdaten im falschen Format gespeichert sind, falsch sind oder ganz weggelassen werden.
- **Wir möchten die Daten unserer Benutzer schützen.** Indem wir unsere Benutzer zwingen, sichere Passwörter einzugeben, wird es einfacher, ihre Kontoinformationen zu schützen.
- **Wir möchten uns selbst schützen.** Es gibt viele Möglichkeiten, wie böswillige Benutzer nicht geschützte Formulare missbrauchen können, um der Anwendung zu schaden. Siehe [Website-Sicherheit](/de/docs/Learn/Server-side/First_steps/Website_security).

  > [!WARNING]
  > Vertrauen Sie niemals Daten, die von Ihrem Client an den Server gesendet werden. Selbst wenn Ihr Formular korrekt validiert und fehlerhafte Eingaben auf der Client-Seite verhindert, kann ein böswilliger Benutzer die Netzwerk-Anfrage dennoch verändern.

## Verschiedene Arten der Client-seitigen Validierung

Es gibt zwei verschiedene Arten der Client-seitigen Validierung, die Sie im Web antreffen werden:

- **HTML-Formularvalidierung**
  HTML-Formularattribute können definieren, welche Formularelemente erforderlich sind und in welchem Format die vom Benutzer eingegebenen Daten sein müssen, um gültig zu sein.
- **JavaScript-Formularvalidierung**
  JavaScript wird normalerweise hinzugefügt, um die HTML-Formularvalidierung zu verbessern oder anzupassen.

Die Client-seitige Validierung kann mit wenig bis gar keinem JavaScript erreicht werden. HTML-Validierung ist schneller als JavaScript, aber weniger anpassbar als JavaScript-Validierung. Es wird generell empfohlen, Ihre Formulare mit robusten HTML-Funktionen zu beginnen und dann bei Bedarf die Benutzererfahrung mit JavaScript zu verbessern.

## Verwendung der integrierten Formularvalidierung

Eine der wichtigsten Funktionen von [Formularsteuerelementen](/de/docs/Learn/Forms/HTML5_input_types) ist die Möglichkeit, die meisten Benutzerdaten zu validieren, ohne sich auf JavaScript zu verlassen.
Dies wird durch die Verwendung von Validierungsattributen für Formularelemente erreicht.
Viele davon haben wir bereits früher im Kurs gesehen, aber um es zusammenzufassen:

- [`required`](/de/docs/Web/HTML/Attributes/required): Gibt an, ob ein Formularfeld ausgefüllt werden muss, bevor das Formular gesendet werden kann.
- [`minlength`](/de/docs/Web/HTML/Attributes/minlength) und [`maxlength`](/de/docs/Web/HTML/Attributes/maxlength): Gibt die minimale und maximale Länge von Textdaten (Strings) an.
- [`min`](/de/docs/Web/HTML/Attributes/min), [`max`](/de/docs/Web/HTML/Attributes/max) und [`step`](/de/docs/Web/HTML/Attributes/step): Gibt die minimalen und maximalen Werte von numerischen Eingabetypen an und das Inkrement oder den Schritt für Werte, beginnend mit dem Minimum.
- [`type`](/de/docs/Web/HTML/Element/input#input_types): Gibt an, ob die Daten eine Zahl, eine E-Mail-Adresse oder ein anderer spezifischer Voreingabetyp sein müssen.
- [`pattern`](/de/docs/Web/HTML/Attributes/pattern): Gibt ein [Regulärer Ausdruck](/de/docs/Web/JavaScript/Guide/Regular_expressions) an, der ein Muster definiert, dem die eingegebenen Daten folgen müssen.

Wenn die in ein Formularfeld eingegebenen Daten alle von den auf das Feld angewendeten Attributen festgelegten Regeln befolgen, werden sie als gültig angesehen. Ansonsten gelten sie als ungültig.

Wenn ein Element gültig ist, sind folgende Dinge wahr:

- Das Element entspricht der {{cssxref(":valid")}} CSS-Pseudoklasse, mit der Sie einen spezifischen Stil auf gültige Elemente anwenden können. Das Steuerelement entspricht auch {{cssxref(":user-valid")}}, wenn der Benutzer mit dem Steuerelement interagiert hat, und kann je nach Eingabetyp und Attributen anderen UI-Pseudoklassen entsprechen, wie z.B. {{cssxref(":in-range")}}.
- Wenn der Benutzer versucht, die Daten zu senden, wird der Browser das Formular einreichen, vorausgesetzt, es gibt nichts anderes, das dies verhindert (z. B. JavaScript).

Wenn ein Element ungültig ist, sind folgende Dinge wahr:

- Das Element entspricht der {{cssxref(":invalid")}} CSS-Pseudoklasse. Wenn der Benutzer mit dem Steuerelement interagiert hat, entspricht es auch der {{cssxref(":user-invalid")}} CSS-Pseudoklasse. Je nach Fehler können auch andere UI-Pseudoklassen übereinstimmen, wie z. B. {{cssxref(":out-of-range")}}. Diese ermöglichen es Ihnen, einen spezifischen Stil auf ungültige Elemente anzuwenden.
- Wenn der Benutzer versucht, die Daten zu senden, wird der Browser die Formulareinreichung blockieren und eine Fehlermeldung anzeigen. Die Fehlermeldung variiert je nach Fehlerart. Die [Constraint Validation API](#die_constraint_validation_api) wird unten beschrieben.

## Eingebaute Beispiele zur Formularvalidierung

In diesem Abschnitt werden wir einige der oben besprochenen Attribute testen.

### Einfaches Startfile

Beginnen wir mit einem einfachen Beispiel: einer Eingabe, die es Ihnen ermöglicht, zu wählen, ob Sie eine Banane oder eine Kirsche bevorzugen.
Dieses Beispiel beinhaltet einen einfachen Text-{{HTMLElement("input")}} mit einem zugehörigen {{htmlelement("label")}} und einem Absende-{{htmlelement("button")}}.

```html
<form>
  <label for="choose">Would you prefer a banana or cherry?</label>
  <input id="choose" name="i-like" />
  <button>Submit</button>
</form>
```

```css
input:invalid {
  border: 2px dashed red;
}

input:valid {
  border: 2px solid black;
}
```

{{EmbedLiveSample("Simple_start_file", "100%", 80)}}

Zu Beginn erstellen Sie eine Kopie der [`fruit-start.html` Datei auf GitHub](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/fruit-start.html) in einem neuen Verzeichnis auf Ihrer Festplatte.

### Das `required` Attribut

Ein häufiges HTML-Validierungsmerkmal ist das [`required`](/de/docs/Web/HTML/Attributes/required) Attribut.
Fügen Sie dieses Attribut einer Eingabe hinzu, um ein Element obligatorisch zu machen.
Wenn dieses Attribut gesetzt ist, entspricht das Element der {{cssxref(':required')}} UI-Pseudoklasse und das Formular wird nicht gesendet, sondern zeigt bei der Eingabe eine Fehlermeldung an, wenn die Eingabe leer ist.
Wenn leer, wird die Eingabe auch als ungültig angesehen und entspricht der {{cssxref(':invalid')}} UI-Pseudoklasse.

Wenn ein Radio-Button in einer gleichnamigen Gruppe das `required` Attribut hat, muss einer der Radio-Buttons in dieser Gruppe aktiviert sein, damit die Gruppe gültig ist; der aktivierte Radio-Button muss nicht unbedingt derjenige mit dem gesetzten Attribut sein.

> [!NOTE]
> Verlangen Sie nur die Eingabe von Daten, die Sie benötigen: Zum Beispiel, ist es wirklich notwendig, das Geschlecht oder den Titel einer Person zu kennen?

Fügen Sie Ihrem Eingabefeld ein `required` Attribut hinzu, wie unten gezeigt.

```html
<form>
  <label for="choose">Would you prefer a banana or cherry? (required)</label>
  <input id="choose" name="i-like" required />
  <button>Submit</button>
</form>
```

Wir haben "(erforderlich)" zum {{htmlelement("label")}} hinzugefügt, um den Benutzer darüber zu informieren, dass das {{htmlelement("input")}} erforderlich ist. Dem Benutzer anzuzeigen, wenn Formularfelder erforderlich sind, ist nicht nur eine gute Benutzererfahrung, sondern auch durch die WCAG- [Zugänglichkeit](/de/docs/Learn/Accessibility) Richtlinien erforderlich.

Wir fügen CSS-Stile hinzu, die je nach dem erforderlich, gültig und ungültig sein des Elements angewendet werden:

```css
input:invalid {
  border: 2px dashed red;
}

input:invalid:required {
  background-image: linear-gradient(to right, pink, lightgreen);
}

input:valid {
  border: 2px solid black;
}
```

Dieses CSS sorgt dafür, dass die Eingabe ein rotes gestricheltes Rand hat, wenn sie ungültig ist, und ein subtileres festes schwarzes Rand, wenn sie gültig ist.
Wir haben auch einen Hintergrundgradienten hinzugefügt, wenn die Eingabe erforderlich _und_ ungültig ist. Probieren Sie das neue Verhalten im folgenden Beispiel aus:

{{EmbedLiveSample("The_required_attribute", "100%", 80)}}

Versuchen Sie, das Formular aus dem [live `required` Beispiel](https://mdn.github.io/learning-area/html/forms/form-validation/fruit-required.html) ohne Wert zu senden. Beachten Sie, wie die ungültige Eingabe den Fokus erhält, eine standardisierte Fehlermeldung ("Bitte füllen Sie dieses Feld aus") erscheint und das Formular verhindert wird, gesendet zu werden. Sie können auch den [Quellcode auf GitHub](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/fruit-required.html) ansehen.

### Validierung mit einem regulären Ausdruck

Ein weiteres nützliches Validierungsmerkmal ist das [`pattern`](/de/docs/Web/HTML/Attributes/pattern) Attribut, das einen [Regulärer Ausdruck](/de/docs/Web/JavaScript/Guide/Regular_expressions) als Wert erwartet.
Ein regulärer Ausdruck (regexp) ist ein Muster, das verwendet werden kann, um Zeichenkombinationen in Textstrings zu vergleichen, sodass regexps ideal für die Formularvalidierung und eine Vielzahl anderer Anwendungen in JavaScript sind.

Regexps sind ziemlich komplex, und wir beabsichtigen nicht, Ihnen sie in diesem Artikel umfassend beizubringen.
Hier sind einige Beispiele, um Ihnen eine grundlegende Vorstellung davon zu geben, wie sie funktionieren.

- `a` — Passt auf ein Zeichen, das `a` ist (nicht `b`, nicht `aa`, usw.).
- `abc` — Passt auf `a`, gefolgt von `b`, gefolgt von `c`.
- `ab?c` — Passt auf `a`, optional gefolgt von einem einzigen `b`, gefolgt von `c`. (`ac` oder `abc`)
- `ab*c` — Passt auf `a`, optional gefolgt von einer beliebigen Anzahl von `b`s, gefolgt von `c`. (`ac`, `abc`, `abbbbbc`, usw.).
- `a|b` — Passt auf ein Zeichen, das `a` oder `b` ist.
- `abc|xyz` — Passt genau `abc` oder genau `xyz` (aber nicht `abcxyz` oder `a` oder `y`, usw.).

Es gibt viele weitere Möglichkeiten, die wir hier nicht abdecken.
Für eine vollständige Liste und viele Beispiele konsultieren Sie unsere [Regulärer Ausdruck](/de/docs/Web/JavaScript/Guide/Regular_expressions) Dokumentation.

Lassen Sie uns ein Beispiel implementieren.
Aktualisieren Sie Ihr HTML, um ein [`pattern`](/de/docs/Web/HTML/Attributes/pattern) Attribut wie folgt hinzuzufügen:

```html
<form>
  <label for="choose">Would you prefer a banana or a cherry?</label>
  <input id="choose" name="i-like" required pattern="[Bb]anana|[Cc]herry" />
  <button>Submit</button>
</form>
```

```css hidden
input:invalid {
  border: 2px dashed red;
}

input:valid {
  border: 2px solid black;
}
```

Dies gibt uns das folgende Update - probieren Sie es aus:

{{EmbedLiveSample("Validating_against_a_regular_expression", "100%", 80)}}

Sie können dieses [Beispiel live auf GitHub](https://mdn.github.io/learning-area/html/forms/form-validation/fruit-pattern.html) zusammen mit dem [Quellcode](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/fruit-pattern.html) finden.

In diesem Beispiel akzeptiert das {{HTMLElement("input")}} Element einen von vier möglichen Werten: die Zeichenfolgen "banana", "Banana", "cherry" oder "Cherry". Reguläre Ausdrücke sind großschreibungssensitiv, aber wir haben es so gemacht, dass es groß- wie auch kleingeschriebene Versionen unterstützt, indem wir ein zusätzliches "Aa" Muster in eckigen Klammern nesteten.

Versuchen Sie an dieser Stelle, den Wert im [`pattern`](/de/docs/Web/HTML/Attributes/pattern) Attribut zu ändern, um einigen der vorher gesehenen Beispiele zu entsprechen, und sehen Sie, wie sich dies auf die Werte auswirkt, die Sie eingeben können, um den Eingabewert gültig zu machen.
Versuchen Sie, einige Ihrer eigenen zu schreiben und sehen Sie, wie es geht.
Machen Sie sie wenn möglich fruchtbezogen, damit Ihre Beispiele sinnvoll erscheinen!

Wenn ein nicht-leerer Wert des {{HTMLElement("input")}} nicht dem Muster des regulären Ausdrucks entspricht, entspricht `input` der {{cssxref(':invalid')}} Pseudoklasse. Wenn leer und das Element nicht erforderlich ist, wird es nicht als ungültig angesehen.

Einige {{HTMLElement("input")}} Elementtypen benötigen kein [`pattern`](/de/docs/Web/HTML/Attributes/pattern) Attribut, um gegen einen regulären Ausdruck validiert zu werden. Beispielsweise validiert das Angeben des `email` Typs den Eingabewert gegen ein gut geformtes E-Mail-Adressmuster oder ein Muster, das eine kommagetrennte Liste von E-Mail-Adressen entspricht, wenn es das [`multiple`](/de/docs/Web/HTML/Attributes/multiple) Attribut hat.

> [!NOTE]
> Das {{HTMLElement("textarea")}} Element unterstützt das [`pattern`](/de/docs/Web/HTML/Attributes/pattern) Attribut nicht.

### Einschränkung der Länge Ihrer Eingaben

Sie können die Zeichenlänge aller von {{HTMLElement("input")}} oder {{HTMLElement("textarea")}} erstellten Texteingabefelder mit den Attributen [`minlength`](/de/docs/Web/HTML/Attributes/minlength) und [`maxlength`](/de/docs/Web/HTML/Attributes/maxlength) begrenzen.
Ein Feld ist ungültig, wenn es einen Wert hat und dieser Wert weniger Zeichen als den [`minlength`](/de/docs/Web/HTML/Attributes/minlength) oder mehr als den [`maxlength`](/de/docs/Web/HTML/Attributes/maxlength) hat.

Browser lassen den Benutzer oft keine längeren Werte als erwartet in Textfeldern eingeben. Eine bessere Benutzererfahrung als nur `maxlength` zu verwenden, besteht darin, auch eine Zeichenanzahl-Rückmeldung auf zugängliche Weise bereitzustellen und den Benutzer seine Inhalte auf die richtige Länge ändern zu lassen.
Ein Beispiel dafür ist das Zeichenlimit beim Posten in sozialen Medien. JavaScript, einschließlich [Lösungen unter Verwendung von `maxlength`](https://github.com/mimo84/bootstrap-maxlength), kann verwendet werden, um dies bereitzustellen.

> [!NOTE]
> Längeneinschränkungen werden nie gemeldet, wenn der Wert programmgesteuert gesetzt wird. Sie werden nur für Benutzereingaben gemeldet.

### Einschränkung der Werte Ihrer Eingaben

Für numerische Felder, einschließlich [`<input type="number">`](/de/docs/Web/HTML/Element/input/number) und der verschiedenen Datumseingabetypen, können die Attribute [`min`](/de/docs/Web/HTML/Attributes/min) und [`max`](/de/docs/Web/HTML/Attributes/max) verwendet werden, um einen Bereich gültiger Werte bereitzustellen.
Wenn das Feld einen Wert außerhalb dieses Bereichs enthält, wird es als ungültig angesehen.

Sehen wir uns ein weiteres Beispiel an.
Erstellen Sie eine neue Kopie der [fruit-start.html](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/fruit-start.html) Datei.

Löschen Sie nun den Inhalt des `<body>` Elements und ersetzen Sie ihn durch folgendes:

```html
<form>
  <div>
    <label for="choose">Would you prefer a banana or a cherry?</label>
    <input
      type="text"
      id="choose"
      name="i-like"
      required
      minlength="6"
      maxlength="6" />
  </div>
  <div>
    <label for="number">How many would you like?</label>
    <input type="number" id="number" name="amount" value="1" min="1" max="10" />
  </div>
  <div>
    <button>Submit</button>
  </div>
</form>
```

- Hier werden Sie sehen, dass wir dem `text` Feld ein `minlength` und `maxlength` von sechs gegeben haben, was der Länge von Banane und Kirsche entspricht.
- Wir haben dem `number` Feld auch ein `min` von eins und ein `max` von zehn gegeben.
  Eingegebene Zahlen außerhalb dieses Bereichs werden als ungültig angezeigt; Benutzer können die Erhöhung-/Verringern-Pfeile nicht verwenden, um den Wert außerhalb dieses Bereichs zu verschieben.
  Wenn der Benutzer manuell eine Zahl außerhalb dieses Bereichs eingibt, sind die Daten ungültig.
  Die Zahl ist nicht erforderlich, sodass das Entfernen des Wertes zu einem gültigen Wert führt.

```css hidden
input:invalid {
  border: 2px dashed red;
}

input:valid {
  border: 2px solid black;
}

div {
  margin-bottom: 10px;
}
```

Hier ist das Beispiel als Live-Demo:

{{EmbedLiveSample("Constraining_the_values_of_your_entries", "100%", 100)}}

Probieren Sie dieses [Beispiel live auf GitHub](https://mdn.github.io/learning-area/html/forms/form-validation/fruit-length.html) aus und sehen Sie sich den [Quellcode](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/fruit-length.html) an.

Numerische Eingabetypen wie `number`, `range` und `date` können ebenfalls das [`step`](/de/docs/Web/HTML/Attributes/step) Attribut aufnehmen. Dieses Attribut gibt an, um welches Inkrement der Wert bei Verwendung der Eingabesteuerungen verschoben wird (z.B. die Aufwärts- und Abwärtspfeile, oder das Verschieben des Schiebereglers). Das `step` Attribut wird in unserem Beispiel weggelassen, sodass der Wert standardmäßig `1` ist. Das bedeutet, dass Gleitkommazahlen wie 3.2 auch als ungültig angezeigt werden.

### Vollständiges Beispiel

Hier ist ein vollständiges Beispiel, um die Verwendung der in HTML eingebauten Validierungsmerkmale zu demonstrieren.
Zuerst etwas HTML:

```html
<form>
  <fieldset>
    <legend>
      Do you have a driver's license?<span aria-label="required">*</span>
    </legend>
    <input type="radio" required name="driver" id="r1" value="yes" /><label
      for="r1"
      >Yes</label
    >
    <input type="radio" required name="driver" id="r2" value="no" /><label
      for="r2"
      >No</label
    >
  </fieldset>
  <p>
    <label for="n1">How old are you?</label>
    <input type="number" min="12" max="120" step="1" id="n1" name="age" />
  </p>
  <p>
    <label for="t1"
      >What's your favorite fruit?<span aria-label="required">*</span></label
    >
    <input
      type="text"
      id="t1"
      name="fruit"
      list="l1"
      required
      pattern="[Bb]anana|[Cc]herry|[Aa]pple|[Ss]trawberry|[Ll]emon|[Oo]range" />
    <datalist id="l1">
      <option>Banana</option>
      <option>Cherry</option>
      <option>Apple</option>
      <option>Strawberry</option>
      <option>Lemon</option>
      <option>Orange</option>
    </datalist>
  </p>
  <p>
    <label for="t2">What's your email address?</label>
    <input type="email" id="t2" name="email" />
  </p>
  <p>
    <label for="t3">Leave a short message</label>
    <textarea id="t3" name="msg" maxlength="140" rows="5"></textarea>
  </p>
  <p>
    <button>Submit</button>
  </p>
</form>
```

Und jetzt etwas CSS, um das HTML zu stylen:

```css
form {
  font: 1em sans-serif;
  max-width: 320px;
}

p > label {
  display: block;
}

input[type="text"],
input[type="email"],
input[type="number"],
textarea,
fieldset {
  width: 100%;
  border: 1px solid #333;
  box-sizing: border-box;
}

input:invalid {
  box-shadow: 0 0 5px 1px red;
}

input:focus:invalid {
  box-shadow: none;
}
```

Dies wird wie folgt gerendert:

{{EmbedLiveSample("Full_example", "100%", 420)}}

Dieses [vollständige Beispiel ist live auf GitHub](https://mdn.github.io/learning-area/html/forms/form-validation/full-example.html) zusammen mit dem [Quellcode](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/full-example.html).

Sehen Sie [Validierungsbezogene Attribute](/de/docs/Web/HTML/Constraint_validation#validation-related_attributes) für eine vollständige Liste der Attribute, die verwendet werden können, um Eingabewerte zu beschränken und die Eingabetypen, die sie unterstützen.

## Validieren von Formularen mit JavaScript

Wenn Sie den Text der nativen Fehlermeldungen ändern möchten, ist JavaScript erforderlich.
In diesem Abschnitt werden wir uns die verschiedenen Möglichkeiten ansehen, dies zu tun.

### Die Constraint Validation API

Die Constraint Validation API besteht aus einer Reihe von Methoden und Eigenschaften, die auf den folgenden Formularelement-DOM-Interfaces verfügbar sind:

- [`HTMLButtonElement`](/de/docs/Web/API/HTMLButtonElement) (repräsentiert ein [`<button>`](/de/docs/Web/HTML/Element/button) Element)
- [`HTMLFieldSetElement`](/de/docs/Web/API/HTMLFieldSetElement) (repräsentiert ein [`<fieldset>`](/de/docs/Web/HTML/Element/fieldset) Element)
- [`HTMLInputElement`](/de/docs/Web/API/HTMLInputElement) (repräsentiert ein [`<input>`](/de/docs/Web/HTML/Element/input) Element)
- [`HTMLOutputElement`](/de/docs/Web/API/HTMLOutputElement) (repräsentiert ein [`<output>`](/de/docs/Web/HTML/Element/output) Element)
- [`HTMLSelectElement`](/de/docs/Web/API/HTMLSelectElement) (repräsentiert ein [`<select>`](/de/docs/Web/HTML/Element/select) Element)
- [`HTMLTextAreaElement`](/de/docs/Web/API/HTMLTextAreaElement) (repräsentiert ein [`<textarea>`](/de/docs/Web/HTML/Element/textarea) Element)

Die Constraint Validation API stellt die folgenden Eigenschaften auf den oben genannten Elementen zur Verfügung.

- `validationMessage`: Gibt eine lokalisierte Nachricht zurück, die die Validierungseinschränkungen beschreibt, die das Steuerelement nicht erfüllt (falls vorhanden). Wenn das Steuerelement kein Kandidat für die Einschränkungsvalidierung ist (`willValidate` ist `false`) oder der Wert des Elements seine Einschränkungen erfüllt (ist gültig), wird dies einen leeren String zurückgeben.
- `validity`: Gibt ein `ValidityState` Objekt zurück, das mehrere Eigenschaften beschreibt, die den Gültigkeitsstatus des Elements beschreiben. Sie können vollständige Details zu allen verfügbaren Eigenschaften auf der [`ValidityState`](/de/docs/Web/API/ValidityState) Referenzseite finden; unten sind einige der gebräuchlicheren aufgeführt:

  - [`patternMismatch`](/de/docs/Web/API/ValidityState/patternMismatch): Gibt `true` zurück, wenn der Wert nicht mit dem angegebenen [`pattern`](/de/docs/Web/HTML/Element/input#pattern) übereinstimmt, und `false`, wenn er übereinstimmt. Wenn `true`, entspricht das Element der {{cssxref(":invalid")}} CSS-Pseudoklasse.
  - [`tooLong`](/de/docs/Web/API/ValidityState/tooLong): Gibt `true` zurück, wenn der Wert länger ist als die maximale Länge, die durch das [`maxlength`](/de/docs/Web/HTML/Element/input#maxlength) Attribut angegeben ist, oder `false`, wenn er kürzer oder gleich der maximalen Länge ist. Wenn `true`, entspricht das Element der {{cssxref(":invalid")}} CSS-Pseudoklasse.
  - [`tooShort`](/de/docs/Web/API/ValidityState/tooShort): Gibt `true` zurück, wenn der Wert kürzer ist als die minimale Länge, die durch das [`minlength`](/de/docs/Web/HTML/Element/input#minlength) Attribut angegeben ist, oder `false`, wenn er größer oder gleich der minimalen Länge ist. Wenn `true`, entspricht das Element der {{cssxref(":invalid")}} CSS-Pseudoklasse.
  - [`rangeOverflow`](/de/docs/Web/API/ValidityState/rangeOverflow): Gibt `true` zurück, wenn der Wert größer ist als das maximale, das durch das [`max`](/de/docs/Web/HTML/Element/input#max) Attribut angegeben wird, oder `false`, wenn er kleiner oder gleich dem Maximum ist. Wenn `true`, entspricht das Element den {{cssxref(":invalid")}} und {{cssxref(":out-of-range")}} CSS-Pseudoklassen.
  - [`rangeUnderflow`](/de/docs/Web/API/ValidityState/rangeUnderflow): Gibt `true` zurück, wenn der Wert kleiner ist als das minimale, das durch das [`min`](/de/docs/Web/HTML/Element/input#min) Attribut angegeben wird, oder `false`, wenn er größer oder gleich dem Minimum ist. Wenn `true`, entspricht das Element den {{cssxref(":invalid")}} und {{cssxref(":out-of-range")}} CSS-Pseudoklassen.
  - [`typeMismatch`](/de/docs/Web/API/ValidityState/typeMismatch): Gibt `true` zurück, wenn der Wert nicht in der erforderlichen Syntax ist (wenn [`type`](/de/docs/Web/HTML/Element/input#type) `email` oder `url` ist), oder `false`, wenn die Syntax korrekt ist. Wenn `true`, entspricht das Element der {{cssxref(":invalid")}} CSS-Pseudoklasse.
  - `valid`: Gibt `true` zurück, wenn das Element alle seine Validierungseinschränkungen erfüllt und daher als gültig angesehen wird, oder `false`, wenn es eine Einschränkung nicht erfüllt. Wenn `true`, entspricht das Element der {{cssxref(":valid")}} CSS-Pseudoklasse; andernfalls der {{cssxref(":invalid")}} CSS-Pseudoklasse.
  - `valueMissing`: Gibt `true` zurück, wenn das Element ein [`required`](/de/docs/Web/HTML/Element/input#required) Attribut hat, aber keinen Wert, oder `false` andernfalls. Wenn `true`, entspricht das Element der {{cssxref(":invalid")}} CSS-Pseudoklasse.

- `willValidate`: Gibt `true` zurück, wenn das Element validiert wird, wenn das Formular gesendet wird; andernfalls `false`.

Die Constraint Validation API stellt die folgenden Methoden auf den oben genannten Elementen und dem [`form`](/de/docs/Web/HTML/Element/form) Element zur Verfügung.

- `checkValidity()`: Gibt `true` zurück, wenn der Wert des Elements keine Gültigkeitsprobleme aufweist; andernfalls `false`. Wenn das Element ungültig ist, löst diese Methode auch ein [`invalid ` Ereignis](/de/docs/Web/API/HTMLInputElement/invalid_event) auf dem Element aus.
- `reportValidity()`: Meldet ungültige Felder mithilfe von Ereignissen. Diese Methode ist in Kombination mit `preventDefault()` in einem `onSubmit`-Ereignishandler nützlich.
- `setCustomValidity(message)`: Fügt dem Element eine benutzerdefinierte Fehlermeldung hinzu; wenn Sie eine benutzerdefinierte Fehlermeldung festlegen, wird das Element als ungültig angesehen und die angegebene Fehlermeldung angezeigt. Dies ermöglicht es Ihnen, JavaScript-Code zu verwenden, um einen Validierungsfehler zu etablieren, der über die standardmäßigen HTML-Validierungseinschränkungen hinausgeht. Die Nachricht wird dem Benutzer angezeigt, wenn das Problem gemeldet wird.

#### Implementieren einer angepassten Fehlermeldung

Wie Sie in den HTML-Validierungseinschränkungsbeispielen zuvor gesehen haben, zeigt der Browser jedes Mal, wenn ein Benutzer versucht, ein ungültiges Formular einzureichen, eine Fehlermeldung an. Die Art und Weise, wie diese Nachricht angezeigt wird, hängt vom Browser ab.

Diese automatisierten Nachrichten haben zwei Nachteile:

- Es gibt keinen Standardweg, ihr Aussehen und Gefühl mit CSS zu ändern.
- Sie hängen vom Browsersprache ab, was bedeutet, dass Sie eine Seite in einer Sprache haben können, aber eine Fehlermeldung in einer anderen Sprache angezeigt wird, wie im folgenden Firefox-Screenshot.

![Beispiel einer Fehlermeldung mit Firefox in Französisch auf einer englischen Seite](error-firefox-win7.png)

Die Anpassung dieser Fehlermeldungen ist einer der häufigsten Anwendungsfälle der Constraint Validation API.
Lassen Sie uns ein Beispiel dafür durchgehen, wie dies gemacht wird.

Wir beginnen mit etwas HTML (fühlen Sie sich frei, dies in eine leere HTML-Datei zu legen; verwenden Sie eine frische Kopie von [fruit-start.html](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/fruit-start.html) als Basis, wenn Sie mögen):

```html
<form>
  <label for="mail">
    I would like you to provide me with an email address:
  </label>
  <input type="email" id="mail" name="mail" />
  <button>Submit</button>
</form>
```

Fügen Sie die folgende JavaScript-Code der Seite hinzu:

```js
const email = document.getElementById("mail");

email.addEventListener("input", (event) => {
  if (email.validity.typeMismatch) {
    email.setCustomValidity("I am expecting an email address!");
  } else {
    email.setCustomValidity("");
  }
});
```

Hier speichern wir einen Verweis auf die E-Mail-Eingabe, dann fügen wir einen Ereignishörer hinzu, der den enthaltenen Code jedes Mal ausführt, wenn sich der Wert innerhalb der Eingabe ändert.

Im enthaltenen Code überprüfen wir, ob die `validity.typeMismatch` Eigenschaft der E-Mail-Eingabe `true` zurückgibt, was bedeutet, dass der enthaltene Wert nicht dem Muster einer gut geformten E-Mail-Adresse entspricht. Wenn ja, rufen wir die [`setCustomValidity()`](/de/docs/Web/API/HTMLInputElement/setCustomValidity) Methode mit einer benutzerdefinierten Nachricht auf. Dies macht die Eingabe ungültig, sodass, wenn Sie versuchen, das Formular zu senden, das Senden fehlschlägt und die benutzerdefinierte Fehlermeldung angezeigt wird.

Wenn die `validity.typeMismatch` Eigenschaft `false` zurückgibt, rufen wir die `setCustomValidity()` Methode mit einem leeren String auf. Dies macht die Eingabe gültig, sodass das Formular gesendet wird. Während der Validierung, wenn ein Formularelement einen `customError` hat, der nicht der leere String ist, wird das Formularsenden blockiert.

Sie können es unten ausprobieren:

{{EmbedGHLiveSample("learning-area/html/forms/form-validation/custom-error-message.html", '100%', 120)}}

Sie können dieses Beispiel live auf GitHub als [custom-error-message.html](https://mdn.github.io/learning-area/html/forms/form-validation/custom-error-message.html) zusammen mit dem [Quellcode](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/custom-error-message.html) finden.

#### Erweiterung der eingebauten Formularvalidierung

Das vorherige Beispiel zeigte, wie Sie eine angepasste Nachricht für einen bestimmten Fehlertyp (`validity.typeMismatch`) hinzufügen können.
Es ist auch möglich, die gesamte eingebaute Formularvalidierung zu verwenden und dann mit `setCustomValidity()` zu erweitern.

Hier demonstrieren wir, wie Sie die eingebaute [`<input type="email">`](/de/docs/Web/HTML/Element/input/email) Validierung erweitern können, um nur Adressen mit der Domain `@example.com` zu akzeptieren.
Wir beginnen mit dem HTML {{htmlelement("form")}} unten.

```html
<form>
  <label for="mail">Email address (@example.com only):</label>
  <input type="email" id="mail" />
  <button>Submit</button>
</form>
```

Der Validierungscode wird unten gezeigt.
Im Falle einer neuen Eingabe setzt der Code zuerst die benutzerdefinierte Gültigkeitsmeldung zurück, indem er `setCustomValidity("")` aufruft.
Dann verwendet er `email.validity.valid`, um zu überprüfen, ob die eingegebene Adresse ungültig ist und wenn ja, kehrt er aus dem Ereignis-Handler zurück.
Dies stellt sicher, dass alle normalen eingebauten Validierungsüberprüfungen durchgeführt werden, solange die eingegebene Text kein gültige E-Mail-Adresse ist.

Sobald die E-Mail-Adresse gültig ist, fügt der Code eine benutzerdefinierte Einschränkung hinzu, indem er `setCustomValidity()` mit einer Fehlermeldung aufruft, wenn die Adresse nicht mit `@example.com` endet.

```js
const email = document.getElementById("mail");

email.addEventListener("input", (event) => {
  // Validate with the built-in constraints
  email.setCustomValidity("");
  if (!email.validity.valid) {
    return;
  }

  // Extend with a custom constraints
  if (!email.value.endsWith("@example.com")) {
    email.setCustomValidity("Please enter an email address of @example.com");
  }
});
```

Sie können dieses Beispiel auf der Seite im {{LiveSampleLink('Extending_built-in_form_validation', 'Live-Demo-Linksquelle')}} ausprobieren.
Versuchen Sie eine ungültige E-Mail-Adresse einzugeben, eine gültige E-Mail-Adresse, die nicht mit `@example.com` endet, und eine, die mit `@example.com` endet.

#### Ein detaillierteres Beispiel

Jetzt, da wir ein sehr einfaches Beispiel gesehen haben, lassen Sie uns sehen, wie wir diese API verwenden können, um etwas umfangreichere benutzerdefinierte Validierung zu erstellen.

Zuerst das HTML. Wiederum, fühlen Sie sich frei, dies mit uns zu bauen:

```html
<form novalidate>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="email" id="mail" name="mail" required minlength="8" />
      <span class="error" aria-live="polite"></span>
    </label>
  </p>
  <button>Submit</button>
</form>
```

Dieses Formular verwendet das [`novalidate`](/de/docs/Web/HTML/Element/form#novalidate) Attribut, um die automatische Validierung durch den Browser zu deaktivieren. Das Setzen des `novalidate` Attributs auf dem Formular verhindert, dass das Formular seine eigenen Fehlermeldungsblasen anzeigt, und ermöglicht uns stattdessen die benutzerdefinierten Fehlermeldungen im DOM auf eine von uns gewählte Weise anzuzeigen.
Jedoch deaktiviert dies nicht die Unterstützung der Einschränkungsvalidierungs-API noch die Anwendung von CSS-Pseudoklassen wie {{cssxref(":valid")}}, usw.
Das bedeutet, dass selbst wenn der Browser die Gültigkeit des Formulars nicht automatisch überprüft, bevor er seine Daten sendet, Sie es dennoch selbst tun und das Formular entsprechend stylen können.

Unsere zu validierende Eingabe ist ein [`<input type="email">`](/de/docs/Web/HTML/Element/input/email), das `required` ist und eine `minlength` von 8 Zeichen hat. Lassen Sie uns diese mit unserem eigenen Code überprüfen und eine benutzerdefinierte Fehlermeldung für jede anzeigen.

Wir beabsichtigen, die Fehlermeldungen in einem `<span>` Element anzuzeigen.
Das [`aria-live`](/de/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) Attribut ist auf diesem `<span>` gesetzt, um sicherzustellen, dass unsere benutzerdefinierte Fehlermeldung jedem präsentiert wird, einschließlich der Tatsache, dass sie auch von Bildschirmleseanwendern ausgegeben wird.

Nun zu etwas grundlegendem CSS, um das Aussehen des Formulars leicht zu verbessern und visuelles Feedback zu geben, wenn die Eingabedaten ungültig sind:

```css
body {
  font: 1em sans-serif;
  width: 200px;
  padding: 0;
  margin: 0 auto;
}

p * {
  display: block;
}

input[type="email"] {
  appearance: none;

  width: 100%;
  border: 1px solid #333;
  margin: 0;

  font-family: inherit;
  font-size: 90%;

  box-sizing: border-box;
}

/* invalid fields */
input:invalid {
  border-color: #900;
  background-color: #fdd;
}

input:focus:invalid {
  outline: none;
}

/* error message styles */
.error {
  width: 100%;
  padding: 0;

  font-size: 80%;
  color: white;
  background-color: #900;
  border-radius: 0 0 5px 5px;

  box-sizing: border-box;
}

.error.active {
  padding: 0.3em;
}
```

Schauen wir uns nun das JavaScript an, das die benutzerdefinierte Fehlerüberprüfung implementiert.
Es gibt viele Möglichkeiten, einen DOM-Knoten auszuwählen; hier verwenden wir das Formular selbst und das E-Mail
Eingabefeld sowie das Span-Element, in das wir die Fehlermeldung platzieren werden.

Mit Ereignishandlern überprüfen wir, ob die Eingabefelder gültig sind, jedes Mal, wenn der Benutzer etwas eingibt. Wenn ein Fehler vorliegt, zeigen wir ihn an. Wenn kein Fehler vorliegt, entfernen wir jede Fehleranzeige.

```js
const form = document.querySelector("form");
const email = document.getElementById("mail");
const emailError = document.querySelector("#mail + span.error");

email.addEventListener("input", (event) => {
  if (email.validity.valid) {
    emailError.textContent = ""; // Remove the message content
    emailError.className = "error"; // Removes the `active` class
  } else {
    // If there is still an error, show the correct error
    showError();
  }
});

form.addEventListener("submit", (event) => {
  // if the email field is invalid
  if (!email.validity.valid) {
    // display an appropriate error message
    showError();
    // prevent form submission
    event.preventDefault();
  }
});

function showError() {
  if (email.validity.valueMissing) {
    // If empty
    emailError.textContent = "You need to enter an email address.";
  } else if (email.validity.typeMismatch) {
    // If it's not an email address,
    emailError.textContent = "Entered value needs to be an email address.";
  } else if (email.validity.tooShort) {
    // If the value is too short,
    emailError.textContent = `Email should be at least ${email.minLength} characters; you entered ${email.value.length}.`;
  }
  // Add the `active` class
  emailError.className = "error active";
}
```

Jedes Mal, wenn wir den Wert der Eingabe ändern, prüfen wir, ob sie gültige Daten enthält. Wenn sie hat, entfernen wir jede angezeigte Fehlermeldung. Sind die Daten nicht gültig, führen wir `showError()` aus, um die entsprechende Fehlermeldung anzuzeigen.

Jedes Mal, wenn wir versuchen, das Formular abzusenden, überprüfen wir erneut, ob die Daten gültig sind. Wenn ja, lassen wir das Formular absenden. Wenn nicht, führen wir `showError()` aus, um die entsprechende Fehlermeldung anzuzeigen und verhindern das Absenden des Formulars mit [`preventDefault()`](/de/docs/Web/API/Event/preventDefault).

Die `showError()` Funktion verwendet verschiedene Eigenschaften des `validity` Objekts der Eingabe, um festzustellen, was der Fehler ist, und zeigt dann eine entsprechende Fehlermeldung an.

Hier ist das Live-Ergebnis:

{{EmbedGHLiveSample("learning-area/html/forms/form-validation/detailed-custom-validation.html", '100%', 150)}}

Sie können dieses Beispiel live auf GitHub als [detailed-custom-validation.html](https://mdn.github.io/learning-area/html/forms/form-validation/detailed-custom-validation.html) zusammen mit dem [Quellcode](https://github.com/mdn/learning-area/blob/main/html/forms/form-validation/detailed-custom-validation.html) finden.

Die Einschränkungsvalidierungs-API bietet Ihnen ein leistungsstarkes Werkzeug zur Handhabung der Formularvalidierung und gibt Ihnen enorme Kontrolle über die Benutzeroberfläche, die über das hinausgeht, was Sie nur mit HTML und CSS machen können.

### Validierung von Formularen ohne eine integrierte API

In einigen Fällen, wie bei [benutzerdefinierten Steuerelementen](/de/docs/Learn/Forms/How_to_build_custom_form_controls), können Sie die Einschränkungsvalidierungs-API nicht verwenden oder wollen es nicht. Hier können Sie mit JavaScript Ihr Formular validieren, müssen jedoch Ihr eigenes schreiben.

Um ein Formular zu validieren, stellen Sie sich ein paar Fragen:

- Welche Art von Validierung sollte ich durchführen?
  - : Sie müssen bestimmen, wie Sie Ihre Daten validieren: Zeichenfolgenoperationen, Typumwandlung, reguläre Ausdrücke und so weiter. Es liegt an Ihnen.
- Was sollte ich tun, wenn das Formular nicht validiert?
  - : Dies ist eindeutig eine Benutzeroberflächenfrage. Sie müssen entscheiden, wie das Formular sich verhält. Sendet das Formular die Daten trotzdem?
    Sollten Sie die Felder hervorheben, die fehlerhaft sind?
    Sollten Sie Fehlermeldungen anzeigen?
- Wie kann ich dem Benutzer helfen, ungültige Daten zu korrigieren?

  - : Um die Frustration des Benutzers zu reduzieren, ist es sehr wichtig, so viele hilfreiche Informationen wie möglich bereitzustellen, um ihnen zu helfen, ihre Eingaben zu korrigieren.
    Sie sollten schon im Voraus Ratschläge geben, damit sie wissen, was erwartet wird, ebenso wie klare Fehlermeldungen.
    Wenn Sie in die Anforderungen an die Formularvalidierungs-Benutzeroberfläche eintauchen möchten, sind hier einige nützliche Artikel, die Sie lesen sollten:

    - [Helfen Sie Benutzer, die richtigen Daten in Formularen einzugeben](https://web.dev/learn/forms/validation/)
    - [Eingaben validieren](https://www.w3.org/WAI/tutorials/forms/validation/)
    - [Wie man Fehler in Formularen meldet: 10 Designrichtlinien](https://www.nngroup.com/articles/errors-forms-design-guidelines/)

#### Ein Beispiel, das die Einschränkungsvalidierungs-API nicht verwendet

Um dies zu veranschaulichen, folgt hier eine vereinfachte Version des vorherigen Beispiels ohne die Einschränkungsvalidierungs-API.

Das HTML ist fast dasselbe; wir haben nur die HTML-Validierungsfeatures entfernt.

```html
<form>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="text" id="mail" name="mail" />
      <span class="error" aria-live="polite"></span>
    </label>
  </p>
  <button>Submit</button>
</form>
```

Ähnlich muss das CSS nicht viel geändert werden; wir haben nur die {{cssxref(":invalid")}} CSS-Pseudoklasse in eine echte Klasse umgewandelt und vermeiden die Verwendung des Attributselektors.

```css
body {
  font: 1em sans-serif;
  width: 200px;
  padding: 0;
  margin: 0 auto;
}

form {
  max-width: 200px;
}

p * {
  display: block;
}

input#mail {
  appearance: none;
  width: 100%;
  border: 1px solid #333;
  margin: 0;

  font-family: inherit;
  font-size: 90%;

  box-sizing: border-box;
}

/* invalid fields */
input#mail.invalid {
  border-color: #900;
  background-color: #fdd;
}

input:focus.invalid {
  outline: none;
}

/* error messages */
.error {
  width: 100%;
  padding: 0;

  font-size: 80%;
  color: white;
  background-color: #900;
  border-radius: 0 0 5px 5px;
  box-sizing: border-box;
}

.error.active {
  padding: 0.3em;
}
```

Die großen Änderungen sind im JavaScript-Code, der viel mehr tun muss.

```js
const form = document.querySelector("form");
const email = document.getElementById("mail");
const error = email.nextElementSibling;

// As per the HTML Specification
const emailRegExp =
  /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

// Now we can rebuild our validation constraint
// Because we do not rely on CSS pseudo-class, we have to
// explicitly set the valid/invalid class on our email field
window.addEventListener("load", () => {
  // Here, we test if the field is empty (remember, the field is not required)
  // If it is not, we check if its content is a well-formed email address.
  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  email.className = isValid ? "valid" : "invalid";
});

// This defines what happens when the user types in the field
email.addEventListener("input", () => {
  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  if (isValid) {
    email.className = "valid";
    error.textContent = "";
    error.className = "error";
  } else {
    email.className = "invalid";
  }
});

// This defines what happens when the user tries to submit the data
form.addEventListener("submit", (event) => {
  event.preventDefault();

  const isValid = email.value.length === 0 || emailRegExp.test(email.value);
  if (!isValid) {
    email.className = "invalid";
    error.textContent = "I expect an email, darling!";
    error.className = "error active";
  } else {
    email.className = "valid";
    error.textContent = "";
    error.className = "error";
  }
});
```

Das Ergebnis sieht so aus:

{{EmbedLiveSample("An_example_that_doesnt_use_the_constraint_validation_API", "100%", 130)}}

Wie Sie sehen können, ist es nicht allzu schwer, ein Validierungssystem selbst zu erstellen. Der schwierige Teil besteht darin, es so allgemein zu gestalten, dass es sowohl plattformübergreifend als auch auf jedes von Ihnen erstellte Formular anwendbar ist. Es gibt viele Bibliotheken, die Formularvalidierung durchführen, wie [Validate.js](https://rickharrison.github.io/validate.js/).

## Testen Sie Ihre Fähigkeiten!

Sie haben das Ende dieses Artikels erreicht, aber können Sie sich die wichtigsten Informationen merken? Sie können einige weitere Tests finden, um zu überprüfen, ob Sie diese Informationen behalten haben, bevor Sie weitermachen - siehe [Testen Sie Ihre Fähigkeiten: Formularvalidierung](/de/docs/Learn/Forms/Test_your_skills:_Form_validation).

## Zusammenfassung

Client-seitige Formularvalidierung erfordert manchmal JavaScript, wenn Sie Styling und Fehlermeldungen anpassen möchten, aber es erfordert _immer_, dass Sie sorgfältig über den Benutzer nachdenken.
Denken Sie immer daran, Ihren Benutzern zu helfen, die bereitgestellten Daten zu korrigieren. Zu diesem Zweck sollten Sie sicherstellen, dass:

- Eindeutige Fehlermeldungen angezeigt werden.
- Sie großzügig mit dem Eingabeformat umgehen.
- Sie genau darauf hinweisen, wo der Fehler auftritt, besonders bei umfangreichen Formularen.

Sobald Sie überprüft haben, dass das Formular korrekt ausgefüllt ist, kann das Formular gesendet werden.
Wir werden uns als Nächstes mit dem [Senden von Formulardaten](/de/docs/Learn/Forms/Sending_and_retrieving_form_data) befassen.

{{PreviousMenuNext("Learn/Forms/UI_pseudo-classes", "Learn/Forms/Sending_and_retrieving_form_data", "Learn/HTML/Forms")}}

### Fortgeschrittene Themen

- [Wie man benutzerdefinierte Formularsteuerelemente erstellt](/de/docs/Learn/Forms/How_to_build_custom_form_controls)
- [Formulare über JavaScript senden](/de/docs/Learn/Forms/Sending_forms_through_JavaScript)
- [Eigenschaftskompatibilitätstabelle für Formular-Widgets](/de/docs/Learn/Forms/Property_compatibility_table_for_form_controls)
