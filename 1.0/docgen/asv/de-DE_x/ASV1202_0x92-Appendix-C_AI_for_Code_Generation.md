# Anhang C: KI-unterstütztes Secure Coding

## Ziel

Dieses Kapitel definiert grundlegende organisatorische Kontrollen für die sichere und effektive Nutzung von KI-unterstützten Codetools während der Softwareentwicklung und stellt dabei die Sicherheit und Nachvollziehbarkeit über den SDLC hinweg sicher.

---

## AC.1 KI-gestützter sicherer Codierungs-Workflow

Integrieren Sie KI-Tooling in den sicheren Softwareentwicklungslebenszyklus (SSDLC) der Organisation, ohne bestehende Sicherheitsfreigaben zu schwächen.

|   #    | Beschreibung                                                                                                                                                                     | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.1.1 | Überprüfen Sie, dass ein dokumentierter Workflow beschreibt, wann und wie KI-Tools Code generieren, refaktorisieren oder überprüfen dürfen.                                      |   1   |
| AC.1.2 | Verifizieren Sie, dass der Workflow jeder SSDLC-Phase zugeordnet ist (Design, Implementierung, Code-Review, Tests, Deployment).                                                  |   2   |
| AC.1.3 | Verifizieren Sie, dass Metriken (z.B. Schwachstellendichte, mittlere Zeit bis zur Erkennung) auf von KI erzeugtem Code erhoben und mit reinen Human-Baselines verglichen werden. |   3   |

---

## AC.2 KI-Tool-Qualifizierung & Threat Modeling

Stellen Sie sicher, dass KI-Programmierwerkzeuge hinsichtlich Sicherheitsfunktionen, Risiko und Auswirkungen auf die Lieferkette vor der Einführung bewertet werden.

|   #    | Beschreibung                                                                                                                                                                                                   | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.2.1 | Stellen Sie sicher, dass für jedes KI-Tool in einem Bedrohungsmodell Fehlanwendungen, Modell-Inversion, Datenabfluss und Risiken der Abhängigkeitshierarchie identifiziert werden.                             |   1   |
| AC.2.2 | Stellen Sie sicher, dass Tool-Bewertungen die statische/dynamische Analyse aller lokalen Komponenten sowie die Bewertung von SaaS-Endpunkten (TLS, Authentifizierung/Autorisierung, Protokollierung) umfassen. |   2   |
| AC.2.3 | Stellen Sie sicher, dass Bewertungen einem anerkannten Rahmen folgen und nach größeren Versionsänderungen erneut durchgeführt werden.                                                                          |   3   |

---

## AC.3 Sichere Prompt- & Kontextverwaltung

Verhindern Sie das Lecken von Geheimnissen, proprietärem Code und personenbezogenen Daten beim Erstellen von Prompts oder Kontexten für KI-Modelle.

|   #    | Beschreibung                                                                                                                                                                                                       | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| AC.3.1 | Überprüfen Sie, dass schriftliche Anweisungen das Senden von Geheimnissen, Zugangsdaten oder klassifizierten Daten in Prompts verbieten.                                                                           |   1   |
| AC.3.2 | Überprüfen Sie, dass technische Kontrollen (clientseitige Redaction, genehmigte Kontextfilter) automatisch sensible Artefakte entfernen.                                                                           |   2   |
| AC.3.3 | Stellen Sie sicher, dass Prompts und Antworten tokenisiert, während der Übertragung und im Ruhezustand verschlüsselt sind und dass die Aufbewahrungsfristen mit der Richtlinie zur Dateneinstufung übereinstimmen. |   3   |

---

## AC.4 Validierung von KI-generiertem Code

Erkennen und Beheben von Schwachstellen, die durch KI-Ausgaben eingeführt werden, bevor der Code zusammengeführt oder bereitgestellt wird.

