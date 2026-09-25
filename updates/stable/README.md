# Signierter Kanal: stable

[Übersicht](../../README.md) · [Veröffentlichungsverfahren](../../docs/PUBLISHING.md)

Dokumentationsstand 25.09.2026: **0.9.64** ist aktiviert. `stable` ist eine technische Kanalkennung, keine öffentliche Produkt- oder Live-Freigabe. Die Veröffentlichung ist eine Beta/Owner-Development-Vorabversion.

## Aufbau

- [latest.beydosh.json](latest.beydosh.json): signierter, veränderlicher Kanalindex.
- `<version>/manifest.beydosh.json`: unveränderliches signiertes Versionsmanifest.
- GitHub-Release `v<version>`: unveränderliche `00001.bupd` und gegebenenfalls weitere Transportchunks.

Der Index bindet die Manifestbytes per SHA-256. Das Manifest bindet Paket-URLs, Größen, Hashes, Inventar und Kompatibilität. Paketformat: `beydosh-signed-plain-v2`. Pakete und Manifest müssen öffentlich erreichbar und geprüft sein, bevor Latest zuletzt aktiviert wird. Bestehende Versionsinhalte werden nicht ersetzt.

## Aktueller dokumentierter Stand

- Version: 0.9.64
- MinimumLauncher: 0.9.0
- Plattform: Windows/x64, .NET 9 Desktop Runtime erforderlich
- SourceCommit: `d0c3c0d6c4e087cb5e0d2d8bad86d4a7338bc403`
- Manifest-SHA-256: `B84E6CF48A9F026ED27C79B84E77319A3C054091C344FFF31D48ED79FC7E4898`
- Aktivierung: [7b9e100](https://github.com/CrystalxSLY/beydosh-updates/commit/7b9e100f68f7c514e09c72b313a13f0bb7204cbd)
- [Veröffentlichungsnachweis und Testgrenzen](../../docs/releases/0.9.64-publication.md)

Diese Angaben sind ein Schnappschuss; der verifizierte Live-Index bleibt maßgeblich. Fehlender Index bedeutet nicht „aktuell“. Netzfehler oder ungültige Signaturen sind kein erfolgreicher Versionsvergleich. Dokumentationsänderungen verändern den signierten Kanal nicht.
