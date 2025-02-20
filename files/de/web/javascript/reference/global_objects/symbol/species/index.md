---
title: Symbol.species
slug: Web/JavaScript/Reference/Global_Objects/Symbol/species
l10n:
  sourceCommit: d4ea77f1c9e15e472e484d9561319597c5cce716
---

{{JSRef}}

Die statische Dateneigenschaft **`Symbol.species`** repräsentiert das [bekannte Symbol](/de/docs/Web/JavaScript/Reference/Global_Objects/Symbol#well-known_symbols) `Symbol.species`. Methoden, die Kopien eines Objekts erstellen, können dieses Symbol im Objekt nachschlagen, um die zu verwendende Konstruktorfunktion beim Erstellen der Kopie zu erhalten.

> [!WARNING]
> Die Existenz von `[Symbol.species]` erlaubt die Ausführung von beliebigem Code und kann Sicherheitslücken erzeugen. Sie erschwert auch bestimmte Optimierungen erheblich. Entwickler von Engines [untersuchen derzeit, ob diese Funktion entfernt werden soll](https://github.com/tc39/proposal-rm-builtin-subclassing). Vermeiden Sie es, sich darauf zu verlassen, wenn möglich.

{{EmbedInteractiveExample("pages/js/symbol-species.html")}}

## Wert

Das bekannte Symbol `Symbol.species`.

{{js_property_attributes(0, 0, 0)}}

## Beschreibung

Die `[Symbol.species]` Zugriffseigenschaft erlaubt es Unterklassen, den Standardkonstruktor für Objekte zu überschreiben. Dies legt ein Protokoll darüber fest, wie Instanzen kopiert werden sollten. Wenn Sie zum Beispiel Kopiermethoden von Arrays verwenden, wie {{jsxref("Array/map", "map()")}}, verwendet die `map()`-Methode `instance.constructor[Symbol.species]`, um den Konstruktor zum Erstellen des neuen Arrays zu erhalten. Weitere Informationen finden Sie unter [Unterklassen von eingebauten Objekten](/de/docs/Web/JavaScript/Reference/Classes/extends#subclassing_built-ins).

Alle eingebauten Implementierungen von `[Symbol.species]` geben den `this`-Wert zurück, welcher der Konstruktor der aktuellen Instanz ist. Dies ermöglicht es Kopiermethoden, Instanzen abgeleiteter Klassen anstelle der Basisklasse zu erstellen – zum Beispiel wird `map()` ein Array desselben Typs wie das ursprüngliche Array zurückgeben.

## Beispiele

### Verwendung von species

Es kann sein, dass Sie {{jsxref("Array")}}-Objekte in Ihrer abgeleiteten Array-Klasse `MyArray` zurückgeben möchten. Zum Beispiel, wenn Sie Methoden wie {{jsxref("Array/map", "map()")}} verwenden, die den Standardkonstruktor zurückgeben, möchten Sie, dass diese Methoden ein übergeordnetes `Array`-Objekt anstelle des `MyArray`-Objekts zurückgeben. Das `species`-Symbol erlaubt Ihnen dies:

```js
class MyArray extends Array {
  // Overwrite species to the parent Array constructor
  static get [Symbol.species]() {
    return Array;
  }
}
const a = new MyArray(1, 2, 3);
const mapped = a.map((x) => x * x);

console.log(mapped instanceof MyArray); // false
console.log(mapped instanceof Array); // true
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`Array[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/Array/Symbol.species)
- [`ArrayBuffer[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer/Symbol.species)
- [`Map[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/Map/Symbol.species)
- [`Promise[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/Promise/Symbol.species)
- [`RegExp[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.species)
- [`Set[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/Set/Symbol.species)
- [`TypedArray[Symbol.species]`](/de/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/Symbol.species)
