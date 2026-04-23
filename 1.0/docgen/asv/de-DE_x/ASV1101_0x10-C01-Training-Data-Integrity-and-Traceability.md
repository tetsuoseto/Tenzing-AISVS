# C1 Trainingsdaten-Integrität & Rückverfolgbarkeit

## Kontrollziel

Trainingsdaten müssen so beschafft, verarbeitet und gepflegt werden, dass Herkunfts- Nachverfolgbarkeit, Integrität und Qualität erhalten bleiben. Die zentrale Sicherheitsbedenke besteht darin, sicherzustellen, dass die Daten nicht manipuliert, vergiftet oder beschädigt wurden. sicherheitsrelevante Verzerrungen (z.B. unausgewogene Missbrauchserkennungs-Trainingsdaten, die Angreifern ermöglichen, Schutzmaßnahmen zu umgehen) werden als mögliche Folge kompromittierter oder nicht validierter Daten behandelt, nicht als eigenständige Kategorie von Kontrollen.

>Geltungsbereich-Notiz -- Bias. AISVS behandelt Bias nur dann, wenn dadurch ein Sicherheitsrisiko entsteht (z.B. Umgehung der Missbrauchserkennung, Authentifizierungs-Heuristiken oder automatisierte Vertrauensentscheidungen). Weitergehende Anforderungen an Governance hinsichtlich Fairness fallen nicht in den Geltungsbereich; siehe z.B. ISO/IEC 42001 oder das NIST AI RMF für allgemeine Leitlinien zu Fairness und Ethik.

>Scope note -- allgemeine Datensicherheit. Allgemeine Kontrolldetails zur Datensicherheit für Zugriffskontrolle, Protokollierung, Verschlüsselung im Ruhezustand und während der Übertragung sowie Datenaufbewahrung/-löschung werden durch ASVS v5 (V8, V11, V12, V14, V16) abgedeckt und gelten für die Speicherung von Trainingsdaten und Labeling-Systeme. Dieser Abschnitt stellt höhere Anforderungen mit Ebenen dar, die spezifisch für KI sind.

---

## C1.1 Herkunft der Trainingsdaten & Nachvollziehbarkeit

Behalten Sie ein überprüfbares Bestandsverzeichnis für alle Datensätze bei, akzeptieren Sie nur vertrauenswürdige Quellen und protokollieren Sie jede Änderung zur Nachvollziehbarkeit.

|   #   | Beschreibung                                                                                                                                                                                                                                                     | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.1.1 | Stellen Sie sicher, dass ein aktuelles Verzeichnis jeder Quelle der Trainingsdaten (Herkunft, verantwortliche Stelle, Lizenz, Sammelmethodik, beabsichtigte Nutzungsbeschränkungen und Verarbeitungshistorie) gepflegt und auf dem neuesten Stand gehalten wird. |   1   |
| 1.1.2 | Stellen Sie sicher, dass die Verarbeitung der Trainingsdaten unnötige Merkmale, Attribute oder Felder ausschließt (z.B. ungenutzte Metadaten, sensible personenbezogene Daten, geleakte Testdaten).                                                              |   1   |
| 1.1.3 | Stellen Sie sicher, dass alle Änderungen am Datensatz einem protokollierten Genehmigungs-Workflow unterliegen.                                                                                                                                                   |   1   |
| 1.1.4 | Überprüfen Sie, dass Datensätze oder Teilmengen, soweit möglich, mit einem Watermark- oder Fingerprinting-Verfahren versehen sind.                                                                                                                               |   3   |

---

## C1.2 Sicherheit & Integrität von Trainingsdaten

Schränken Sie den Zugriff auf Trainingsdaten ein, verschlüsseln Sie sie im Ruhezustand und während der Übertragung und validieren Sie ihre Integrität, um Manipulation, Diebstahl oder Datenvergiftung zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                         | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 1.2.1 | Überprüfen Sie, dass Zugriffskontrollen den Speicher von Trainingsdaten und die Pipelines schützen.                                                                                                                                  |   1   |
| 1.2.2 | Stellen Sie sicher, dass der gesamte Zugriff auf Trainingsdaten protokolliert wird, einschließlich Benutzer, Zeitpunkt und Aktion.                                                                                                   |   1   |
| 1.2.3 | Stellen Sie sicher, dass Trainingsdatensätze während der Übertragung und im Ruhezustand verschlüsselt sind, unter Verwendung aktueller empfohlener kryptografischer Algorithmen und bewährter Verfahren für das Schlüsselmanagement. |   1   |
| 1.2.4 | Verifizieren Sie, dass kryptografische Hashes oder digitale Signaturen verwendet werden, um die Datenintegrität während der Speicherung und Übertragung von Trainingsdaten sicherzustellen.                                          |   2   |
| 1.2.5 | Überprüfen Sie, dass automatisiertes Integritätsmonitoring angewendet wird, um unbefugte Änderungen oder eine Beschädigung der Trainingsdaten zu verhindern.                                                                         |   2   |
| 1.2.6 | Stellen Sie sicher, dass veraltete Trainingsdaten sicher gelöscht oder anonymisiert werden.                                                                                                                                          |   1   |
| 1.2.7 | Stellen Sie sicher, dass alle Versionen der Trainingsdaten eindeutig identifiziert, unveränderlich gespeichert und revisionsfähig sind, um Rollbacks und forensische Analysen zu unterstützen.                                       |   3   |

---

## C1.3 Datenerfassungs- und Annotationssicherheit

Stellen Sie sicher, dass Kennzeichnungs- und Annotierungsprozesse mit Zugriffskontrollen versehen und revisionssicher sowie nachvollziehbar sind.

