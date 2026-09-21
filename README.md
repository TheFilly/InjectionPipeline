# Skalierbare Pipeline zum Einfügen vertraulicher Informationen in medizinische Dokumente

Diese README dokumentiert das Softwarepaket entsprechend der Checkliste
„Dokumentation von Daten & Code in Abschlussarbeiten“.

## Kurzbeschreibung

- **Autor:** Philipp Till
- **Betreuer:** Prof. Dr. Martin Spott, Anja Hirsch
- **Abschlussarbeit:** *Skalierbare Pipeline zum Einfügen vertraulicher Informationen in medizinische Dokumente*, Wirtschaftsinformatik
- **Softwarepaket / Version:** `injection-pipeline-release`, Version `0.1.0`
- **Veröffentlichungsdatum:** 21.09.2026
- **Identifier:** kein DOI oder anderer öffentlicher Identifier vorhanden
- **Untersuchungsgegenstand und Ziel:** Entwicklung und technische Verifikation einer Pipeline, die kontrollierte synthetische personenbezogene Informationen in bereits anonymisierte medizinische Dokumente einfügt. Die erzeugten Dokumente werden zusammen mit maschinenlesbaren Ground-Truth-Artefakten gespeichert. Die Pipeline ist kein De-Identifikationsverfahren.

## 1. Datensatz und Softwarepaket (Was?)

- **Datenarten:** Die Pipeline verarbeitet DICOM-, JPG/JPEG- und PDF-Dateien. Sie erzeugt injizierte Dokumente, Vorschaubilder, JSON-Run-Manifeste, Ground-Truth- beziehungsweise PDF-Annotationsdateien sowie PDF-Ausgaben. Die Testfälle erzeugen synthetische DICOM- und JPG-Fixtures zur Laufzeit.
- **Software und Zweck:** Das Python-Paket plant und führt kontrollierte Injektionen aus. Je nach Dokumenttyp werden synthetische Werte als sichtbare Pixel beziehungsweise Text oder als DICOM-Metadaten eingefügt. Die Positionen und die Zuordnung zu den Eingaben werden separat dokumentiert.
- **Sprache(n):** Python 3.13 oder neuer; JSON für Konfigurationen und Annotationen; Markdown für die Dokumentation. Die sichtbaren Testtexte sind schema- und testspezifisch und bilden kein festes Sprachkorpus.
- **Wissenschaftliche Methode:** Konstruktive Softwareentwicklung mit prototypischer Implementierung und testbasierter technischer Verifikation anhand synthetischer Fixtures. Eine eigene Primärdatenerhebung oder statistische Datenerhebung fand nicht statt.
- **Datenerhebung:** Keine Umfrage und keine sonstige eigene Primärdatenerhebung. Verwendet werden lokal bereitgestellte, bereits anonymisierte Eingabedokumente sowie synthetisch erzeugte Testdokumente und Testwerte. Die lokalen Eingabedaten sind nicht Teil dieses Release-Pakets.
- **Verarbeitung:** Eingaben werden formatbezogen geladen und validiert. Ein externes JSON-Identifier-Schema steuert die synthetische Identität und die möglichen DICOM-Routen. Anschließend werden sichtbare Injektionen und, sofern vorgesehen, DICOM-Tags geschrieben. Für jeden Lauf werden die Ausgabe und ein separates, versioniertes Ground-Truth-Artefakt erzeugt.

## 2. Datenursprung und Rechte (Wer?)

- **Autor / Erzeuger:** Philipp Till; Test-Fixtures und Laufzeitartefakte werden durch die Pipeline erzeugt.
- **Datenursprung:** Kombination aus synthetisch erzeugten Testdaten und lokal bereitgestellten, bereits anonymisierten Eingabedokumenten. Es wird kein eigener Forschungsdatensatz veröffentlicht.
- **Herkunft und Quellenreferenzen:** Die technische Herkunft und die Dateistruktur sind in [`docs/README.md`](docs/README.md) und [`docs/dicom-injection.md`](docs/dicom-injection.md) beschrieben. Lokale Eingabedaten, erzeugte Run-Ausgaben, Modellgewichte und Zugangsdaten gehören nicht zum Release.
- **Datenlizenz:** Für die im Release enthaltenen synthetischen Test-Fixtures nicht zutreffend. Rechte und Nutzungsbedingungen externer oder lokal bereitgestellter Eingabedaten bleiben bei deren jeweiligen Quellen.
- **Identifier:** nicht vorhanden; kein DOI.
- **Urheber- und sonstige Schutzrechte:** Der eigene Code und die eigene Dokumentation stammen aus dem Projekt von Philipp Till. Abhängigkeiten sowie gegebenenfalls verwendeter Drittcode, Handschrift-Quellcode und Modellgewichte unterliegen den jeweiligen Bedingungen ihrer Urheber. Echte Patientendaten werden nicht mit diesem Paket veröffentlicht.