|   #    | Beschreibung                                                                                                                                                                                               | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.4.1 | Stellen Sie sicher, dass von KI generierter Code immer einer menschlichen Codeüberprüfung unterliegt.                                                                                                      |   1   |
| AC.4.2 | Verifizieren Sie, dass automatisierte Scanner (SAST/IAST/DAST) bei jeder Pull Request mit durch KI generiertem Code ausgeführt werden und dass Zusammenführungen bei kritischen Befunden blockiert werden. |   2   |
| AC.4.3 | Verifizieren Sie, dass differentielles Fuzz-Testing oder eigenschaftsbasierte Tests sicherheitskritische Verhaltensweisen nachweisen (z. B. Eingabevalidierung, Autorisierungslogik).                      |   3   |

---

## AC.5 Erklärbarkeit & Nachverfolgbarkeit von Code-Vorschlägen

Stellen Sie Prüfern und Entwicklern Einblicke dafür bereit, warum eine Empfehlung abgegeben wurde und wie sie sich weiterentwickelt hat.

|   #    | Beschreibung                                                                                                                                                                                                                  | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.5.1 | Verifizieren, dass Prompt/Antwort-Paare mit Commit-IDs protokolliert werden.                                                                                                                                                  |   1   |
| AC.5.2 | Stellen Sie sicher, dass Entwickler Modellzitate (Trainingsausschnitte, Dokumentation) bereitstellen können, die eine Empfehlung stützen.                                                                                     |   2   |
| AC.5.3 | Stellen Sie sicher, dass Explainability-Berichte zusammen mit Design-Artefakten gespeichert und in Sicherheitsüberprüfungen referenziert werden, und dass damit die Traceability-Prinzipien von ISO/IEC 42001 erfüllt werden. |   3   |

---

## AC.6 Kontinuierliches Feedback & Modell-Feinabstimmung

Verbessern Sie die Modell-Sicherheitsleistung im Laufe der Zeit und verhindern Sie gleichzeitig negatives Drift.

|   #    | Beschreibung                                                                                                                                                                                                                                    | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.6.1 | Verifizieren Sie, dass Entwickler unsichere oder nicht konforme Vorschläge kennzeichnen können und dass Kennzeichnungen nachverfolgt werden.                                                                                                    |   1   |
| AC.6.2 | Stellen Sie sicher, dass aggregiertes Feedback periodisches Fine-Tuning oder retrieval-augmented generation mit validierten Secure-Coding-Korpora (z.B. OWASP Cheat Sheets) beeinflusst.                                                        |   2   |
| AC.6.3 | Stellen Sie sicher, dass eine geschlossene Evaluationsumgebung nach jedem Fine-Tuning Regressionstests ausführt; Sicherheitsmetriken müssen die bisherigen Benchmarks mindestens erreichen oder übertreffen, bevor eine Bereitstellung erfolgt. |   3   |

---

## AC.7 KI-generierte Infrastruktur- und Pipeline-Artefakte

Stellen Sie sicher, dass KI-generierte Infrastructure-as-Code (IaC), CI/CD-Workflows, Bereitstellungskonfigurationen und sicherheitspolitische Artefakte einer angemessenen Validierung und Governance unterliegen.

|   #    | Beschreibung                                                                                                                                                                                                                                  | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.7.1 | Verifizieren Sie, dass KI-generierte Infrastructure-as-Code, CI/CD-Workflows und Sicherheitsrichtlinien-Artefakte eindeutig identifiziert und nachverfolgt werden.                                                                            |   1   |
| AC.7.2 | Stellen Sie sicher, dass durch KI generierte Infrastructure- und Pipeline-Konfigurationen vor der Ausführung einer angemessenen Prüfung und Freigabe bedürfen.                                                                                |   2   |
| AC.7.3 | Stellen Sie sicher, dass KI-generierte Änderungen an Infrastruktur und Workflows einer Sicherheitsvalidierung, Konfigurationsprüfungen und einer Richtlinienerzwingung unterliegen, die mindestens genauso streng ist wie für Anwendungscode. |   3   |

---

## AC.8 Autonome-Agenten-Änderungssteuerungs-Einschränkungen

Stellen Sie sicher, dass autonome KI-Agenten, die an der Erstellung von Code oder Konfigurationen beteiligt sind, einer angemessenen Aufgabentrennung unterliegen und ihre eigenen Änderungen nicht unabhängig genehmigen oder bewerben können.

