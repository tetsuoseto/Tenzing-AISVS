# C1 Schulungsdatenverwaltung und Bias-Management

## Kontrollziel

Trainingsdaten müssen so beschafft, gehandhabt und gepflegt werden, dass Herkunft, Sicherheit, Qualität und Fairness gewahrt bleiben. Dies erfüllt gesetzliche Verpflichtungen und verringert Risiken von Verzerrungen, Manipulationen oder Datenschutzverletzungen, die den gesamten KI-Lebenszyklus beeinträchtigen könnten.

---

## C1.1 Herkunft der Trainingsdaten

Führen Sie ein überprüfbares Inventar aller Datensätze, akzeptieren Sie nur vertrauenswürdige Quellen und protokollieren Sie jede Änderung zur Prüfungsnachvollziehbarkeit.

|   #   | Beschreibung                                                                                                                                                                                                               | Ebene | Rolle |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 1.1.1 | Stellen Sie sicher, dass ein aktuelles Inventar jeder Trainingsdatenquelle (Herkunft, verantwortliche Partei, Lizenz, Erfassungsmethode, Einschränkungen der geplanten Verwendung und Verarbeitungshistorie) geführt wird. |   1   |  D/V  |
| 1.1.2 | Stellen Sie sicher, dass die Trainingsdatenprozesse unnötige Merkmale, Attribute oder Felder ausschließen (z. B. nicht verwendete Metadaten, sensible personenbezogene Daten, durchgesickerte Testdaten).                  |   1   |  D/V  |
| 1.1.3 | Stellen Sie sicher, dass alle Änderungen am Datensatz einem protokollierten Genehmigungsworkflow unterliegen.                                                                                                              |   1   |  D/V  |
| 1.1.4 | Überprüfen Sie, ob Datensätze oder Teilmengen, wo möglich, mit Wasserzeichen versehen oder mit Fingerabdrücken gekennzeichnet sind.                                                                                        |   3   |  D/V  |

---

## C1.2 Sicherheit und Integrität der Trainingsdaten

Beschränken Sie den Zugriff auf Trainingsdaten, verschlüsseln Sie diese im Ruhezustand und während der Übertragung und überprüfen Sie deren Integrität, um Manipulation, Diebstahl oder Datenvergiftung zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                               | Ebene | Rolle |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 1.2.1 | Überprüfen Sie, ob Zugriffskontrollen den Speicherort der Trainingsdaten und die Verarbeitungspipelines schützen.                                                                                          |   1   |  D/V  |
| 1.2.2 | Stellen Sie sicher, dass jeder Zugriff auf Trainingsdaten protokolliert wird, einschließlich Benutzer, Zeit und Aktion.                                                                                    |   1   |  D/V  |
| 1.2.3 | Stellen Sie sicher, dass Trainingsdatensätze während der Übertragung und im Ruhezustand mithilfe der derzeit empfohlenen kryptografischen Algorithmen und Schlüsselverwaltungsmethoden verschlüsselt sind. |   1   |  D/V  |
| 1.2.4 | Verifizieren Sie, dass kryptographische Hashes oder digitale Signaturen verwendet werden, um die Datenintegrität während der Speicherung und Übertragung von Trainingsdaten sicherzustellen.               |   2   |  D/V  |
| 1.2.5 | Überprüfen Sie, dass eine automatisierte Integritätsüberwachung angewendet wird, um unbefugte Änderungen oder Beschädigungen der Trainingsdaten zu verhindern.                                             |   2   |  D/V  |
| 1.2.6 | Überprüfen Sie, dass veraltete Trainingsdaten sicher gelöscht oder anonymisiert werden.                                                                                                                    |   1   |  D/V  |
| 1.2.7 | Stellen Sie sicher, dass alle Versionen des Trainingsdatensatzes eindeutig identifiziert, unveränderlich gespeichert und prüfbar sind, um Rücksetzungen und forensische Analysen zu unterstützen.          |   3   |  D/V  |

---

## C1.3 Sicherheit bei der Datenkennzeichnung und Annotation

Stellen Sie sicher, dass Kennzeichnungs- und Annotationsprozesse zugangskontrolliert, prüfbar sind und sensible Informationen schützen.

