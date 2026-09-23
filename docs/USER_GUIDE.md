# Beydosh bedienen

[Zur Übersicht](../README.md) · [Fehlerhilfe](TROUBLESHOOTING.md) · [Versionshistorie](CHANGELOG.md)

Stand: 0.9.56, 23.09.2026. Beschrieben ist der aktuelle Owner-Development-Stand, keine Freigabe für produktiven Handel.

## 1. Aktualisieren und Daten erhalten

„Nach Aktualisierung suchen“ startet den verifizierten Updatepfad. Ein GitHub-Release allein aktiviert keinen Kanal; dafür ist der gültige signierte Latest-Index maßgeblich. Pakete nicht manuell in die Installation entpacken und keine Receipts oder Vertrauensdateien ändern.

Programmdateien liegen normalerweise unter `%LOCALAPPDATA%/Programs/Beydosh`, Benutzerdaten getrennt unter `%LOCALAPPDATA%/Beydosh`. Vor größeren Importänderungen die Anwendung schließen und eine geeignete Sicherung der eigenen Daten anlegen. Das Beibehalten von Daten bei einer Deinstallation ersetzt keine Sicherung. Zugangsdaten liegen in gesonderten Windows-Vault-Einträgen; sie gehören nicht in veröffentlichte Archive.

Alte Programmversionen nicht ungeprüft über neuere Daten installieren. Eine vorhandene ältere Setup-Datei ist keine sichere Datenmigration oder Rücksetzfunktion.

## 2. Shopwährung und Einkaufspreise

Unter Einstellungen wird die Shopwährung festgelegt. Sie ist die gemeinsame Berechnungsbasis, nicht automatisch die Währung jeder Lieferantendatei oder jedes Angebots.

Der Ablauf ist:

1. EK aus den unveränderten Quelldaten mit seiner tatsächlichen Quellwährung lesen.
2. Falls erforderlich in die Shopwährung umrechnen.
3. Den normalisierten EK mit seiner Währung im Produkt speichern.
4. Je Verkaufskanal und Land die passende Preisregel auf diesen EK anwenden.
5. Das Ergebnis in die Angebotswährung umrechnen.
6. **Erst dort** die Rundungsregel anwenden; den Euro-Gegenwert aus diesem gerundeten Angebotspreis bestimmen.

Gewinnziele, Gebühren und Rundung sind konfigurierbar. Es gibt weder einen fest eingebauten Anbieter noch einen allgemeinen Gewinnaufschlag von 10 EUR.

Die Shopwährung lässt sich bei vorhandenen betroffenen Preisen/Regeln nicht einfach umbenennen: Das würde bestehende Geldwerte falsch kennzeichnen. Ein notwendiger Währungswechsel erfordert einen kontrollierten Daten-/Migrationsweg.

## 3. Import und erneuter Import

In „Daten bearbeiten“ beziehungsweise der Importprüfung steht **„EK-Währung der Quelldaten“** neben **„Zahlenformat“**. Zahlenformat bestimmt die Zahlinterpretation, nicht die Währung.

- Die tatsächliche Quellwährung auswählen. Alternativ muss eine geeignete Währungsspalte zugeordnet sein.
- Widersprechen sich ausgewählte Währung und zugeordneter Zeilenwert, wird der Preis nicht stillschweigend umgedeutet.
- Bei gleicher Quell- und Shopwährung ist kein Wechselkurs nötig.
- Bei Umrechnung werden passende, aktuelle EZB-Kurse verlangt. Fehlende oder ungültige Grundlagen dürfen vorhandene Preise nicht überschreiben.
- Quellbetrag, Quellwährung und Umrechnungsnachweis bleiben nachvollziehbar. Die Originaldatei wird nicht umgeschrieben.
- Automatische Abrufe nutzen die gespeicherte EK-Währung.
- Wiederholte Importe beginnen beim Originalbetrag, nicht beim bereits umgerechneten Produkt-EK.

### Bereits importierte Produkte wieder auswählen

Seit 0.9.54 werden beim erneuten Öffnen der Daten eindeutig zuordenbare, zuvor importierte Produkte wieder ausgewählt. Die Zuordnung basiert auf Produktkennungen und Lieferantenbezug, nicht auf der früheren Zeilennummer. Eine andere Zeilenreihenfolge allein soll deshalb keine falschen Produkte auswählen.

