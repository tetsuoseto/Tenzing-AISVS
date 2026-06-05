# C1 Trainingsdatenintegrität und Rückverfolgbarkeit

## Kontrollziel

Dieses Kapitel behandelt die Beschaffung, Handhabung und Wartung von Trainingsdaten so, dass die Herkunfts- Nachverfolgbarkeit, Integrität und Qualität erhalten bleiben. Die zentrale Sicherheitsbedenken besteht darin, sicherzustellen, dass die Daten nicht manipuliert, vergiftet oder beschädigt wurden.

---

## C1.1 Herkunft der Trainingsdaten & Nachverfolgbarkeit

Die Herkunft und Nachverfolgbarkeit von Trainingsdaten sind entscheidend für die Sicherheit und Vertrauenswürdigkeit jedes KI-Systems. Datensätze müssen aus nachweisbaren Quellen bezogen und über ihren gesamten Lebenszyklus hinweg verfolgt werden, damit Manipulationen oder unautorisierte Änderungen erkannt werden können.

|   #   | Beschreibung                                                                                                                                                                                                                                          | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.1.1 | Stellen Sie sicher, dass ein aktuelles Verzeichnis jeder Quelle der Trainingsdaten (Herkunft, verantwortliche Stelle, Lizenz, Erfassungsmethode, Einschränkungen für die beabsichtigte Verwendung und Verarbeitungshistorie) gepflegt wird.           |   1   |
| 1.1.2 | Überprüfen Sie, dass Trainingsdatenverarbeitungen nur die für den angegebenen Zweck des Modells erforderlichen Merkmale, Attribute und Felder enthalten und alle anderen ausschließen (z. B. ungenutzte Metadaten, sensible PII, geleakte Testdaten). |   1   |
| 1.1.3 | Stellen Sie sicher, dass alle Änderungen am Datensatz einem protokollierten Genehmigungs-Workflow unterliegen.                                                                                                                                        |   1   |
| 1.1.4 | Stellen Sie sicher, dass Datensätze oder Teilmengen mit einem Wasserzeichen versehen oder mit Fingerprints versehen sind, um eine nachgelagerte Zuordnung und Erkennung nicht autorisierter Nutzung zu ermöglichen.                                   |   3   |

---

## C1.2 Datensicherheit und -integrität im Training

Trainingsdaten müssen während ihres gesamten Lebenszyklus vor Manipulation, Beschädigung und Vergiftung geschützt werden. Generische Datensicherheitskontrollen (Zugriffskontrolle auf dem Speicher, Zugriffserfassung und Verschlüsselung bei der Speicherung sowie bei der Übertragung) werden durch OWASP ASVS v5 (V6, V7, V8) abgedeckt und müssen als Baseline implementiert werden. Dieser Abschnitt behandelt KI-spezifische Anliegen: Integritätsprüfung gegen Data Poisoning, unveränderliche Dataset-Versionierung für Rollback und das verbleibende Risiko der Residual-Memorization, das in trainierten Modellen fortbesteht, nachdem die Trainingsdaten zurückgezogen wurden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                       | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.2.1 | Stellen Sie sicher, dass dokumentiert wird, dass beim Ausscheiden oder Entfernen von Trainingsdaten eine Folgenabschätzung durchgeführt wird, die alle auf diesen Daten trainierten Modelle abdeckt, das bewertete verbleibende Risiko für Residual Memorization beschreibt und die ausgewählte Maßnahme zur Minderung (gezieltes Fine-Tuning, Machine Unlearning, Modellaustraining oder dokumentierte Risikoakzeptanz) festlegt. |   1   |
| 1.2.2 | Stellen Sie sicher, dass kryptografische Hashes oder digitale Signaturen verwendet werden, um die Datenintegrität während der Speicherung und Übertragung der Trainingsdaten zu gewährleisten.                                                                                                                                                                                                                                     |   2   |
| 1.2.3 | Verifizieren Sie, dass die automatische Integritätsüberwachung angewendet wird, um unbefugte Änderungen oder die Beschädigung von Trainingsdaten zu verhindern.                                                                                                                                                                                                                                                                    |   2   |
| 1.2.4 | Stellen Sie sicher, dass alle Versionen des Trainingsdatensatzes eindeutig identifiziert sind, unveränderlich gespeichert werden und revisionsfähig sind, um Rollbacks und forensische Analysen zu unterstützen.                                                                                                                                                                                                                   |   3   |

