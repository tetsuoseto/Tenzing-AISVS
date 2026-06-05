# C12 Datenschutzschutz & Verwaltung personenbezogener Daten

## Kontrollziel

Wahren Sie strenge Datenschutzzusicherungen über den gesamten KI-Lebenszyklus hinweg (Datenbeschaffung, Training, Inferenz und Incident Response), sodass personenbezogene Daten nur mit eindeutiger Einwilligung, im minimal notwendigen Umfang, mit nachweisbarer Löschung (Erasure) und mit formellen Datenschutzgarantien verarbeitet werden. Dieses Kapitel konzentriert sich auf KI-spezifische Datenschutzbedenken: Datenschutz-Eigenschaften von Trainingsdaten und daraus abgeleiteten Modellartefakten, Löschung und Unlearning über ML-Artefakte hinweg, Differential Privacy-Budgetverwaltung für das Training, Purpose Binding für Datensätze und Modelle, consent-aware Inferenz-Gating sowie datenschutzbezogene Kontrollmechanismen für Federated Learning.

---

## C12.1 Anonymisierung & Datenminimierung

Entfernen oder transformieren Sie persönliche Kennungen vor dem Training, um eine Re-Identifizierung zu verhindern und die Privatsphäreexposition zu minimieren.

|   #    | Beschreibung                                                                                                                                                                                                                                             | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.1.1 | Stellen Sie sicher, dass direkte und quasi-identifizierende Merkmale in Trainings- und Feinabstimmungsdatensätzen entfernt, gehasht oder generalisiert werden, bevor die Daten verwendet werden, um ein Modell zu trainieren oder zu aktualisieren.      |   1   |
| 12.1.2 | Stellen Sie sicher, dass automatisierte Audits k-Anonymität oder l-Diversität in Trainingsdatensätzen messen und benachrichtigen, wenn die Schwellenwerte unter die Richtlinie fallen.                                                                   |   2   |
| 12.1.3 | Stellen Sie sicher, dass Modell-Feature-Importance- oder Attributionsanalysen auf trainierten Modellen durchgeführt werden, um zu bestätigen, dass kein entfernter Identifier oder quasi-Identifier als hochwichtige Feature rekonstruiert wurde.        |   2   |
| 12.1.4 | Stellen Sie sicher, dass formale Beweise oder Zertifizierungen für synthetische Daten zeigen, dass das Risiko einer Re-Identifizierung gegenüber trainierten Modellen unter Verknüpfungsangriffen weiterhin unter einem dokumentierten Richtwert bleibt. |   3   |

---

## C12.2 Recht auf Vergessenwerden & Durchsetzung der Löschung

Stellen Sie sicher, dass Anfragen zur Löschung von betroffenen Personen sich über alle KI-Artefakte hinweg ausbreiten, und dass das Modell-Unlearning verifizierbar ist.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.2.1 | Verifizieren Sie, dass Data-Subject-Löschanfragen auf AI-abgeleitete Artefakte einschließlich Trainings- und Fine-Tuning-Datensätzen, Modell-Checkpoints, Evaluationssets, abgeleiteten Caches und Feature Stores innerhalb einer Service-Level-Vereinbarung von weniger als 30 Tagen propagiert werden. Die Propagation von Einbettungen und RAG-Indexes wird durch C8.3 geregelt. |   1   |
| 12.2.2 | Verifizieren Sie, dass Shadow-Model- oder Membership-Inference-Evaluierungen zeigen, dass vergessene Datensätze weniger Einfluss auf die Ausgaben des Modells haben als eine dokumentierte Schwellenwert-Policy nach dem Unlearning.                                                                                                                                                |   2   |
| 12.2.3 | Verifizieren Sie, dass Machine-Unlearning-Routinen, wenn sie behauptet werden, entweder das betroffene Modell physisch auf den zurückbehaltenen Daten neu trainieren oder einen zertifizierten Unlearning-Algorithmus anwenden, mit dokumentierten (ε, δ)-Garantien.                                                                                                                |   3   |

---

## C12.3 Schutzmaßnahmen der Differential Privacy

Verfolgen und erzwingen Sie Datenschutzbudgets, um formale Garantien gegen individuelle Datenlecks bereitzustellen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                               | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 12.3.1 | Stellen Sie sicher, dass der Differential-Privacy-Budgetverbrauch (sowohl ε- als auch δ-Werte) pro Trainingsrunde verfolgt und aufgezeichnet wird und dass der kumulative Verbrauch einen Alarm auslöst, wenn ε die festgelegten Richtlinien-Schwellenwerte überschreitet.                 |   2   |
| 12.3.2 | Verifizieren Sie, dass Black-Box-Privacy-Audits empirisch ε̂ als Untergrenze auf einem angegebenen Konfidenzniveau (z.B. Clopper-Pearson- oder f-DP-Konfidenzintervalle) schätzen und dass die Schätzung mit dem deklarierten Budget innerhalb der dokumentierten Toleranz konsistent ist. |   2   |
| 12.3.3 | Stellen Sie sicher, dass formale Datenschutzbeweise alle Post-Training-Feinabstimmungen und Embedding-Generierungsschritte abdecken, die dieselben Quelldaten verbrauchen.                                                                                                                 |   3   |