|   #   | Beschreibung                                                                                                                                                                                    | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 1.3.1 | Stellen Sie sicher, dass Beschriftungsschnittstellen und -plattformen Zugriffskontrollen durchsetzen und Prüfprotokolle aller Beschriftungsaktivitäten führen.                                  |   1   |  D/V  |
| 1.3.2 | Überprüfen Sie, dass kryptografische Hashes oder digitale Signaturen auf Kennzeichnungsartefakte und Annotationsdaten angewendet werden, um deren Integrität und Authentizität sicherzustellen. |   2   |  D/V  |
| 1.3.3 | Verifizieren Sie, dass Labeling-Audit-Logs manipulationssicher sind und dass Labeling-Plattformen vor unbefugten Änderungen schützen.                                                           |   2   |  D/V  |
| 1.3.4 | Stellen Sie sicher, dass sensible Informationen in Bezeichnungen im Ruhezustand und während der Übertragung mit geeigneter Granularität geschwärzt, anonymisiert oder verschlüsselt werden.     |   2   |  D/V  |

---

## C1.4 Trainingsdatenqualität und Sicherheitsgarantie

Kombinieren Sie automatisierte Validierung, manuelle Stichprobenkontrollen und protokollierte Korrekturmaßnahmen, um die Zuverlässigkeit des Datensatzes zu gewährleisten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                          | Ebene | Rolle |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 1.4.1 | Stellen Sie sicher, dass automatisierte Tests Formatfehler und Nullwerte bei jedem Import oder jeder bedeutenden Datenumwandlung erfassen.                                                                                                                                                                                                            |   1   |   D   |
| 1.4.2 | Stellen Sie sicher, dass Trainings- und Feinabstimmungs-Pipelines Techniken zur Validierung der Datenintegrität und zur Erkennung von Datenvergiftungen implementieren (z. B. statistische Analyse, Ausreißererkennung, Embedding-Analyse), um potenzielle Datenvergiftungen oder unbeabsichtigte Korruption in den Trainingsdaten zu identifizieren. |   2   |  D/V  |
| 1.4.3 | Stellen Sie sicher, dass automatisch generierte Labels (z. B. durch Modelle oder schwache Aufsicht) Konfidenzschwellen und Konsistenzprüfungen unterliegen, um irreführende oder Labels mit geringer Konfidenz zu erkennen.                                                                                                                           |   2   |  D/V  |
| 1.4.4 | Stellen Sie sicher, dass geeignete Schutzmaßnahmen wie adversariales Training, Datenaugmentation mit gestörten Eingaben oder robuste Optimierungstechniken implementiert und entsprechend der Risikobewertung für relevante Modelle abgestimmt sind.                                                                                                  |   3   |  D/V  |
| 1.4.5 | Stellen Sie sicher, dass automatisierte Tests bei jeder Datenaufnahme oder wesentlichen Datenumwandlung Label-Skews erkennen.                                                                                                                                                                                                                         |   2   |   D   |

---

## C1.5 Datenherkunft und Rückverfolgbarkeit

Verfolgen Sie den gesamten Weg jedes Datensatzes von der Quelle bis zur Modellein­gabe zur Nachvollziehbarkeit und für die Vorfallsreaktion.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                      | Ebene | Rolle |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 1.5.1 | Überprüfen Sie, dass die Herkunft jedes Datensatzes und seiner Komponenten, einschließlich aller Transformationen, Erweiterungen und Zusammenführungen, dokumentiert ist und rekonstruiert werden kann.                                                                                           |   1   |  D/V  |
| 1.5.2 | Überprüfen Sie, dass Abstammungsdaten unveränderlich, sicher gespeichert und für Prüfungen zugänglich sind.                                                                                                                                                                                       |   2   |  D/V  |
| 1.5.3 | Stellen Sie sicher, dass die Verfolgung der Herkunft auch synthetische Daten abdeckt, die durch Augmentierung, Synthese oder datenschutzfreundliche Techniken erzeugt wurden, und dass alle synthetischen Daten im gesamten Prozess klar gekennzeichnet und von echten Daten unterscheidbar sind. |   2   |  D/V  |

---

## Literaturverzeichnis

* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
* [EU AI Act – Article 10: Data & Data Governance](https://artificialintelligenceact.eu/article/10/)
* [CISA Advisory: Securing Data for AI Systems](https://www.cisa.gov/news-events/cybersecurity-advisories/aa25-142a)
* [OpenAI Privacy Center – Data Deletion Controls](https://privacy.openai.com/policies?modal=take-control)

