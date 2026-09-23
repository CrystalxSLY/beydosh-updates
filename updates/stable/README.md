# Signierter Kanal: stable

[Übersicht](../../README.md) · [Veröffentlichungsverfahren](../../docs/PUBLISHING.md)

Dokumentationsstand 23.09.2026: Der Kanal ist veröffentlicht und **0.9.56** ist aktiviert. Der Ordnername `stable` ist eine Kanalkennung, keine öffentliche Produkt-/Live-Freigabe; der aktuelle GitHub-Release ist ein Owner-Development-Prerelease.

## Aufbau

- [latest.beydosh.json](latest.beydosh.json): signierter, veränderlicher Kanalindex.
- `<version>/manifest.beydosh.json`: unveränderliches signiertes Versionsmanifest.
- GitHub-Release `v<version>`: unveränderliche `00001.bupd` und gegebenenfalls weitere Transportchunks.

Der Index bindet die exakten Manifestbytes per SHA-256. Das Manifest bindet Paket-URLs, Größen, Hashes, Inventar, Kompatibilität und weitere Sicherheitsmetadaten. Paketformat: `beydosh-signed-plain-v2`.

Neue Paket-URLs und das Manifest müssen erreichbar und geprüft sein, **bevor Latest zuletzt aktiviert wird**. Bestehende Versionsinhalte werden nicht ersetzt. Es gibt keine zweite manuell gepflegte Versionsliste als Update-Autorität.

## Aktueller dokumentierter Stand

- Version: 0.9.56
- MinimumLauncher: 0.9.0
- Plattform: Windows/x64
- SourceCommit: `d0c4e29969bb9d89d704b6545c3e99dbd3318ee3`
- Manifest-SHA-256: `C1211BFA8367AAD1F4B3D1F6DD625AA4EB8DF89C5599860C9878E4C9EED736A8`
- Aktivierung: [6e4b05c](https://github.com/CrystalxSLY/beydosh-updates/commit/6e4b05c427c0edf689455a01513d17d64345e240)

Diese Angaben sind ein dokumentierter Schnappschuss. Der verifizierte Live-Index bleibt maßgeblich. [Versionshistorie](../../docs/CHANGELOG.md) und [Veröffentlichungsnachweis](../../docs/releases/0.9.56-publication.md) erläutern Änderungen und Prüfgrenzen.

Fehlender Index bedeutet nicht „aktuell“; Netzfehler oder ungültige Signaturen dürfen nicht als erfolgreicher Versionsvergleich behandelt werden. Dokumentationsänderungen verändern den signierten Kanal nicht.
