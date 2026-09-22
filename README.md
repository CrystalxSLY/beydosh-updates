# Beydosh Update Channel

Öffentlicher Kanal für signierte Updates der Beydosh-Windows-Anwendung. Dieses Repository enthält Update-Metadaten, Dokumentation und Verweise auf Pakete, nicht den Anwendungsquellcode.

## Aktueller Stand

Dokumentationsstand: **22. September 2026**. Im signierten Kanal ist **0.9.54** aktiviert. Die GitHub-Veröffentlichung ist ein **Owner-Development-Prerelease**, keine Freigabe für Live-Verkauf oder eine fertig abgenommene öffentliche Produktversion. Der Verzeichnisname `stable` ändert diese Einordnung nicht.

Maßgeblich ist immer der vom Launcher verifizierte [signierte Kanalindex](updates/stable/latest.beydosh.json), nicht diese Versionsangabe. [Release 0.9.54](https://github.com/CrystalxSLY/beydosh-updates/releases/tag/v0.9.54) enthält das Update-Paket.

## Dokumentation

- [Bedienung: Update, Import, Währungen, Märkte, Versand und KI](docs/USER_GUIDE.md)
- [Fehlerhilfe und bekannte Grenzen](docs/TROUBLESHOOTING.md)
- [Vollständige Versionshistorie 0.9.1–0.9.54](docs/CHANGELOG.md)
- [Veröffentlichung und kryptografischer Update-Vertrag](docs/PUBLISHING.md)
- [Kanalstruktur](updates/stable/README.md)
- [Nachweise und Grenzen der Veröffentlichung 0.9.54](docs/releases/0.9.54-publication.md)
- [Historischer Owner-Test 0.9.1](docs/releases/0.9.1-owner-test.md)

## Update installieren

In einer kompatibel installierten Beydosh-Anwendung **„Nach Aktualisierung suchen“** verwenden und dem angebotenen Update folgen. Der installierte Launcher prüft Signaturen, lädt Pakete, prüft deren Integrität und führt Staging, Aktivierung und Neustart aus.

Das aktuelle Paket richtet sich an **Windows x64**, setzt mindestens Launcher **0.9.0** voraus und ist ein frameworkabhängiger .NET-9-Windows-Build. Eine passende .NET-Desktop-Runtime ist erforderlich. `.bupd`-Dateien sind Transportpakete, **keine direkt ausführbaren Installationsprogramme**. Dieses Repository bietet keinen eigenständigen Erstinstallations-Download an.

Für bestehende Produkte ohne bekannte EK-Währung: Quelldaten unter „Daten bearbeiten“ öffnen, die tatsächliche **EK-Währung der Quelldaten** wählen und erneut importieren. Seit 0.9.54 werden eindeutig zugeordnete, bereits importierte Produkte wieder ausgewählt. Details und Schutzgrenzen stehen in der Bedienungsanleitung.

## Vertrauen und Sicherheit

Verwendet wird ausschließlich **`beydosh-signed-plain-v2`**: signiert, aber bewusst nicht verschlüsselt. Kein AES-Schlüssel und kein encrypted-v1-Fallback. NIST-P-256-Signaturen, fest hinterlegte öffentliche Vertrauensschlüssel, SHA-256, genaue Dateiinventare sowie Versions-, URL- und Replay-Prüfungen sichern den Updatepfad.

Eine gültige Signatur bestätigt Herkunft innerhalb dieses Vertrauensmodells und Integrität. Sie bestätigt weder fachliche Fehlerfreiheit noch Authenticode/SmartScreen-Reputation oder rechtliche Freigaben. Die Trust-Zweckbezeichnung `Production` ist keine Customer-/Legal-Freigabe.

- Index-HTTP-404 bedeutet „Kanal nicht veröffentlicht“, nicht „aktuell“.
- Netzfehler bedeuten „nicht prüfbar“, nicht „aktuell“.
- Ungültige, unvollständige oder nicht vertrauenswürdige Metadaten werden abgelehnt.
- Veröffentlichte Versionsmanifeste, Tags und Paketbytes werden nicht durch andere Inhalte ersetzt. Latest wird bei einem neuen Update zuletzt geändert.

Die [Schemas](schemas/README.md) und [Vorlagen](templates/UNPUBLISHED-NOT-A-RELEASE/README.md) stammen aus dem früheren encrypted-v1-Vertrag und sind **keine gültigen v2-Validatoren**.

Private Schlüssel, Zugangsdaten, Kundendaten und Quellcodearchive gehören weder in dieses Repository noch in Release-Assets oder Logs. Live-Verkauf, echte Bestellungen und reale Kundendatennutzung bleiben bis zu gesondert dokumentierter Freigabe gesperrt.

Eine reine Dokumentationsänderung veröffentlicht keine neue App-Version und verändert keine signierten Update-Dateien.