---

## C1.3 Datensatzkennzeichnung und Annotationssicherheit

Kennzeichnungs- und Annotierungsprozesse müssen vor unbefugter Änderung, Zuordnungsverlust, Datenleckage und Beeinträchtigung der Integrität geschützt werden. Annotationplattformen sollten Zugriffskontrollen durchsetzen, die Nachvollziehbarkeit gewährleisten, eine verifizierte Zuordnung von Annotierenden beibehalten und während der gesamten Trainingspipeline Kennzeichnungsartefakte, Präferenzdaten und sensible Label-Inhalte schützen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                        | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.3.1 | Stellen Sie sicher, dass Kennzeichnungs-Interfaces und -Plattformen Zugriffskontrollen durchsetzen, die einschränken, wer Anmerkungen erstellen, ändern oder genehmigen kann.                                                                                                                                       |   1   |
| 1.3.2 | Stellen Sie sicher, dass alle Kennzeichnungsaktivitäten in Audit-Logs protokolliert werden, einschließlich der Identität der annotierenden Person, des Zeitstempels und der durchgeführten Aktion.                                                                                                                  |   1   |
| 1.3.3 | Stellen Sie sicher, dass Metadaten zur Identität des Annotators exportiert und zusammen mit dem Datensatz beibehalten werden, sodass jede Annotation oder jedes Präferenzpaar einem spezifischen, verifizierten menschlichen Annotator zugeordnet werden kann, und zwar über die gesamte Trainings-Pipeline hinweg. |   2   |
| 1.3.4 | Stellen Sie sicher, dass kryptografische Hashes oder digitale Signaturen auf Labeling-Artefakte, Annotationsdaten und Datensätze zum Fine-Tuning-Feedback (einschließlich RLHF-Präferenzpaaren) angewendet werden, um deren Integrität und Authentizität sicherzustellen.                                           |   2   |
| 1.3.5 | Stellen Sie sicher, dass sensible Informationen in Bezeichnungen vor der Verwendung in irgendeinem Kennzeichnungsartefakt entweder redigiert, anonymisiert oder verschlüsselt sind, sowohl im Ruhezustand als auch während der Übertragung.                                                                         |   2   |

---

## C1.4 Qualität der Trainingsdaten und Sicherheitsgewährleistung

