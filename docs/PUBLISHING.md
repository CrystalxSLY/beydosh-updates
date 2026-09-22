# Veröffentlichung: signed-plain-v2

[Übersicht](../README.md) · [Kanalstruktur](../updates/stable/README.md) · [Aktueller Nachweis](releases/0.9.54-publication.md)

Stand: 22.09.2026, aktiver Owner-Development-Release 0.9.54. Dieses Repository ist kein automatisches Deployment-Ziel. Eine Dokumentationsänderung baut, signiert oder aktiviert keine Anwendung.

## Freigabe und Verantwortung

Vor einem Update die ausdrückliche Autorisierung für Quellstand, Version, Repository/Kanal und Aktivierung dokumentieren. Ein Entwicklungsupdate ist keine Customer-, Legal-, Live-Business- oder finale öffentliche Produktfreigabe. Live-Verkauf und echte Bestellungen bleiben gesondert gesperrt.

Passende automatisierte Tests ausführen und tatsächliche Ergebnisse festhalten. Ein nicht durchgeführter Installationstest bleibt offen. Funktionstests nicht als unabhängiges „QA-PASS“ ausgeben. Die Draft-EULA sowie gegebenenfalls erforderliche Authenticode-/Clean-Windows-Nachweise bleiben eigenständige Grenzen.

## Kontrollierter Build- und Signierpfad

Die folgenden Werkzeuge gehören zum Anwendungs-/Operatorprojekt, **nicht zu diesem öffentlichen Kanalrepository**. Sie sind keine Endnutzeranleitung und ersetzen keine Freigabe.

1. Exakten Quellcommit festlegen; fachliche Regressionstests ausführen und in einem isolierten sauberen Checkout bauen.
2. Kompatiblen App-/Launcher-Maintenance-Payload mit `ops/setup/Build-LauncherMaintenance.ps1 -Version <version>` erzeugen.
3. Maintenance-Komponenten durch die autorisierte Operatorrolle mit `sign-launcher-maintenance-parent-version` signieren; Payload mit `Complete-LauncherMaintenancePayload.ps1` vervollständigen.
4. `Test-LauncherMaintenanceStartup.ps1` auf den konkreten Build anwenden.
5. Den kontrollierten Operatorbefehl ausführen:

   `Beydosh.OwnerDevelopment.TrustTool pack-remote <canonical-app-payload> <new-local-output-root> <version> <40-character-source-commit> <patch-notes-file>`

   Bei DLL-Aufruf wird die Operator-DLL über `dotnet` gestartet. Der feste Adapter bindet den autorisierten Release-Schlüssel, den Kanal und signed-plain-v2; er ist kein Freibrief für andere Rollen oder Ziele. Bereits existierende Ausgabewurzeln werden nicht überschrieben.

6. Inventar, Versions-/Commitmetadaten, unerwünschte Dateien, Schlüsselidentität und alle Signaturen/Hashes prüfen. Private Recovery-Schlüssel werden nicht verwendet.
7. Signiertes isoliertes Staging testen: Authentizität, Manipulationsablehnung, atomare Aktivierung, Receipt, Startbereitschaft und einschlägige Fehler-/Rollbackfälle. Erwartete PASS-Marker und Testanzahl verlangen, nicht nur Prozess-Exit 0.

`sign-base` für eingebettete lokale Pakete ist kein Ersatz für den Remote-v2-Build. Private Schlüssel bleiben außerhalb von Repository, Paketen und Logs. Keine Credentials, Kundendaten, Quellcodearchive oder Preview-/Testprogramme veröffentlichen.

## Kryptografischer Vertrag

Ausschließlich `beydosh-signed-plain-v2`: signiert und unverschlüsselt. Kein AES-Schlüssel, kein encrypted-v1-Fallback, kein unsigned-Fallback. NIST P-256 und SHA-256 werden mit gepinnter öffentlicher Vertrauensidentität kombiniert. Latest bindet die exakten signierten Manifestbytes per SHA-256; die vertrauenswürdige KeyId muss passen.

Jeder Transportchunk beginnt mit dem ASCII-Header:

`BUPD|2|signed-plain|<version>|<index>|<total>|`