---

## C12.4 Zweckbindung & Scope-Creep-Schutz

Verhindern, dass Modelle und Datensätze über ihren ursprünglich zugestimmten Zweck hinaus verwendet werden.

|   #    | Beschreibung                                                                                                                                                                                                                                                                   | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 12.4.1 | Stellen Sie sicher, dass jedes Datenset und jeder Modell-Checkpoint über ein maschinenlesbares Zweck-Tag verfügt, das mit der ursprünglichen Einwilligung und der Rechtsgrundlage übereinstimmt, unter der die Quelldaten erhoben wurden.                                      |   1   |
| 12.4.2 | Stellen Sie sicher, dass Laufzeitmonitore Abfragen erkennen, die nicht mit dem deklarierten Zweck des Datensatzes oder des Modells übereinstimmen, und dass erkannte Abfragen entweder zu einer Soft-Ablehnung führen oder blockiert werden, bis eine Überprüfung erfolgt ist. |   1   |
| 12.4.3 | Stellen Sie sicher, dass Policy-as-Code-Gates eine erneute Bereitstellung von Modellen in neue Domänen ohne DPIA-Prüfung blockieren.                                                                                                                                           |   3   |
| 12.4.4 | Überprüfen Sie, dass formale Traceability-Nachweise zeigen, dass jeder Lebenszyklus personenbezogener Daten innerhalb des vereinbarten Zuständigkeitsbereichs bleibt.                                                                                                          |   3   |

---

## C12.5 Einwilligungsmanagement & Nachverfolgung der Rechtsgrundlage

Setzen Sie die Einwilligung bei AI-spezifischen Entscheidungspunkten durch (Training-Datenaufnahme, Inferenz) und propagieren Sie den Widerruf über alle AI-Artefakte hinweg.

|   #    | Beschreibung                                                                                                                                                                                                                                                                       | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.5.1 | Prüfen Sie, dass die Modellinferenz den Gültigkeitsbereich der Einwilligung validiert, bevor die Verarbeitung erfolgt, und decken Sie sowohl die angeforderte Operation als auch die betroffenen Personen ab, deren Daten die Antwort maßgeblich beeinflussen.                     |   2   |
| 12.5.2 | Verifizieren Sie, dass das System die Antwort verweigert oder herabstuft, bevor es sie an den Aufrufer übergibt, wenn der validierte Einwilligungsumfang die angeforderte Operation oder die betroffenen Personen, deren Daten die Antwort wesentlich beeinflussen, nicht abdeckt. |   2   |
| 12.5.3 | Pruefen Sie, dass der Widerruf der Einwilligung die gleiche AI-Artifact-Propagation-Pipeline ausloest wie eine Loeschanfrage (siehe 12.2.1), und dass Inferenzpfade, die auf die zurueckgezogenen Daten angewiesen sind, innerhalb der gleichen SLA deaktiviert werden.            |   2   |

---

## C12.6 Föderiertes Lernen mit Datenschutzkontrollen

Wenden Sie Differential Privacy und Datenschutz-Auditing auf föderiertes Lernen an, um die personenbezogenen Daten einzelner Teilnehmender zu schützen.

|   #    | Beschreibung                                                                                                                                                                                                                            | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.6.1 | Überprüfen Sie, dass Client-Updates eine lokale Differential-Privacy-Rauschbeimischung vor der Aggregation anwenden, oder dass ein dokumentierter zentraler Differential-Privacy-Mechanismus am Aggregator durchgesetzt wird.           |   1   |
| 12.6.2 | Stellen Sie sicher, dass Trainingsmetriken, die an den Aggregator oder an Clients weitergegeben werden, differenziell privat sind und niemals den Verlust eines einzelnen Clients oder einzelne Client-Gradienten offenlegen.           |   2   |
| 12.6.3 | Stellen Sie sicher, dass föderierte Lernsysteme canary-basierte Datenschutzprüfungen implementieren, um den Datenschutzverlust empirisch zu begrenzen, wobei die Prüfergebnisse protokolliert und pro Trainingszyklus überprüft werden. |   3   |
| 12.6.4 | Verifizieren Sie, dass formale Beweise das gesamte ε-Budget sowie die entsprechende Nutzenminderung gegenüber einer deklarierten Baseline dokumentieren.                                                                                |   3   |

---

## Referenzen

* [OWASP LLM02:2025 Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/)
* [General Data Protection Regulation (GDPR)](https://gdpr-info.eu/)
* [California Consumer Privacy Act (CCPA)](https://oag.ca.gov/privacy/ccpa)
* [EU Artificial Intelligence Act](https://artificialintelligenceact.eu/)
* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

