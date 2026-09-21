# Prüfkatalog KI-Sichtbarkeit

Sechs Bereiche, jeder Punkt einzeln prüfbar. Die Reihenfolge ist keine Rangfolge nach
Wichtigkeit, sondern nach Abhängigkeit: Was oben steht, ist Voraussetzung für das, was
darunter kommt.

Jeder Punkt nennt die Prüffrage, den Grund und den Prüfweg. Wo ein Wert keine allgemein
gültige Schwelle hat, steht das dabei, statt eine Zahl zu erfinden.

---

## 1. Maschinelle Auffindbarkeit

Ohne Abruf kein Zitat. Dieser Bereich ist die Eintrittskarte, und er wird am häufigsten
übersehen, weil er in klassischen SEO-Audits als erledigt gilt.

### 1.1 Dürfen die KI-Crawler die Seite holen?

**Prüfen:** `robots.txt` auf Einträge für `GPTBot`, `ClaudeBot`, `PerplexityBot`,
`Google-Extended`, `CCBot`, `Bytespider`, `Applebot-Extended`.

**Warum:** Diese Kennungen sind von den Suchmaschinen-Crawlern getrennt. Eine Website kann
für Google perfekt erreichbar und für KI-Systeme vollständig gesperrt sein, ohne dass das
in einem SEO-Audit auffällt. Umgekehrt entscheidet man sich manchmal bewusst gegen den
Abruf, etwa bei Inhalten, die nicht in Trainingsdaten sollen. Beides ist vertretbar, aber
es muss eine Entscheidung sein und kein Versehen.

**Achtung bei `Google-Extended`:** Die Kennung steuert die Verwendung in Gemini und den
Trainingsdaten, nicht die Anzeige in den AI Overviews. Wer dort nicht erscheinen will,
erreicht das über `robots.txt` nicht.

### 1.2 Steht der Inhalt ohne JavaScript im HTML?

**Prüfen:** Seite ohne JavaScript-Ausführung abrufen, etwa per `curl`, und zählen, wie viel
sichtbarer Text im ausgelieferten HTML steht.

**Warum:** Ein Teil der KI-Crawler rendert kein JavaScript. Eine Single-Page-Anwendung, die
erst im Browser Text erzeugt, liefert diesen Crawlern eine leere Seite. Ein gemessener Fall
aus der Praxis: 79 Zeichen Text im HTML gegenüber 4.117 nach der Umstellung auf
serverseitiges Rendering.

### 1.3 Antwortet die Seite schnell genug?

**Prüfen:** Serverantwortzeit bei kaltem Cache, nicht nur beim zweiten Aufruf.

**Warum:** Crawler treffen einzelne URLs meist kalt. Wer nur warm misst, misst den Cache
und nicht die Realität. Eine Seite, deren Long-Tail regelmäßig zwei Sekunden bis zum ersten
Byte braucht, wird seltener und flacher erfasst.

### 1.4 Gibt es eine `llms.txt`?

**Prüfen:** `/llms.txt` abrufen, auf Erreichbarkeit und darauf, ob die dort verlinkten URLs
leben.

**Warum:** Das Format ist kein Standard, den ein Anbieter garantiert ausliest. Der Nutzen
liegt darin, dass es zwingt, den eigenen Bestand zu ordnen und die wichtigsten Einstiege zu
benennen. Der häufigste Fehler ist eine Datei, die nach Monaten auf gelöschte Seiten zeigt.
Prüfe jede URL darin auf Status 200, nicht nur die Existenz der Datei.

**Keine `noindex`-Seiten in die `llms.txt` aufnehmen.** Wer eine Seite aus dem Index hält
und sie gleichzeitig Modellen anbietet, widerspricht sich.

---

## 2. Entität

Ein Modell zitiert Quellen, denen es eine Identität zuordnen kann.

### 2.1 Ist die Organisation als eine Einheit erkennbar?

**Prüfen:** Über alle Seiten hinweg auszählen, wie oft die Organisation im JSON-LD definiert
wird und unter welchen `@id`-Werten.

**Warum:** Wenn jede Seite eine eigene `Organization` ohne gemeinsame Kennung definiert,
entstehen viele Objekte statt einer Entität. Richtig ist ein globaler Knoten mit fester
`@id`, auf den alle Seiten per Referenz zeigen.

### 2.2 Tragen Organisation und handelnde Personen normierte Kennungen?

**Prüfen:** Vorhandensein von ISNI, ORCID, GND, Wikidata, Handelsregister, und ob sie im
Schema als `identifier` und `sameAs` hinterlegt sind.