## 3. Zeitraum (Wann?)

| Arbeitsschritt | Zeitraum |
| --- | --- |
| Datenbezug / Datengrundlage | Kein eigener Erhebungszeitraum; lokale anonymisierte Eingaben und synthetische Test-Fixtures wurden während der Entwicklung verwendet. |
| Datenbereinigung und -aufbereitung | Nicht zutreffend als separate Datensatzaufbereitung; Eingaben werden vor der Verarbeitung formatbezogen validiert. |
| Datenanalyse / Evaluation | Während der Entwicklungsphase durch Tests, Artefaktprüfungen und technische Validierung. |
| Softwareentwicklung | 16.04.2026 bis 18.09.2026; Veröffentlichung des dokumentierten Stands am 21.09.2026. |

## 4. Datenformate und -größe (Welche? Wie viel?)

Es gibt keinen festen Forschungsdatensatz und daher keine feste Datensatzgröße.
Die Größe der Laufzeitartefakte hängt von Eingabedokument, Seed und
Ausgabeformat ab.

| Daten / Artefakt | Format | Größe / Anzahl | Beschreibung |
| --- | --- | --- | --- |
| Eingabedokumente | `.dcm`, `.jpg`, `.jpeg`, `.pdf` | Laufabhängig; nicht im Release enthalten | Bereits anonymisierte lokale Dokumente beziehungsweise PDF-Vorlagen |
| Konfigurationen | `.json` | 2 versionierte Dateien im Release | Identifier-Schema und Evaluationskonfiguration |
| Injizierte Dokumente und Vorschauen | `.dcm`, `.jpg`, `.png`, `.pdf` | Laufabhängig | Ausgaben eines Pipeline-Laufs |
| Ground Truth und Run-Metadaten | `.json` | Je nach Lauf mehrere Sidecar-Dateien | Positionen, Werte, Zuordnungen, Schema- und Laufmetadaten |
| Test-Fixtures | synthetisch, zur Laufzeit erzeugt | Kein dauerhafter Datensatz | DICOM-/JPG-Fixtures für Unit- und Integrationstests |

## 5. Werkzeuge

| Werkzeug | Zweck | Version | Referenz |
| --- | --- | --- | --- |
| Python | Laufzeit und Implementierung | `>= 3.13` | [`pyproject.toml`](pyproject.toml) |
| `uv` | Abhängigkeiten und virtuelle Umgebung | über `uv.lock` festgelegt | [`docs/README.md`](docs/README.md) |
| Pydantic | Datenmodelle und Validierung | `>= 2.0` | [`pyproject.toml`](pyproject.toml) |
| pydicom | Lesen und Schreiben von DICOM | `>= 2.4` | [`pyproject.toml`](pyproject.toml) |
| ReportLab und pypdf | Erzeugung und Zusammenführung von PDF-Ausgaben | `>= 4.0` / `>= 5.0` | [`pyproject.toml`](pyproject.toml) |
| matplotlib | Erzeugung von Vorschaubildern und Visualisierungen | `>= 3.10.8` | [`pyproject.toml`](pyproject.toml) |
| Faker | Erzeugung synthetischer Identitätswerte | `>= 25.0` | [`pyproject.toml`](pyproject.toml) |
| pytest, pytest-cov | Unit-/Integrationstests und Coverage | `>= 8.0` / `>= 5.0` | [`pyproject.toml`](pyproject.toml) |
| ruff und mypy | Linting, Formatierung und statische Typprüfung | `>= 0.4` / `>= 1.10` | [`pyproject.toml`](pyproject.toml) |

## 6. Qualitätssicherung

- Pydantic-Modelle, Schema-Versionen und formatbezogene Loader/Writer prüfen die Eingaben und erzeugten Artefakte.
- Unit- und Integrationstests decken die DICOM-, JPG- und PDF-Pfade sowie die Ground-Truth-Erzeugung ab. Synthetische End-to-End-Fixtures ermöglichen wiederholbare Tests ohne reale Patientendaten.
- `ruff`, `mypy` im Strict-Modus und die pytest-Suite werden als technische Qualitätssicherung verwendet.
- Feste Seeds und feste Zeitstempel werden für Reproduzierbarkeits- und Artefaktprüfungen eingesetzt. Zusätzlich sind manuelle visuelle Prüfungen für ausgewählte Ausgaben vorgesehen.

## 7. Datenschutz und Schutzrechte