Neue, zuvor nicht ausgewählte Produkte werden dadurch nicht automatisch ausgewählt. Bereits bewusst gespeicherte Auswahlen bleiben erhalten. Mehrdeutige oder nicht mehr zuordenbare Zeilen müssen geprüft werden. Innerhalb der geöffneten Bearbeitung kann die Auswahl geändert werden; beim erneuten Öffnen greift wieder die Wiederherstellung.

Für eine EK-Währungskorrektur:

1. Die vorhandenen Importdaten öffnen.
2. Wiederhergestellte Auswahl und Identitäten prüfen.
3. Richtige Quellwährung auswählen.
4. Importprüfung und eventuelle Hinweise beachten.
5. Erneut importieren; anschließend ein Beispielprodukt prüfen.

Lieferanten-/Produktkennungen nicht ändern, um die Zuordnung zu erzwingen. Das kann neue Produkte statt einer Aktualisierung erzeugen.

### Was beim Neuimport erhalten bleibt

Bei eindeutig zugeordneten vorhandenen Produkten bleiben Produkt-ID und bestehende Bilder, benannte Downloads sowie lokale Dateianhänge erhalten. Diese Fälle sind automatisiert getestet. Ein erneuter Import ersetzt nicht pauschal das ganze Produkt einschließlich seiner Anhänge.

Nicht zugeordnete Quellspalten sind kein Auftrag, bestehende Felder zu löschen. Leere Preis-/Bestandswerte werden nicht einfach als Null übernommen. Andere ausdrücklich zugeordnete beschreibende Felder können jedoch durch den Import verändert werden: „Neuimport“ bedeutet nicht „alle bisherigen Felder unveränderbar“.

Abwählen oder Entfernen einer Quellzeile löscht nicht automatisch das bereits angelegte Produkt. Explizites Löschen von Produkten/Anhängen und die spätere Erreichbarkeit externer Bildlinks sind davon getrennte Vorgänge.

### Reservierte und wiederhergestellte IDs

Seit 0.9.55 erscheinen bereits reservierte IDs beim erneuten Öffnen unveränderter gespeicherter Importdaten sofort. Ein gelöschtes Produkt kann seine bisherige ID zurückbekommen, wenn es innerhalb desselben Lieferanten anhand Lieferanten-Artikelnummer, SKU oder gültiger EAN/GTIN eindeutig wiedererkannt wird und keine andere vorhandene Kennung widerspricht. Mehrdeutige Treffer werden gesperrt. Alte IDs werden nicht allgemein für andere Produkte freigegeben.

0.9.56 behebt einen Fehler aus 0.9.55: Ein einzelner uneindeutiger Wiederherstellungstreffer brach dort die gesamte ID-Reservierung ab. Jetzt werden solche Zeilen einzeln mit einem konkreten Hinweis gesperrt; unabhängige eindeutige Zeilen erhalten weiterhin IDs und können importiert werden. Zusätzliche passende Kennungen können eine mehrfach vorhandene EAN disambiguieren. Widersprüche werden nicht übergangen. Nach einem Import mit Hinweisen die betroffenen Zeilen prüfen; ein Teilimport ist kein erfolgreicher Import sämtlicher ausgewählter Produkte.

Frühere Löschungen werden aus den ausdrücklich im Löschprotokoll benannten Sicherungen rekonstruiert. Fehlt dieser Nachweis, wird nicht geraten. Wiederhergestellt wird die Identität, nicht automatisch jeder bewusst gelöschte Anhang oder alte Datenstand. Bei großen Löschungen läuft die Verarbeitung im Hintergrund; die Ladeanzeige informiert über die Aktion. Vorher wird weiterhin eine Sicherung erstellt.

## 4. Verkaufskanäle und Länderpreise

Ein Verkaufskanal beschreibt eine Plattform oder einen Shop. Innerhalb **desselben Kanals** können Länder unterschiedliche Preisregeln und Angebotswährungen erhalten. Für jedes Land einen neuen gleichnamigen Kanal anzulegen ist nicht erforderlich.

1. Verkaufskanal anlegen und auswählen.
2. Länder beziehungsweise Ländergruppen und Preisregeln konfigurieren.
3. Gebühren, Gewinnziel, Geltungsbereich und Rundung prüfen.
4. Beispielprodukte kalkulieren.
5. Den Kanal bei geeigneten Regeln über **„Markt aktivieren“** aktivieren.

