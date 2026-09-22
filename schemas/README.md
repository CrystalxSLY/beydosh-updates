# Historische JSON-Schemas

Die beiden JSON-Schemas in diesem Verzeichnis stammen aus dem früheren **encrypted-v1**-Vertrag. Sie werden aus historischen Gründen aufbewahrt und sind **keine Validatoren für den aktuell verwendeten signed-plain-v2-Kanal**.

Eine erfolgreiche Prüfung gegen diese Altdateien belegt weder v2-Kompatibilität noch eine gültige Signatur. Der ausgelieferte strikte Client-Parser und seine Tests sind maßgeblich. Unknown Fields und inkompatible Dokumente werden nicht durch ein großzügigeres Schema zulässig.

Eine technische Migration der Schemas muss gesondert implementiert und gegen den echten Parser geprüft werden. Das aktuelle Dokumentationsupdate verändert die JSON-Dateien nicht.

[Update-Vertrag und Veröffentlichung](../docs/PUBLISHING.md) · [Nicht veröffentlichbare Vorlagen](../templates/UNPUBLISHED-NOT-A-RELEASE/README.md)