Steuerungen zur Absicherung der Datenqualität und zur Sicherheit im Training helfen, Korruption, Vergiftung, Kennzeichnungsfehler und ausnutzbare Musterdarstellungen in Datensätzen zu erkennen, bevor sie das Modellverhalten beeinträchtigen. Pipelines sollten automatisierte Validierung, Vergiftungsdetektion, Prüfungen der Label-Qualität und Bias-Analysen kombinieren.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 1.4.1 | Stellen Sie sicher, dass automatisierte Tests Formatfehler und Nullwerte bei jeder Ingestion oder jeder wesentlichen Datenumwandlung erfassen.                                                                                                                                                                                                                                                                                                                                                               |   1   |
| 1.4.2 | Überprüfen Sie, dass Trainings- und Feinabstimmungs-Pipelines Techniken zur Validierung der Datenintegrität und zur Erkennung von Poisoning implementieren (z.B. statistische Analyse, Ausreißererkennung, Einbettungsanalyse), um potenzielles Daten-Poisoning oder unbeabsichtigte Beschädigung in Trainingsdaten zu identifizieren.                                                                                                                                                                       |   2   |
| 1.4.3 | Stellen Sie sicher, dass automatisch generierte Labels (z.B. via Modelle oder schwache Überwachung) Grenzwerte für die Konfidenz und Konsistenzprüfungen unterliegen, um irreführende oder niedrig-konfidente Labels zu erkennen.                                                                                                                                                                                                                                                                            |   2   |
| 1.4.4 | Verifizieren Sie, dass automatisierte Tests Label-Skews bei jeder Ingest- oder signifikanten Datenumwandlung erkennen.                                                                                                                                                                                                                                                                                                                                                                                       |   2   |
| 1.4.5 | Stellen Sie sicher, dass die Modelle, die in sicherheitsrelevanten Entscheidungen eingesetzt werden (z.B. Missbrauchserkennung, Betrugs-Scores, automatisierte Vertrauensentscheidungen), vor der Bereitstellung und nach jeder bedeutenden Modellaktualisierung auf systematische Verzerrungsmuster bewertet werden, die ein Angreifer ausnutzen könnte, um Kontrollen zu umgehen (z.B. indem er einen vertrauenswürdigen Sprachstil oder ein demografisches Muster nachahmt, um die Erkennung zu umgehen). |   2   |
| 1.4.6 | Stellen Sie sicher, dass Abwehrmaßnahmen gegen Data Poisoning zur Trainingszeit ausgewählt und angewendet werden, basierend auf einer dokumentierten Risikoanalyse, wobei die gewählte Abwehrmaßnahme (z.B. adversarial Training, Datenaugmentation mit verfälschten Eingaben oder robuste Optimierung) und ihre Begründung für die Abstimmung zusammen mit dem Modellartefakt dokumentiert werden.                                                                                                          |   2   |
| 1.4.7 | Verifizieren Sie, dass Abwehrmaßnahmen gegen Clean-Label-Poisoning-Angriffe (z. B. Input-Purification, k-NN-Filterung, Datenpartitionierung und -aggregation) für Modelle implementiert sind, die untrusted oder teilweise trusted Trainingsdatensources ausgesetzt sind.                                                                                                                                                                                                                                    |   3   |

---

## C1.5 Datenherkunft und Nachverfolgbarkeit

Datenherkunfts- und Rückverfolgbarkeitskontrollen stellen sicher, dass Datensätze vom Ausgangspunkt über Transformation, Augmentation, Zusammenführung und den finalen Modelleingang nachverfolgt werden können. Die Herkunftsaufzeichnungen sollten vollständig, manipulationssicher, revisionsfähig und ausreichend sein, um Reproduzierbarkeit, Incident Response, Rollback sowie die Untersuchung kompromittierter oder unangemessener Trainingsdaten zu unterstützen.

|   #   | Beschreibung                                                                                                                                                                                                      | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 1.5.1 | Verifizieren Sie, dass die Herkunft (Lineage) jedes Datensatzes und seiner Komponenten, einschließlich aller Transformationen, Augmentierungen und Zusammenführungen, erfasst wird und rekonstruiert werden kann. |   1   |
| 1.5.2 | Stellen Sie sicher, dass Abstammungsaufzeichnungen unveränderlich sind, sicher gespeichert und für Prüfungen zugänglich sind.                                                                                     |   2   |
| 1.5.3 | Verifizieren Sie, dass die Nachverfolgung der Herkunft die über Augmentierung, Synthese oder datenschutzfreundliche Techniken erzeugten synthetischen Daten abdeckt.                                              |   2   |
| 1.5.4 | Stellen Sie sicher, dass synthetische Daten im gesamten Prozess klar gekennzeichnet und eindeutig von echten Daten unterscheidbar sind.                                                                           |   2   |

---

## Referenzen

* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
* [EU AI Act: Article 10: Data & Data Governance](https://artificialintelligenceact.eu/article/10/)
* [CISA Advisory: Securing Data for AI Systems](https://www.cisa.gov/news-events/cybersecurity-advisories/aa25-142a)
* [OpenAI Privacy Center: Data Deletion Controls](https://privacy.openai.com/policies?modal=take-control)