Die Karte zeigt aktiv/inaktiv; bei Aktivierung wechselt der Button zu **„Markt deaktivieren“**. Der Schalter wirkt auf alle Regeln der Karte. Ein Kanal mit mindestens einer aktiven Regel gilt als aktiv. Konflikte mehrerer gleichzeitig geltender aktiver Regeln für dasselbe Land werden nicht stillschweigend aufgelöst. Ohne Preisregel ist eine Aktivierung nicht sinnvoll/verfügbar.

Die Länderanzahl umfasst konfigurierte Länder auch bei pausierten Regeln. „0 Länder“ trotz Ländername im Regeltext ist deshalb kein Beweis, dass eine tatsächliche Länderzuordnung gespeichert wurde; die Zuordnung in der Regel prüfen.

### Kalkulation

Seit 0.9.55 ist der VK ausdrücklich der **Brutto-Endpreis** inklusive des eingetragenen Verkaufssteuersatzes. Der Rechenweg zeigt Netto, Steueranteil und Endpreis getrennt. Vorhandene Steuersätze werden nicht automatisch geändert. Bei zutreffender Steuerbefreiung gibt es keinen pauschalen Verkaufssteueraufschlag; Gebührensteuer ist eine andere Kostenposition. Die alte separate Nettomarktpreis-Tabelle bleibt weiterhin netto bezeichnet.

Der EK muss wirtschaftliche Einkaufskosten darstellen: ohne abziehbare Vorsteuer, aber einschließlich nicht abziehbarer Steuer. Der Import rechnet nur Währungen um, nicht brutto in netto. Steuerstatus, EK-Steuerbasis und zusätzliche Plattform-Steuern beim Checkout müssen zum tatsächlichen Fall passen. Die KI soll unklare Brutto-/Netto-Vorgaben gezielt klären, statt Steuersätze zu erfinden.

Seit 0.9.56 zeigt die Auswahl eines Marktes seine Preisregeln als **waagerechte Kalkulationsreihe von EK bis VK brutto**. Pfeile führen das Zwischenergebnis weiter; Plus, Minus, Multiplikation, Division und Klammern zeigen den jeweiligen Rechenschritt. Die Reihe übernimmt Gewinnmodell, Gebührenbasis, Steuer, Wechselkurs und Rundung aus der Regel. Lange Reihen sind seitlich scrollbar. Die gleiche Ansicht erscheint in KI-Entwürfen und der Preisregel-Beispielrechnung; geänderte Eingaben machen die bisherige Beispielreihe bis zur Neuberechnung ungültig.

Der Markt berechnet deterministisch aus dem gespeicherten EK in Shopwährung. Gewinnmodelle und Gebühren sind konfigurierbar. Prozentuale Gebühren auf den Verkaufspreis müssen aus dem Verkaufspreis zurückgerechnet werden; sie sind nicht einfach derselbe prozentuale Aufschlag auf den EK.

Geltungsbereich, Gebührenstaffeln, Mindestgebühren, Zusatzkosten, Steuereinstellungen und Kontobedingungen müssen zur Regel passen. Ein erfolgreicher Beispielpreis beweist keine Abdeckung aller Produkte. Die Anzahl der importierten Artikel ersetzt keine Prüfung ihrer Währung, Kategorie und Regelzuordnung.

Ist keine Angebotswährung ausdrücklich vorgegeben, wird die Länderwährung berücksichtigt; eine ausdrücklich konfigurierte Angebotswährung kann davon abweichen. Die Rundung bezieht sich auf die tatsächliche Angebotswährung, nicht zuerst auf EUR.

## 5. VK im Produkt sehen

Unter **„Preise & Märkte“** zeigt **„Aktueller VK aus Verkaufskanal-Regeln“** die aktuelle Berechnung aus gespeicherten Produktdaten, gruppiert nach Verkaufskanal und darunter nach Land. Sichtbar sind Angebots-VK, Euro-Gegenwert, Preisregel, Verdienst und Status.

Aktive passende Regeln liefern automatisch eine aktuelle Kalkulation. Pausierte Regeln sind nur Vorschau. Änderungen im Produkt müssen zuerst gespeichert sein. Bei fehlender Berechnungsgrundlage erscheint ein Status statt eines erfundenen Preises.