**Warum:** Normierte Kennungen sind der Weg, auf dem verschiedene Datenbestände dieselbe
Entität zusammenführen. Sie sind der Unterschied zwischen „eine Firma, die so heißt" und
„diese Firma". ISNI wird über eine Registrierungsagentur vergeben und verlangt einen
Werknachweis, ORCID ist selbst anlegbar.

**Vor der Registrierung auf Dubletten prüfen.** Eine doppelte Kennung ist schwerer zu
beseitigen als ein doppeltes Verzeichnisprofil.

### 2.3 Stimmen die Angaben über alle Quellen hinweg überein?

**Prüfen:** Name, Anschrift, Telefonnummer, Gründungsjahr, Mitarbeiterzahl und
Selbstbeschreibung auf der Website mit allen Verzeichnisprofilen vergleichen.

**Warum:** Modelle meiden Quellen, die sich selbst widersprechen, und sie ziehen
Beschreibungen aus Verzeichnissen, nicht nur von der eigenen Website. Ein gemessener Fall:
Die Beschreibung einer Firma in einer KI-Antwort stammte wörtlich aus zwei
Verzeichnisprofilen und enthielt eine Positionierung, die die Firma seit Jahren nicht mehr
verwendete. Zwei unabhängige Domains mit identischem Wortlaut wirken wie eine Bestätigung.

### 2.4 Gibt es die Entität außerhalb der eigenen Website?

**Prüfen:** Erwähnungen in Fachpublikationen, Verzeichnissen, Katalogen von Bibliotheken,
Wikidata.

**Warum:** Eine Entität, die nur über sich selbst spricht, ist schwach belegt. Externe
Nennungen sind der Beleg, den ein System gegenprüfen kann.

---

## 3. Strukturierte Daten

### 3.1 Sind die Knoten verknüpft statt dupliziert?

**Prüfen:** Auf einer Unterseite nachsehen, ob Autor, Organisation und Website per `@id`
referenziert oder erneut vollständig definiert werden.

**Warum:** Referenzen bauen einen Graphen, Duplikate bauen Rauschen.

### 3.2 Definieren zwei Quellen denselben Knoten?

**Prüfen:** Alle JSON-LD-Blöcke einer Seite einsammeln und nach doppelten `@id`-Werten
suchen, besonders wenn ein SEO-Plugin und eine eigene Auszeichnung parallel laufen.

**Warum:** Bei Knoten, deren Inhalt aus **Feldern** besteht, ergänzen sich zwei Quellen
harmlos. Bei Knoten, deren Inhalt eine **Liste** ist, widersprechen sie sich. Ein
gemessener Fall: Zwei `BreadcrumbList`-Definitionen unter derselben `@id`, beide für sich
korrekt, führten nach dem Zusammenführen zu Validierungsfehlern auf mehreren hundert
Seiten. Die Regel lautet: Vor jedem neuen Knotentyp prüfen, ob eine andere Quelle denselben
Typ unter derselben Kennung liefert. Wenn ja, muss eine weichen.

### 3.3 Ist `speakable` gesetzt, und zeigt es auf existierende Elemente?

**Prüfen:** Ob die im `speakable`-Feld genannten CSS-Klassen im ausgelieferten HTML
tatsächlich vorkommen.

**Warum:** Eine Auszeichnung, die auf eine Klasse zeigt, die es auf der Seite nicht gibt,
ist wirkungslos. Der Fehler entsteht typischerweise, wenn das Schema aus einer Vorlage
kommt und das Layout später geändert wurde.

### 3.4 Ist die Sprachangabe die reale Seitensprache?

**Prüfen:** `inLanguage` im Schema gegen `<html lang>` und den tatsächlichen Text.

**Warum:** Ein Array aus zwei Sprachen behauptet eine Zweisprachigkeit, die eine einzelne
URL nicht hat. Das kommt häufig aus der Zeit, als eine Domain über ein Übersetzungswerkzeug
zwei Sprachen auslieferte.

---

## 4. Zitierfähige Inhalte

### 4.1 Steht die Aussage im ersten Satz?

**Prüfen:** Bei Definitions- und Erklärseiten: Enthält der erste Satz die Definition, oder
kommt zuerst Herleitung, Kontrast oder ein Einschub?

