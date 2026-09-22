# Fehlerhilfe und bekannte Grenzen

[Übersicht](../README.md) · [Bedienung](USER_GUIDE.md)

Stand: 0.9.54. Bei Problemen zuerst installierte Version, betroffenen Bereich und genaue Statusmeldung festhalten. Screenshots vor dem Teilen auf Zugangsdaten und persönliche Daten prüfen.

## Markt aktiv, aber kein Verkaufspreis

„Aktiv“ allein reicht nicht. Prüfen:

1. Hat das Produkt einen gültigen, gespeicherten EK mit bekannter Währung?
2. Ist diese Währung tatsächlich die Shopwährung beziehungsweise korrekt normalisiert?
3. Hat die Regel eine echte Länderzuordnung und passt ihr Geltungsbereich?
4. Gibt es eine eindeutig passende aktive Regel, ohne Konflikte?
5. Sind benötigte Wechselkurse gültig und aktuell?
6. Welche Begründung steht in der Statusspalte und im Rechenweg?

Bei Altprodukten ohne EK-Währung die vorhandenen Quelldaten öffnen, korrekte Quellwährung wählen und erneut importieren. Keine Währung anhand eines Zahlenformats oder eines Landesnamens raten.

Bei Shop-, EK- und Angebotswährung EUR ist keine EUR-zu-EUR-Umrechnung nötig. Bleibt trotzdem ein Kurshinweis, die vollständige Meldung und die tatsächlich gespeicherten Währungsfelder prüfen; nicht einfach einen Kurs erfinden.

Die Tabelle gespeicherter Marktpreise kann leer bleiben, obwohl „Aktueller VK“ einen berechneten Wert zeigt. Die Vorschau ist kein gespeicherter oder veröffentlichter Preis.

## 0 Länder auf der Marktkarte

Die Zahl soll auch Länder pausierter Regeln zählen. Der Text „Deutschland“ oder ein anderer Ländername im frei vergebenen Regelnamen ersetzt keine Länderzuordnung.

Preisregel öffnen und die gespeicherten Länder/Ländergruppen prüfen. Sind sie vorhanden und bleibt die Zahl nach Aktualisierung falsch, Version und Regelkonfiguration als Fehlernachweis festhalten. Nicht für jedes Land einen zweiten Verkaufskanal anlegen, um die Anzeige zu umgehen.

## Wechselkurs fehlt oder ist veraltet

Fehlende, zukünftige, unplausible oder mehr als vier Kalendertage alte EZB-Grundlagen sowie unvereinbare Kursdaten können die Umrechnung sperren. Nicht jede Währung wird unterstützt. Netzwerkverfügbarkeit und unterstützte Währungen prüfen; ein alter Kurs darf nicht durch bloßes Umdatieren „aktuell“ gemacht werden.

Gleiche Quell- und Zielwährung braucht keinen Umrechnungskurs. Originalpreise und bestehende Produkte müssen bei einer blockierten Umrechnung erhalten bleiben.

## Wiederhergestellte Importauswahl fehlt oder wirkt falsch

Die Wiederherstellung benötigt eine eindeutige Verbindung zum früher importierten Produkt und Lieferanten. Andere Kennungen, andere Lieferantenzuordnung, doppelte Schlüssel oder fehlende Quellzeilen können sie verhindern.

Zeilenreihenfolge ist nicht die Identität. Nicht wahllos alle Zeilen markieren und nicht Produkte löschen, um eine Zuordnung zu erzwingen. Betroffene Schlüssel und die Importprüfung kontrollieren. Neue Produkte bleiben durch die automatische Wiederherstellung unmarkiert, sofern sie nicht bereits bewusst ausgewählt wurden.

Beim Neuimport bleiben zugeordnete vorhandene Produktanhänge erhalten. Explizite Löschaktionen, beschädigte Dateien und nicht mehr erreichbare externe Links sind davon nicht gedeckt.

## Speichern meldet zwischenzeitlich geänderte Daten

Die Meldung schützt vor dem Überschreiben eines neueren Standes. Entwurf soweit möglich sichern, Bearbeitung schließen, aktuellen Stand erneut öffnen und Änderungen prüfen. Nicht durch Manipulation von Versions-/Hashfeldern umgehen. Tritt der Konflikt ohne erkennbare parallele Bearbeitung wiederholt auf, ist das ein untersuchungsbedürftiger Fehler.

## KI antwortet nicht, fragt nach oder liefert nur einen Entwurf

Während einer Anfrage Status und Abbruchmöglichkeit prüfen. Ein Abbruch beendet nicht rückwirkend bereits beim Anbieter entstandene Kosten. Verbindungsfehler oder unvollständige Ergebnisse dürfen nicht als fertige Regel übernommen werden.

Rückfragen stehen im eigenen Reiter. Öffentlich recherchierbare Fakten sollen recherchiert werden; persönliche Kontoeinstellungen oder fachliche Entscheidungen kann die KI nicht zuverlässig erraten. Fehlende Recherchebestätigung ist keine bestätigte Webrecherche.

Ein fortgeschriebener Arbeitsauftrag speichert noch keine Markt-/Versandregel. Entwurf prüfen und übernehmen; anschließend Aktivierungszustand kontrollieren. Eine fremde Sektion darf dabei nicht geändert werden.

## Update nicht verfügbar oder Prüfung scheitert

- Index nicht vorhanden/HTTP 404: Kanal nicht veröffentlicht; kein Nachweis „aktuell“.
- Netzwerkfehler: Status nicht prüfbar.
- Signatur-/Hash-/Inventarfehler: Update ablehnen, nicht Sicherheitsprüfungen deaktivieren.
- Inkompatibler Launcher oder fehlende .NET-Desktop-Runtime: kompatible Installation/Umgebung erforderlich.
- GitHub-Release sichtbar, aber noch nicht angeboten: Nur der gültige signierte Kanalindex aktiviert eine Version.

Keine Pakete, Vertrauensdateien oder Installationsreceipts manuell ersetzen. Die Wiederherstellung eines fehlgeschlagenen Starts und ein fernpublizierter Versionsrücksprung sind unterschiedliche Vorgänge. Archivierte Versionen sind kein freigegebener Downgradeweg.

## Aussagegrenzen

Automatisierte Tests und isoliertes signiertes Staging sind keine vollständige manuelle Prüfung der Benutzerinstallation. Die 0.9.54-Nachweise umfassen keine reale Neuimport-Prüfung sämtlicher Nutzerdaten. Bekannte Sicherheits-/Fachgrenzen dürfen nicht durch pauschale Aussagen wie „alle Produkte funktionieren garantiert“ ersetzt werden.
