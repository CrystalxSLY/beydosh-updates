# Unveröffentlichte Altvorlagen – kein Release

[Übersicht](../../README.md) · [Veröffentlichungsverfahren](../../docs/PUBLISHING.md)

Die JSON-Dateien in diesem Ordner sind historische **encrypted-v1-Platzhalter**, keine gültigen signed-plain-v2-Dokumente. Sie enthalten unter anderem `UNPUBLISHED_TEMPLATE_ONLY` und Platzhalterwerte. Nicht nach `updates/stable/` kopieren, nicht unverändert signieren und nicht als Release-Metadaten hochladen.

Auch die vorhandenen JSON-Schemas unter `schemas/` sind keine autoritativen v2-Validatoren. Maßgeblich sind der tatsächlich ausgelieferte strikte Parser, seine Tests und der kontrollierte v2-Builder. Vorlagen/Schema müssten vor einer technischen Wiederverwendung ausdrücklich migriert und gegen diesen Vertrag getestet werden.

Reale Metadaten erzeugt der kontrollierte Offline-Release-Builder; sie werden mit der autorisierten extern gehaltenen Release-Schlüsselrolle signiert und vor der Aktivierung erneut geprüft. Diese Dokumentation ändert keine Vorlagen, Signaturen oder Live-Update-Dateien.
