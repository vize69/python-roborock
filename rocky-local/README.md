# Rocky Local 0.1.0

Eigene Roborock-Integration fuer Home Assistant Core **2026.10.0b3**.
Status: gebaut und lokal geprueft, noch nicht auf dem Zielsystem installiert oder live getestet.

## Korrekturen

- Neuester Reinigungseintrag anhand des groessten Zeitstempels statt Listenposition.
- Custom-Reinigungsmodus bei unterstuetzter Wasser-Schieberegler-Funktion.
- Wasser-Schieberegler: Lesewerte 221–250 und passende Schreibcodes.

Die Integration ist eine Kopie aus Home Assistant 2026.10.0b3 mit eigener Versionsnummer und festgelegter Bibliothek. Domain und Entity-IDs bleiben gleich; keine neue Anmeldung vorgesehen. Deutsche und englische Uebersetzungen stammen aus dem offiziellen HA-Wheel derselben Version. Der bestehende Dashboard-Code wird nicht bearbeitet.

Bibliothek: python-roborock 7.12.1+rocky.1, unveraenderlicher Commit:
https://github.com/vize69/python-roborock/commit/0aeaa40ad8093ca535fe0630c9aa2a16286adc84

## Installation

`install-rocky.sh` enthaelt alle Integrationsdateien samt SHA256-Pruefung.
Im Terminal-&-SSH-Add-on ausfuehren (kein Docker-Zugriff erforderlich):

```bash
bash /config/exchange/install-rocky-0.1.0.sh --check
bash /config/exchange/install-rocky-0.1.0.sh --apply
```

Vorher das Skript aus diesem Paket nach `/config/exchange/install-rocky-0.1.0.sh` kopieren oder den veroeffentlichten GitHub-Download verwenden. Das Skript bricht bei einer anderen HA-Version, einer bestehenden fremden Custom-Integration oder konkurrierenden Bibliotheksanforderungen ab. Bei fehlerhaftem `ha core check` wird die neu installierte Integration entfernt. Es fuehrt keinen Neustart aus.

Nach erfolgreichem Einbau ist ein separat freizugebender HA-Neustart notwendig. Danach Reinigungsmodus, letzte Reinigung und Logs pruefen. Erst dann ist die Live-Funktion bestaetigt.

## Rueckweg

```bash
bash /config/exchange/install-rocky-0.1.0.sh --rollback
```

Verschiebt die unveraenderte eigene Integration nach `exchange/rocky-disabled.*`, prueft die Konfiguration und laesst HA unangetastet weiterlaufen. Nach einem separaten Neustart greift wieder die offizielle Integration samt ihrer Bibliotheksanforderung. Kontodaten und Entity-Registry werden nicht bearbeitet.

## Pruefung und Grenzen

- Gesamte Bibliothek: 1521 Tests bestanden, 11 abgewählt, 53 erwartete Fehlschlaege, 96 Snapshots bestanden.
- Nach letzter typkompatibler Anpassung: 131 Status-Tests bestanden, alle Pre-commit-Pruefungen einschliesslich Mypy bestanden.
- Installation der Bibliothek vom festgelegten GitHub-Archiv in frischer Umgebung erfolgreich.
- Integrationssyntax mit Python 3.14 geprueft; unveraenderte Python-Quelldateien mit offiziellem HA-Wheel verglichen.
- Installer: Vorpruefung, Installation, wiederholter Aufruf, Rueckweg, Konfigurationsfehler und Konflikte mit simuliertem HA getestet.
- Kein Live-Test auf dem Roboter; kein Reinigungsbefehl ausgefuehrt.

Die Dateien bleiben bei HA-Updates erhalten. Kompatibilitaet mit zukuenftigen HA-Versionen ist damit nicht garantiert: diese Kopie muss bei Bedarf gepflegt werden. Keine automatische HACS-Aktualisierung eingerichtet. Die offizielle Integration wird erst nach Entfernung dieser Kopie wieder verwendet.

Home-Assistant-Quellcode: Apache-2.0, siehe LICENSE-Home-Assistant. Bibliothek: Lizenz im verlinkten Repository. Dieses Paket enthaelt keine Kontodaten, Schluessel oder privaten Roboterdiagnosen.
