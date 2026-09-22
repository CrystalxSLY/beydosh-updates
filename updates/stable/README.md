# Signierter Kanal: stable

[Übersicht](../../README.md) · [Veröffentlichungsverfahren](../../docs/PUBLISHING.md)

Dokumentationsstand 22.09.2026: Der Kanal ist veröffentlicht und **0.9.54** ist aktiviert. Der Ordnername `stable` ist eine Kanalkennung, keine öffentliche Produkt-/Live-Freigabe; der aktuelle GitHub-Release ist ein Owner-Development-Prerelease.

## Aufbau

- [latest.beydosh.json](latest.beydosh.json): signierter, veränderlicher Kanalindex.
- `<version>/manifest.beydosh.json`: unveränderliches signiertes Versionsmanifest.
- GitHub-Release `v<version>`: unveränderliche `00001.bupd` und gegebenenfalls weitere Transportchunks.

Der Index bindet die exakten Manifestbytes per SHA-256. Das Manifest bindet Paket-URLs, Größen, Hashes, Inventar, Kompatibilität und weitere Sicherheitsmetadaten. Paketformat: `beydosh-signed-plain-v2`.

Neue Paket-URLs und das Manifest müssen erreichbar und geprüft sein, **bevor Latest zuletzt aktiviert wird**. Bestehende Versionsinhalte werden nicht ersetzt. Es gibt keine zweite manuell gepflegte Versionsliste als Update-Autorität.

## Aktueller dokumentierter Stand

- Version: 0.9.54
- MinimumLauncher: 0.9.0
- Plattform: Windows/x64
- SourceCommit: `c24d2eb6e80b7d889e7bd3a1a6f52bb56b91052f`
- Manifest-SHA-256: `69BDD8109454AEF8B8D9F2C9256CB75801DC16DA19ACD6684D91E59055D824F1`
- Aktivierung: [45d458a](https://github.com/CrystalxSLY/beydosh-updates/commit/45d458a306a12bd77b179f6dd5dc666cffad0bc8)

Diese Angaben sind ein dokumentierter Schnappschuss. Der verifizierte Live-Index bleibt maßgeblich. [Versionshistorie](../../docs/CHANGELOG.md) und [Veröffentlichungsnachweis](../../docs/releases/0.9.54-publication.md) erläutern Änderungen und Prüfgrenzen.

Fehlender Index bedeutet nicht „aktuell“; Netzfehler oder ungültige Signaturen dürfen nicht als erfolgreicher Versionsvergleich behandelt werden. Dokumentationsänderungen verändern den signierten Kanal nicht.