**Warum:** Herausgelöst wird der Abschnitt, nicht die Seite. Ein Einschub vor der Aussage
verschiebt den Kern an eine Stelle, an der er beim Zerlegen verloren geht. „Ein Keyword, auch
bekannt als Schlüsselwort oder Suchbegriff, ist ein …" gehört umgestellt zu „Ein Keyword ist
… Es wird auch Schlüsselwort oder Suchbegriff genannt."

### 4.2 Sind die Abschnitte für sich verständlich?

**Prüfen:** Einen beliebigen Abschnitt aus dem Zusammenhang nehmen und lesen. Ergibt er
allein noch eine vollständige Aussage?

**Warum:** Genau das passiert bei der Einbettung.

### 4.3 Beantwortet die Seite eine Frage, die jemand stellt?

**Prüfen:** Die Überschriften gegen reale Fragestellungen halten.

**Warum:** Antworten entstehen zu Fragen. Eine Seite, die ein Thema umkreist, aber keine
Frage beantwortet, liefert keinen Abschnitt, der zu einer Anfrage passt.

### 4.4 Gibt es Substanz, die nur hier steht?

**Prüfen:** Eigene Zahlen, eigene Fälle, eigene Messungen im Text.

**Warum:** Ein System, das zwischen zwanzig gleichlautenden Quellen wählt, hat keinen Grund,
ausgerechnet eine davon zu nennen. Eine eigene Messung ist ein Grund.

---

## 5. Messung

### 5.1 Wird über mehrere Systeme gemessen?

**Prüfen:** Mindestens ChatGPT, Gemini, Perplexity, den KI-Modus von Google und die AI
Overviews.

**Warum:** Dieselbe Frage führt zu grundlegend verschiedenen Ergebnissen. Ein gemessener
Fall: keine Nennung bei Perplexity und ChatGPT, gleichzeitig Platz 2 im KI-Modus von Google.
Wer aus einem System schließt, misst Zufall.

### 5.2 Wird mit mehreren Formulierungen gemessen?

**Prüfen:** Dieselbe Kaufabsicht in mindestens drei Varianten, darunter Singular und Plural.

**Warum:** Der Wortlaut entscheidet mit. Im gemessenen Fall wechselte zwischen Singular und
Plural derselben Frage die halbe Ergebnisliste.

### 5.3 Wird die Quellenziehung erfasst, nicht nur die Nennung?

**Prüfen:** Ob die eigene Domain in den angegebenen Quellen der Antwort auftaucht, getrennt
von der Frage, ob die Marke im Text genannt wird.

**Warum:** Die Nennung schwankt, die Quellenziehung erklärt sie. Wo die eigene Seite als
Quelle gezogen wurde, kam die Marke vor; wo nicht, fehlte sie.

### 5.4 Ist klar, dass rückwirkend nichts messbar ist?

**Warum:** Eine Modellantwort existiert nur, wenn sie zum Zeitpunkt X erhoben wurde. Niemand
sammelt sie auf Vorrat. Wer heute anfängt, hat ab heute Daten. Rückwirkend gibt es nur die
Referrer der eigenen Webanalyse und die klassische Ranking-Historie.

---

## 6. SEO-Fundament

Kein eigenes Kapitel im engeren Sinn, aber die Voraussetzung für alles darüber: Die Systeme
greifen überwiegend auf Quellen zurück, die organisch auffindbar sind.

### 6.1 Ist die Seite indexierbar und indexiert?

Ein `noindex`, das niemand gesetzt haben wollte, ist der häufigste stille Totalausfall.

### 6.2 Hat die Seite genau eine H1, und beschreibt sie den Inhalt?

Mehrere H1 entstehen oft unbemerkt, wenn ein Template eine Überschrift rendert und der
Inhalt eine zweite mitbringt.

### 6.3 Ist die Seite intern verlinkt, und zwar redaktionell?

Links aus Navigation und Fußzeile stehen auf jeder Seite und werden entsprechend gewichtet.
Entscheidend sind Links aus dem Fließtext thematisch passender Seiten. Eine Seite, die nur
an der Navigation hängt, hat kein Signal.

### 6.4 Konkurrieren mehrere eigene Seiten um dieselbe Frage?

Wenn zwei eigene Seiten dieselbe Zuständigkeit beanspruchen, teilen sie sich die Signale.
Prüfbar über die gesetzten Fokuskeywords des gesamten Bestands, nicht über Titel und
Adressen: Die Zuständigkeit steht im Fokuskeyword, nicht im Namen.

---

## Stand

21. September 2026. Gepflegt von der [taismo GmbH](https://taismo.de/), München.
Korrekturen willkommen, am liebsten mit der Messung, die dagegen spricht.