|   #   | Beschreibung                                                                                                                                                                                                                                                                             | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.3.1 | Stellen Sie sicher, dass Kennzeichnungs-Interfaces und -Plattformen Zugriffskontrollen durchsetzen, die einschränken, wer Anmerkungen erstellen, ändern oder genehmigen kann.                                                                                                            |   1   |
| 1.3.2 | Stellen Sie sicher, dass alle Kennzeichnungsaktivitäten in Audit-Logs aufgezeichnet werden, einschließlich der Identität des Annotators, des Zeitstempels und der ausgeführten Aktion.                                                                                                   |   1   |
| 1.3.3 | Verifizieren Sie, dass Identitätsmetadaten der Annotatoren zusammen mit dem Datensatz exportiert und beibehalten werden, sodass jede Annotation oder jedes Präferenzpaar einem spezifischen, verifizierten menschlichen Annotator im gesamten Trainings-Workflow zugeordnet werden kann. |   1   |
| 1.3.4 | Stellen Sie sicher, dass kryptografische Hashes oder digitale Signaturen auf Labeling-Artifacts, Annotierungsdaten und Datensätze zum Fine-Tuning-Feedback (einschließlich RLHF-Präferenzpaaren) angewendet werden, um deren Integrität und Authentizität sicherzustellen.               |   2   |
| 1.3.5 | Stellen Sie sicher, dass vertrauliche Informationen in Bezeichnungen abgedeckt, anonymisiert oder verschlüsselt werden, unter Verwendung einer geeigneten Granularität im Ruhezustand und bei der Übertragung.                                                                           |   2   |

---

## C1.4 Trainingsdatenqualität und Sicherheitsabsicherung

Kombinieren Sie automatisierte Validierung, manuelle Stichprobenprüfungen und protokollierte Behebungsmaßnahmen, um die Datenbestandszuverlässigkeit zu gewährleisten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.4.1 | Überprüfen Sie, dass automatische Tests Formatfehler und Nullwerte bei jeder Ingestion oder jeder wesentlichen Datenumwandlung erfassen.                                                                                                                                                                                                                                                                                        |   1   |
| 1.4.2 | Überprüfen Sie, dass die Trainings- und Feinabstimmungs-Pipelines Validierungstechniken zur Sicherstellung der Datenintegrität und Techniken zur Erkennung von Poisoning implementieren (z.B. statistische Analyse, Outlier-Erkennung, Embedding-Analyse), um potenzielles Data-Poisoning oder unbeabsichtigte Datenkorruption in den Trainingsdaten zu identifizieren.                                                         |   2   |
| 1.4.3 | Stellen Sie sicher, dass automatisch generierte Bezeichnungen (z.B. über Modelle oder schwache Überwachung) Schwellenwerte für die Konfidenz und Konsistenzprüfungen unterliegen, um irreführende oder niedrigkonfidente Bezeichnungen zu erkennen.                                                                                                                                                                             |   2   |
| 1.4.4 | Stellen Sie sicher, dass geeignete Abwehrmaßnahmen, wie z.B. adversariales Training, Datenaugmentation mit pertubierten Eingaben oder Techniken der robusten Optimierung, für relevante Modelle auf Grundlage der Risikobewertung implementiert und abgestimmt sind.                                                                                                                                                            |   3   |
| 1.4.5 | Stellen Sie sicher, dass automatisierte Tests Label-Skews bei jeder Ingestion oder jeder signifikanten Datenumwandlung erkennen.                                                                                                                                                                                                                                                                                                |   2   |
| 1.4.6 | Verifizieren Sie, dass Modelle, die in sicherheitsrelevanten Entscheidungen verwendet werden (z. B. Missbrauchserkennung, Fraud-Scoring, automatisierte Vertrauensentscheidungen), auf systematische Verzerrungsmuster bewertet werden, die ein Angreifer ausnutzen könnte, um Kontrollen zu umgehen (z. B. indem er einen vertrauenswürdigen Sprachstil oder ein demografisches Muster nachahmt, um die Erkennung zu umgehen). |   2   |

---

## C1.5 Datenherkunft und Nachverfolgbarkeit

Verfolgen Sie die gesamte Reise jedes Datensatzes von der Quelle bis zur Modellschnittstelle, um Nachvollziehbarkeit für Audits und Incident Response sicherzustellen.

|   #   | Beschreibung                                                                                                                                                                                                    | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.5.1 | Stellen Sie sicher, dass die Abstammung jedes Datensatzes und seiner Komponenten, einschließlich aller Transformationen, Augmentierungen und Zusammenführungen, dokumentiert ist und rekonstruiert werden kann. |   1   |
| 1.5.2 | Stellen Sie sicher, dass Herkunftsaufzeichnungen unveränderlich sind, sicher gespeichert werden und für Audits zugänglich sind.                                                                                 |   2   |
| 1.5.3 | Stellen Sie sicher, dass die Nachverfolgung der Herkunft die synthetischen Daten abdeckt, die durch Augmentation, Synthese oder datenschutzfreundliche Techniken erzeugt werden.                                |   2   |
| 1.5.4 | Stellen Sie sicher, dass synthetische Daten im gesamten Pipeline-Verlauf eindeutig gekennzeichnet und klar von echten Daten unterscheidbar sind.                                                                |   2   |

---

## References

* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
* [EU AI Act: Article 10: Data & Data Governance](https://artificialintelligenceact.eu/article/10/)
* [CISA Advisory: Securing Data for AI Systems](https://www.cisa.gov/news-events/cybersecurity-advisories/aa25-142a)
* [OpenAI Privacy Center: Data Deletion Controls](https://privacy.openai.com/policies?modal=take-control)

