# Wiederverwendung: Bestandsprüfung für 0.9.64

Stand: 25.09.2026. Ziel ist eine gemeinsame Quelle für gleiches Verhalten, nicht eine möglichst große Universal-Klasse.

## Umfang und Ergebnis

Quelltextsuche über die Desktop-Anwendung (155 C#-Dateien), ihre XAML-Stile sowie angrenzende Produkt-, Automatisierungs- und Update-Bausteine. Vertieft geprüft wurden wiederkehrende Symbole, Eingabefelder, Zahlenparser, Dateischreibabläufe, Ladehinweise und die bestehenden Fachgrenzen. Dies ist keine vollständige semantische Prüfung jeder Funktion des gesamten Repositories.

| Bereich | Ergebnis und Änderung |
| --- | --- |
| Symbole und Schließen | `UiIcons` und `CloseButton`: zentrale Geometrien/Stile, getrennte visuelle Instanzen, zugängliche Namen. Kopfzeile, interne Seiten, Markteditor, Varianten, Importvorlagen und Kategorien verwenden diese. Fenster-Systembefehle bleiben erhalten. |
| Eingabefelder | `UiFields`: gemeinsame Text-/Mehrzeilenfelder und Auswahllisten für Produkt- und Markt-/Versand-Editoren. Fachliche Höchstlängen, Auswahl, Fehlermarkierungen und Mausradverhalten bleiben beim Aufrufer. |
| Aktionen | `UiActions`: gemeinsame Button-Erzeugung in Attribut-, Markt- und Produktansichten; bestehende Fehlerbehandlung bleibt erhalten. |
| Auswahllisten | Die gemeinsame Vorlage berücksichtigt den ItemTemplateSelector. Dadurch werden DisplayMemberPath-Werte statt interner Objektdarstellungen angezeigt. |
| Zahlen | `DecimalText`: sieben Verbraucherbereiche für PIM-Werte, Produktbearbeitung, Produktpreistabelle, Marktkalkulation, Gebühren-/Gewinnstaffeln und numerische Sortierung. Vorzeichen, äußere Leerzeichen und Trim-Verhalten sind explizit; keine Gruppierung/Exponenten. |
| Entwurfsspeicherung | `AtomicDraftFile`: Kategorie-Chat, Markt-/Versand-Chat und Kategorie-JSON. Temporäre Datei im selben Verzeichnis, Flush auf Datenträger, atomarer Austausch, vorherige Datei als Sicherung, Aufräumen bei Fehlern. Validierung, Pfade, Größenlimits und Revisionssperren bleiben bei den Stores. |
| Ladehinweise | Bestehendes `LoadingNotice` bleibt die gemeinsame Oberfläche. Der Zusatz „Bitte kurz warten“ wird idempotent ergänzt statt mehrfach angehängt. |
| E-Mail | Kontoloser Zustand, Kontoauswahl, Lesen und Schreiben benutzen gemeinsame Stile und Schließen-Bedienung. Keine neue Transportlogik. |
| Buildvarianten | `DesktopSharedDependencies.props` definiert gemeinsame Desktop-Abhängigkeiten zentral für Hauptanwendung, PrivatePreview und UiPreview. Die fehlende MailKit-Referenz im mitbenutzten Quelltext ist damit behoben. PrivatePreview-Launcher bindet das bestehende gemeinsame Fortschrittsfenster ein; Vertrauensvarianten bleiben getrennt. |

## Bewusst nicht zusammengeführt

- Importzahlen mit explizitem Quellen-Zahlenformat: Tausendertrennzeichen und Import-Normalisierung sind ein anderer Vertrag als manuelle Dezimalwerte. Keine stille Änderung importierter Preise.
- Preisrundung: Markt-Aufrunden zum Zielpreis, allgemeine Core-Rundung und ältere Automatisierungsregeln haben unterschiedliche Grenzen und Bedeutung. Keine Änderung des Gewinns durch kosmetisches Refactoring.
- Katalog-, Import-, Credential- und Update-Speicherung: besondere Pfad-/Link-Prüfungen, Locks, Transaktionen, Signaturen und Berechtigungen dürfen nicht durch einen einfachen Entwurfswriter ersetzt werden.
- Fehlerklassen und Abbruch: `DesktopDataOperation`, `SafeErrorLog` und bestehende Fachprüfungen bleiben die zuständigen Bausteine. Nicht jeder ähnliche catch-Block hat denselben Vertrag.
- KI: bestehende gemeinsame Layout-, Aktivitäts-, Rückfragen- und Interaktionsbausteine werden weiterverwendet; keine neue parallele Assistentenarchitektur.
- Lokaler/Core-Betrieb: keine neue Synchronisationszusage. Gemeinsame Logik ist nicht automatisch ein gemeinsamer Datenspeicher.

## Prüfung und weitere Pflege

- Neuer `SharedFoundationTests` prüft über 32.000 Vergleichsfälle gegen das bisherige Dezimalverhalten, negative Werte, gemischte Trennzeichen, Overflow und leere Eingaben.
- Dateitests prüfen Erstanlage, Austausch, unveränderte Sicherung bei blockiertem Ziel und Entfernung temporärer Dateien. Bestehende Chat-Tests prüfen weiterhin Revisionen und Isolation.
- UI-Tests prüfen gemeinsame Stile, zugängliche Feldnamen, genau einen Aktionsaufruf, getrennte Symbolinstanzen sowie E-Mail-Leerzustand, Einrichtung, Kontoisolation, Lesen/Schreiben und Kopfzeilenausrichtung.
- Bestehende Preis-, Import-, Varianten- und Fenstertests bleiben erforderlich. Ein grüner synthetischer Test ist kein Nachweis echten Mailversands oder produktiver Verkäufe.

Offen bleiben spezielle Formularlayouts und weitere historisch ähnliche Abläufe mit unterschiedlichen Verträgen. Neue Arbeiten müssen gemäß `AGENTS.md` zuerst vorhandene Bausteine suchen, geeignete Gemeinsamkeiten nutzen und relevante Restdopplungen benennen. Kein pauschales Ersetzen aller ähnlichen Codezeilen.