|   #    | Beschreibung                                                                                                                                                                                            | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.8.1 | Stellen Sie sicher, dass autonome Agenten keine Artefakte genehmigen, zusammenführen, signieren oder bereitstellen können, die sie selbst erzeugt haben.                                                |   1   |
| AC.8.2 | Überprüfen Sie, dass KI-Systeme mit abgegrenzten Identitäten und Berechtigungen arbeiten, die verhindern, dass generierte Artefakte über Umgebungen hinweg zur Selbstförderung weiterverbreitet werden. |   2   |
| AC.8.3 | Überprüfen Sie, dass die Aufgabentrennung zwischen den Phasen der Artefakterzeugung, der Überprüfung, der Genehmigung und der Bereitstellung für durch KI generierte Änderungen durchgesetzt wird.      |   3   |

---

## AC.9 Validierung der Herkunft von KI-Artefakten für die Bereitstellung

Stellen Sie sicher, dass Bereitstellungs- und Promotions-Pipelines die Herkunft und die Generierungshistorie von durch KI erzeugten Artefakten validieren, bevor sie befördert werden.

|   #    | Beschreibung                                                                                                                                                                                                          | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.9.1 | Stellen Sie sicher, dass KI-generierte Artefakte Herkunfts- und Erzeugungsmetadaten enthalten, die das KI-System identifizieren, das sie erzeugt hat, den Erzeugungskontext sowie zugehörige Prüfaufzeichnungen.      |   1   |
| AC.9.2 | Überprüfen Sie, dass Bereitstellungspipelines das Vorhandensein und die Integrität von Ursprungs- und Generierungsmetadaten für KI-generierte Artefakte vor der Freigabe validieren.                                  |   2   |
| AC.9.3 | Überprüfen Sie, dass Artefakte ohne erforderliche Angaben zur Herkunft und zur Generierung oder die von nicht vertrauenswürdigen KI-Systemen oder Umgebungen erzeugt wurden, bei der Bereitstellung abgelehnt werden. |   3   |

---

## AC.10 Vollständigkeit und Validierung des Generierungs-Audit-Trails

Stellen Sie sicher, dass KI-generierte Artefakte vollständige und konsistente Herkunfts- und Generierungsaufzeichnungen enthalten und dass diese Aufzeichnungen vor der Integration oder Bereitstellung validiert werden.

In der Praxis hängt die Durchsetzung auf Basis von Richtlinien von der Verfügbarkeit und Qualität von Ursprungs- und Erzeugungsnachweisen ab. Unvollständige oder inkonsistente Nachweise können dazu führen, dass Erkennungen übersehen werden oder es zu Durchsetzungslücken kommt. Diese Kontrollen stellen sicher, dass das Ursprungsverfolgen als eine erstklassige Anforderung behandelt und vor der Annahme des Artefakts validiert wird.

|    #    | Beschreibung                                                                                                                                                                                                        | Ebene |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| AC.10.1 | Stellen Sie sicher, dass KI-generierte Artefakte die erforderlichen Felder für Ursprung und Generierung enthalten (z.B. Modellidentität, Generierungskontext, menschliche Beteiligung und Sitzungsidentifikatoren). |   1   |
| AC.10.2 | Prüfen Sie, dass die Metadaten für Herkunft und Generierung auf Vollständigkeit und Konsistenz validiert werden (z.B. keine fehlenden oder mehrdeutigen Felder, normalisierte Darstellungen).                       |   2   |
| AC.10.3 | Überprüfen Sie, dass Artefakte mit unvollständigen, inkonsistenten oder nicht verifizierbaren Metadaten zur Herkunft und Generierung vor dem Zusammenführen oder der Bereitstellung abgewiesen werden.              |   3   |

---

## References

* [NIST AI Risk Management Framework 1.0](https://nvlpubs.nist.gov/nistpubs/ai/nist.ai.100-1.pdf)
* [ISO/IEC 42001:2023: AI Management Systems Requirements](https://www.iso.org/standard/81230.html)
* [OWASP Secure Coding Practices: Quick Reference Guide](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/)