- **Sensible oder personenbezogene Daten:** Im Release nein. Die Pipeline ist für bereits anonymisierte Eingabedokumente vorgesehen und erzeugt ausschließlich synthetische personenbezogene Werte. Lokale Eingabedaten werden nicht mitgeliefert.
- **Einwilligungen:** Nicht zutreffend, da keine eigenen Personen befragt oder personenbezogene Primärdaten erhoben wurden.
- **Pseudo- bzw. Anonymisierungsmaßnahmen:** Eingabedokumente müssen vor der Verarbeitung bereits anonymisiert sein. Die Pipeline selbst ist kein Anonymisierungswerkzeug; sie injiziert kontrollierte synthetische Werte.
- **Umgang mit Zugangsbeschränkungen:** Lokale Eingaben, lokale Ausgaben, Modellgewichte und sonstige nicht versionierte Artefakte verbleiben in geschützten Arbeitsverzeichnissen. Das Release enthält nur Code, Konfiguration, Tests und Dokumentation.
- **Urheberrechte und weitere Schutzrechte:** Für Drittanbieter-Abhängigkeiten und gegebenenfalls verwendete externe Handschriftkomponenten gelten deren jeweilige Lizenzen.
- **Relevante Richtlinien / Referenzen:** Projektregeln in [`AGENTS.md`](../Masterarbeit/AGENTS.md), technische Dokumentation in [`docs/README.md`](docs/README.md) und [`docs/dicom-injection.md`](docs/dicom-injection.md) sowie die Checkliste „Dokumentation von Daten & Code in Abschlussarbeiten“.

## 8. Ablageort, Zugriff und Veröffentlichung

### Während des Projekts

- **Ordnerstruktur:** `src/` enthält den Paketcode, `tests/` die Tests, `configs/` Konfigurationen, `docs/` technische Dokumentation, `tools/` Hilfsprogramme. `DicomData/`, `output/` und `thesis-results/` enthalten lokale Arbeitsdaten und werden nicht als Release-Daten geführt.
- **Dateibenennungskonvention:** Laufartefakte werden unter `output/<run-id>/` abgelegt. Typische Dateien sind `*_injected.dcm` beziehungsweise `*_injected.jpg`, `ground_truth.json`, `run_manifest.json`, `preview.png` und `preview_annotated.png`. PDF-Ausgaben folgen der in [`docs/dicom-injection.md`](docs/dicom-injection.md) beschriebenen Struktur.
- **Versionierung:** Der Entwicklungscode wird mit Git versioniert; die Python-Abhängigkeiten werden zusätzlich über `uv.lock` festgehalten. Der Release-Stand ist in `pyproject.toml` als Version `0.1.0` gekennzeichnet.
- **Backup-Strategie:** Der versionierte Code wird über das Git-Repository und dessen Remote gesichert. Lokale Eingabedaten und erzeugte Ausgaben sind nicht Bestandteil des automatisierten Releases und müssen bei weiterem Aufbewahrungsbedarf separat gesichert werden.
- **Zugriffsberechtigte Personen:** Auf lokale Eingabedaten und nicht veröffentlichte Ausgaben erhalten nur autorisierte Projektbeteiligte Zugriff. Der Release enthält keine solchen Daten.

### Nach dem Projektende

- **Repository / Archiv:** Der Entwicklungscode liegt im Git-Projekt `Masterarbeit`; der dokumentierte Release-Stand liegt im Verzeichnis `injection-pipeline-release/`. Ein DOI-Archiv ist nicht vorhanden.
- **Zugriffsvoraussetzungen:** Python `>= 3.13` und `uv`; anschließend `uv sync --extra dev`. Für lokale Eingaben oder die optionale Handschriftverarbeitung sind zusätzliche, nicht mitgelieferte Dateien beziehungsweise Laufzeitvoraussetzungen erforderlich.
- **Veröffentlichte Bestandteile:** Python-Code, Tests, Konfigurationen, technische Dokumentation und die zugehörige Dependency-Sperrdatei. Keine realen Patientendaten, lokalen Eingabedateien, Laufzeitausgaben, Secrets oder Modellgewichte.
- **Alternative Ablageorte:** Keine weiteren veröffentlichten Ablageorte dokumentiert. Die lokale Arbeitskopie und nicht versionierte Eingabedaten werden getrennt vom Release aufbewahrt.
- **Aufbewahrungsdauer:** Für Code und Dokumentation ist eine dauerhafte Aufbewahrung im Git-Projekt vorgesehen, soweit das Repository weitergeführt wird. Für lokale Eingabedaten gelten die jeweils vereinbarten Projekt- und Datenschutzvorgaben.
- **Löschdatum:** Für Code und Dokumentation nicht vorgesehen. Nicht versionierte lokale Daten werden gelöscht, sobald ihre projektbezogene Aufbewahrung nicht mehr erforderlich ist.