Der Index ist nullbasiert, Dateinamen sind einsbasiert (`00001.bupd`). Archivbytes folgen dem Header. Transport- und Plain-Chunks bleiben auf jeweils höchstens 50 MiB begrenzt.

Das Manifest bindet Version, Release-ID, Quellcommit, UTC-Zeit, KeyId, MinimumLauncher, Plattform, PackageFormat, geordnete URLs, Plain-/Transportgrößen und -Hashes, Gesamtgrößen/-Hashes, exaktes Dateiinventar sowie Rollback-/Sicherheitsmetadaten. Der Gesamttransporthash bezieht sich auf die in Indexreihenfolge verketteten exakten Transportbytes.

Optionale signierte PatchNotes: höchstens 100 Klartextzeilen mit jeweils höchstens 1000 Zeichen, kein dynamisches HTML. Der echte Parser bleibt strikt; unbekannte Felder und inkompatible Dokumente werden abgelehnt. Die [Alt-Schemas](../schemas/README.md) und [Altvorlagen](../templates/UNPUBLISHED-NOT-A-RELEASE/README.md) sind keine v2-Validatoren.

## Unveränderliche Veröffentlichung, Latest zuletzt

1. Autorisierung, Quellcommit, Version, Tests, Build und lokale Signier-/Stagingnachweise festhalten.
2. Versions-/Tag-/Assetkollisionen ausschließen. Keine bereits veröffentlichten Bytes ersetzen.
3. Chunks unter Release-Tag `v<version>` hochladen. Im autorisierten Owner-Development-Pfad als Prerelease veröffentlichen; ein privater Draft-Link ist kein öffentlicher Verfügbarkeitsnachweis.
4. Pakete über ihre endgültigen URLs unter `https://github.com/CrystalxSLY/beydosh-updates/releases/download/v<version>/` herunterladen und Länge/Hashes gegen die signierten lokalen Bytes prüfen.
5. Das signierte Manifest unter `updates/stable/<version>/manifest.beydosh.json` committen; exakt veröffentlichte Bytes erneut herunterladen und prüfen.
6. Signierten Index gegen Manifest und aktuellen erwarteten Vorgänger prüfen. `updates/stable/latest.beydosh.json` **zuletzt** aktualisieren. Bei parallel geändertem Vorgänger stoppen und neu prüfen, nicht überschreiben.
7. Öffentlichen Index über den unveränderlichen Aktivierungscommit herunterladen und Byte-/Signaturbindung prüfen. Manifest-/Aktivierungscommits, Assetstatus und Hashes dokumentieren.
8. Einen ausdrücklich autorisierten realen Installationstest getrennt durchführen und protokollieren. Isoliertes Staging belegt nicht automatisch den Neustart einer konkreten Nutzerinstallation.

Fehler vor der Aktivierung lassen den bisherigen Latest unverändert. Ein Fehler nach Aktivierung erlaubt keinen stillen Indexrücksprung, kein Asset-Ersetzen und keinen Sicherheitsbypass.

## Wiederherstellung und Freigabegrenzen

Lokaler transaktionaler Rollback nach einem fehlgeschlagenen Start unterscheidet sich von einem veröffentlichten Remote-Downgrade. Recovery braucht eigene Autorisierung und muss Highest-Seen-/Anti-Replay-/Previous-Manifest-Regeln erfüllen. Das aktuelle 0.9.54-Manifest kennzeichnet Remote-Rollback als `blocked`; ein synthetischer Staging-Rollback ist damit nicht gleichzusetzen.

Die Trust-Bezeichnung `Production` wählt einen kryptografischen Verifier, keine fachliche oder rechtliche Freigabe. Owner-Schlüssel begründen keine vom lokalen Builder unabhängige Produktprovenienz und keine Authenticode-/SmartScreen-Reputation.

## Dokumentationsänderungen

Nur Markdown ändern, relative Links und Versionsangaben prüfen und die Unverändertheit aller übrigen Dateien nachweisen. Keine Versionsanhebung, Neuunterzeichnung, Tags, Release-Assets oder Latest-Änderung allein für Dokumentation. Historische Berichte behalten ihren zeitlichen Geltungsbereich.