**Aktuelle Kalkulation und gespeicherter Verkaufspreis sind verschieden:** Die automatische Anzeige speichert oder veröffentlicht kein Angebot. Der Bereich mit gespeicherten Verkaufspreisen enthält übernommene Preisstände und kann leer sein, obwohl eine aktuelle Kalkulation vorliegt. Gespeicherte Werte können nach Regeländerungen veraltet sein und müssen erneut geprüft werden.

Den aufklappbaren Rechenweg und „Preise aus Verkaufskanal-Karten prüfen“ zur Kontrolle verwenden. Zum Test verschiedene EK-Höhen, Länder und relevante Regelgrenzen wählen, nicht nur einen einzelnen Artikel.

## 6. Versand bleibt getrennt

Im Menü **„Versand“** werden Versanddienste und Tarife eingerichtet. Unterstützte Kalkulationsformen umfassen feste Beträge, Staffeln und Formeln sowie unterschiedliche Berechnungsbezüge. Eine benannte Dienstkarte ist noch keine echte Anbieteranbindung.

Die Märkte-KI kalkuliert den Marktanteil; Versand wird separat unter „Versand“ kalkuliert und nicht automatisch als kostenlos behandelt. Vorhandene ausdrücklich konfigurierte manuelle Versandverknüpfungen sind gesondert zu prüfen. Die Märkte-KI darf keine Versanddienste oder Versandregeln ändern.

Eine spätere automatische optionale Einbeziehung von Versand abhängig von Plattform-Schnittstellen ist nicht als bereits vollständige Funktion zu verstehen. Es werden keine Versandlabels erzeugt oder Sendungen gebucht. Die Artikelkalkulation ist kein vollständiger gemischter Warenkorb-/Paketoptimierer.

## 7. Gemeinsamer KI-Assistent

Kategorien, Märkte und Versand verwenden ein gemeinsames Grundlayout mit bereichsspezifischer Vorschau und Aktionen:

- Links aktueller Stand, vorgeschlagene Änderungen und **Rückfragen**.
- Rechts Gespräch und Eingabe.
- Arbeitsstatus und Stopp-/Abbruchmöglichkeit während einer Anfrage.
- Schriftgröße, Entwurf laden/speichern, Arbeitsauftrag und optionale Webrecherche.
- Quellen-/Verbrauchshinweise, soweit tatsächlich geliefert.

Bei Rückfragen wird der entsprechende Reiter geöffnet. Fragen lassen sich zur Beantwortung in das Eingabefeld übernehmen. Die angezeigten Arbeitsschritte sind Statusmeldungen, keine Garantie vollständiger Recherche oder fehlerfreier Ergebnisse.

In Märkten/Versand ist der Assistent erst für einen bereits erstellten und ausgewählten Kanal/Dienst verfügbar. Die Bereiche bleiben getrennt: Märkte dürfen keine Kategorien oder Versandtarife erstellen, Versand darf keine Marktregeln ändern und Kategorien keine fremden Bereiche bearbeiten.

Der Arbeitsauftrag beschreibt das gewünschte Ergebnis. Bei Märkten und Versand wird er aus dem Gespräch fortgeschrieben, wenn der Nutzer Änderungen wünscht. Das ist keine automatische Freigabe des resultierenden Regelentwurfs. Entwürfe prüfen und bewusst übernehmen; neue/geänderte Regeln bleiben zur Prüfung pausiert.

Die KI soll recherchieren, erklären und einen prüfbaren Vorschlag erstellen. Notwendige kontospezifische Angaben oder Entscheidungen können Rückfragen erfordern. Quellen können veraltet oder unvollständig sein; bestätigte Webrecherche und reine Modellantworten sind zu unterscheiden. Gebühren-/Steuerannahmen nicht ungeprüft aktivieren.

Anfragen gehen an den konfigurierten KI-Dienst und können Kosten verursachen. Verbrauchswerte sind nicht automatisch eine verlässliche Geldkostenabrechnung. Keine Zugangsdaten oder unnötigen personenbezogenen Daten in Arbeitsauftrag, Chat oder Entwurfsdateien eingeben. KI-Texte dürfen keine Produktdaten erfinden.

## 8. Grenzen

Kalkulation, lokale Speicherung, Aktivierung einer Preisregel und Veröffentlichung auf einer Plattform sind getrennte Schritte. Das aktuelle System eröffnet durch „Markt aktivieren“ keinen Live-Verkauf und führt keine Bestellungen aus. Rechtliche/steuerliche Angaben bleiben prüfpflichtige Arbeitsunterlagen.
