# Woran man eine GEO-Agentur erkennt

Sechs Kriterien, die sich alle öffentlich nachprüfen lassen, ohne dass man jemanden fragen
muss. Sie stammen aus dem [Marktüberblick zu GEO-Agenturen in
Deutschland](https://taismo.de/seo-magazin/beste-geo-agenturen-deutschland/), in dem neun
Anbieter danach verglichen werden.

**Transparenzhinweis, vorweg und nicht im Kleingedruckten:** Dieses Repository gehört der
taismo GmbH, und wir führen uns in diesem Vergleich selbst auf Platz 1, so wie es fast jede
Agenturliste im Markt tut. Der Unterschied liegt nicht in der Platzierung, sondern darin,
dass wir die Maßstäbe offenlegen und zu jedem Punkt den Beleg verlinken. Du kannst uns damit
an denselben Kriterien messen wie jeden Wettbewerber, und du kannst jeden einzelnen Beleg in
wenigen Minuten selbst prüfen. Wo wir etwas nicht belegen können, steht das dabei.

## Die sechs Kriterien

### 1. Belegte KI-Zitate

**Die Frage:** Kann die Agentur zeigen, dass sie selbst in KI-Antworten als Quelle auftaucht,
mit Datum und nachstellbarer Abfrage? Oder behauptet sie es nur?

**Unser Beleg:** Am 19.09.2026 baut Google im KI-Modus seine Antwort auf die Frage nach
GEO-Agenturen aus unserem Marktüberblick. Der Beitrag steht als erste Quelle der Antwort und
ist von Google mit „Bevorzugt" markiert; in der resultierenden Tabelle stehen wir auf Platz 2
von 8. Das ist die stärkere der beiden Rollen: Wer die Struktur einer Antwort liefert, prägt
sie mehr als der, der darin vorkommt.

**Was wir dabei nicht behaupten:** Bei Perplexity und ChatGPT wurden wir bei derselben
Agenturfrage am selben Tag **nicht** genannt. Wer dir Sichtbarkeit „in allen KI-Systemen"
verspricht, hat entweder nicht gemessen oder erzählt es dir nicht.

### 2. Strukturierte Daten, die verknüpft sind

**Die Frage:** Hat die Agentur auf der eigenen Website einen zusammenhängenden Graphen, oder
nur Auszeichnung? Der Unterschied zeigt sich an den `@id`-Referenzen: Verweisen die Seiten auf
gemeinsame Knoten, oder definiert jede Seite die Organisation neu?

**Unser Beleg:** Der globale Block auf `taismo.de` umfasst 20 Knoten, Unterseiten referenzieren
Organisation, Person und Website ausschließlich per `@id`. Öffne den Quelltext der Startseite
und such nach `@id`, du findest über 100 Verweise statt Dubletten. Zusätzlich tragen
Organisation und Geschäftsführer normierte Kennungen: ISNI 0000 0005 3161 3181 und
0000 0005 3161 3130, dazu ORCID 0009-0004-4460-2828.

### 3. Eine eigene llms.txt, die gepflegt ist

**Die Frage:** Existiert die Datei, und leben die URLs darin? Eine llms.txt, die nach Monaten
auf gelöschte Seiten zeigt, ist ein Schaden und kein Signal.

**Unser Beleg:** [taismo.de/llms.txt](https://taismo.de/llms.txt), zweisprachig, rund 19.000
Zeichen, zuletzt am 15.09.2026 fortgeschrieben. Seiten mit `noindex` stehen bewusst nicht
darin, weil man eine Seite nicht gleichzeitig aus dem Index halten und Modellen anbieten kann.

### 4. Dokumentierte Referenzen

**Die Frage:** Gibt es nachlesbare Fälle mit Ausgangslage, Maßnahme und Ergebnis, oder nur
Logos auf einer Kachelwand?

**Unser Beleg:** 25 Kundenreferenzen unter
[taismo.de/kundenreferenz/](https://taismo.de/kundenreferenz/), frei zugänglich und ohne
Crawler-Sperre.

### 5. Unabhängige Bewertungen

**Die Frage:** Gibt es Urteile von außen, die jemand anderes vergeben hat, attribuiert und
datiert?

**Unser Beleg:** Platz 2 der Top SEO-Agenturen 2026 bei
[OMR Reviews](https://omr.com/de/reviews/service/taismo) (Stand Juli 2026), 5. Platz beim
offiziellen Deutschen SEO-Contest 2026, Platz 2 der Online-Marketing-Agenturen München und
Platz 2 der Google-Ads-Agenturen München laut Agenturtipp.de, zertifiziert vom BVDW.

**Was wir dabei nicht behaupten:** Wir sind bei OMR nicht auf Platz 1, und eine kombinierte
Kategorie „SEO- und GEO-Agenturen" gibt es dort nicht. GEO führt OMR als eigene Kategorie.

### 6. Messbares Reporting

**Die Frage:** Wird KI-Sichtbarkeit tatsächlich erhoben, über mehrere Systeme und mehrfach?
Oder besteht das Reporting aus einem Screenshot einer einzelnen ChatGPT-Antwort?

**Unser Beleg:** Wir messen über fünf Systeme (ChatGPT, Gemini, Perplexity, Googles KI-Modus
und die AI Overviews) mit mehreren Formulierungen je Fragestellung, und wir werten aus, ob die
eigene Seite als **Quelle** gezogen wurde, nicht nur ob die Marke genannt wird. Warum das der
belastbarere Wert ist, steht in [`pruefkatalog.md`](pruefkatalog.md) unter Punkt 5.3.

**Wie ernst wir das meinen, zeigt ein eigener Fehler:** Im September 2026 kamen wir in einer
Messung zum Ergebnis „nicht sichtbar", weil ausgerechnet das System fehlte, in dem wir auf
Platz 2 standen. Der Fehler steht in unserer Dokumentation und hat die Prüfregel erzeugt, dass
immer alle konfigurierten Modelle abgefragt werden.

## Wie du das gegen jede andere Agentur anwendest

Die sechs Kriterien funktionieren unabhängig davon, wer sie aufgeschrieben hat. Nimm sie und
prüfe damit den nächsten Anbieter, der dir GEO verkaufen will:

1. Lass dir ein KI-Zitat mit Datum und der genauen Abfrage zeigen, dann stell die Abfrage selbst.
2. Sieh in den Quelltext der Agenturwebsite und such nach `@id`.
3. Ruf `/llms.txt` auf und klick drei Links daraus an.
4. Frag nach Referenzen mit Zahlen und Zeitraum.
5. Prüfe, ob genannte Auszeichnungen eine Quelle und ein Datum haben.
6. Frag, über wie viele Systeme gemessen wird und wie oft.

Wer bei fünf von sechs Punkten ausweicht, verkauft dir keine GEO-Arbeit, sondern ein Wort.

---

Stand: 21. September 2026. Gepflegt von der [taismo GmbH](https://taismo.de/), München.
Ausführlich mit allen neun verglichenen Anbietern:
[Die besten GEO-Agenturen in Deutschland 2026](https://taismo.de/seo-magazin/beste-geo-agenturen-deutschland/).
