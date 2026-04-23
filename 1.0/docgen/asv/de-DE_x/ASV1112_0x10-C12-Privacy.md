# C12 Datenschutzschutz & Verwaltung personenbezogener Daten

## Kontrollziel

Behalten Sie strenge Datenschutzzusicherungen über den gesamten AI-Lebenszyklus hinweg bei (Sammlung, Training, Inferenz und Incident Response), sodass personenbezogene Daten nur mit klarer Einwilligung, minimal erforderlichem Umfang, nachweisbarer Löschung und formalen Datenschutzgarantien verarbeitet werden.

---

## C12.1 Anonymisierung & Datenminimierung

Entfernen Sie persönliche Identifikatoren vor dem Training oder wandeln Sie sie um, um eine Re-Identifizierung zu verhindern und die Datenschutzbelastung zu minimieren.

|   #    | Beschreibung                                                                                                                                                              | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.1.1 | Verifizieren Sie, dass direkte und quasi-identifizierende Merkmale entfernt und gehasht werden.                                                                           |   1   |
| 12.1.2 | Stellen Sie sicher, dass automatisierte Audits k-Anonymität/l-Diversität messen und eine Warnung ausgeben, wenn Schwellenwerte unter die Richtlinie fallen.               |   2   |
| 12.1.3 | Überprüfen Sie, dass modellbasierte Feature-Importance-Berichte keinen Identifier-Leckage über eine gegenseitige Information von ε = 0.01 hinaus belegen.                 |   2   |
| 12.1.4 | Stellen Sie sicher, dass formale Beweise oder Zertifizierungen für synthetische Daten das Risiko einer Re-Identifizierung ≤ 0.05 auch unter Verknüpfungsangriffen zeigen. |   3   |

---

## C12.2 Recht auf Vergessenwerden & Durchsetzung von Löschung

Stellen Sie sicher, dass Löschanfragen von betroffenen Personen über alle KI-Artefakte hinweg propagiert werden, und dass das Modell-Unlearning verifizierbar ist.

|   #    | Beschreibung                                                                                                                                                                                                     | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.2.1 | Überprüfen Sie, dass Datenschutzlöschanfragen für Betroffene innerhalb von Service Level Agreements von weniger als 30 Tagen in Rohdaten, Checkpoints, Embeddings, Protokollen und Backups weitergegeben werden. |   1   |
| 12.2.2 | Verifizieren Sie, dass "machine-unlearning"-Routinen physisch neu trainieren oder mithilfe zertifizierter unlearning-Algorithmen Entfernung approximieren.                                                       |   2   |
| 12.2.3 | Verifizieren Sie, dass die Bewertung des Shadow-Modells beweist, dass vergessene Datensätze nach dem Unlearning einen Einfluss von weniger als 1% auf die Ausgaben haben.                                        |   2   |
| 12.2.4 | Verifizieren Sie, dass Löschereignisse unveränderlich protokolliert und für Aufsichtsbehörden nachvollziehbar sind.                                                                                              |   3   |

---

## C12.3 Schutzmaßnahmen zur Differential-Privacy

Verfolgen und Erzwingen von Datenschutzbudgets, um formale Garantien gegen individuelle Daten-Lecks bereitzustellen.

|   #    | Beschreibung                                                                                                                                                                                                                      | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.3.1 | Überprüfen Sie, dass der Verbrauch des Differential Privacy Budgets (sowohl ε- als auch δ-Werte) pro Trainingsrunde verfolgt und aufgezeichnet wird.                                                                              |   2   |
| 12.3.5 | Überprüfen Sie, ob Dashboards für den kumulierten Differential Privacy-Budget über Benachrichtigungen verfügen, wenn ε die festgelegten Richtlinien-Schwellenwerte überschreitet.                                                 |   2   |
| 12.3.2 | Verifizieren Sie, dass Black-Box-Privacy-Audits ε̂ innerhalb von 10% des deklarierten Werts schätzen.                                                                                                                             |   2   |
| 12.3.3 | Stellen Sie sicher, dass formale Beweise alle Post-Training-Feinabstimmungen und Einbettungen abdecken.                                                                                                                           |   3   |
| 12.3.4 | Stellen Sie sicher, dass föderierte Lernsysteme Canary-basierte Datenschutzprüfungen implementieren, um den Datenschutzverlust empirisch einzugrenzen; die Prüfergebnisse werden protokolliert und pro Trainingszyklus überprüft. |   3   |

---

## C12.4 Zweckbindung & Scope-Creep-Schutz

Verhindern Sie, dass Modelle und Datensätze über ihren ursprünglich vereinbarten Zweck hinaus verwendet werden.

|   #    | Beschreibung                                                                                                                                                           | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.4.1 | Verifizieren Sie, dass jedes Dataset und jeder Model-Checkpoint einen maschinenlesbaren Zweck-Tag trägt, der mit der ursprünglichen Einwilligung übereinstimmt.        |   1   |
| 12.4.2 | Stellen Sie sicher, dass Laufzeitmonitore Abfragen erkennen, die nicht mit dem deklarierten Zweck des Datensatzes oder Modells übereinstimmen.                         |   1   |
| 12.4.5 | Überprüfen Sie, dass Abfragen, die als unvereinbar mit dem angegebenen Zweck erkannt wurden, eine sanfte Ablehnung auslösen oder bis zur Überprüfung blockiert werden. |   1   |
| 12.4.3 | Überprüfen Sie, dass policy-as-code gates die erneute Bereitstellung von Modellen in neue Domains ohne DPIA-Review blockieren.                                         |   3   |
| 12.4.4 | Überprüfen Sie, dass formale Nachverfolgbarkeitsbeweise sicherstellen, dass jeder Lebenszyklus personenbezogener Daten innerhalb des genehmigten Umfangs bleibt.       |   3   |

---

## C12.5 Einwilligungsverwaltung & Nachverfolgung der Rechtsgrundlage

Erfasse, erzwinge und widerrufe die Einwilligung über AI-Verarbeitungs-Pipelines hinweg.

|   #    | Beschreibung                                                                                                                                                                                                               | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.5.1 | Verifizieren Sie, dass eine Consent-Management-Plattform (CMP) den Opt-in-Status, den Zweck und die Aufbewahrungsdauer je betroffener Person erfasst.                                                                      |   1   |
| 12.5.2 | Verifizieren Sie, dass APIs Consent-Token offenlegen, die den Opt-in-Status der betroffenen Person, den Zweck und die Aufbewahrungsfrist kodieren.                                                                         |   2   |
| 12.5.4 | Stellen Sie sicher, dass Modelle die Gültigkeit des Zustimmungs-Token-Scopes vor der Inferenz überprüfen und die Verarbeitung verweigern, wenn das Token fehlt, ungültig ist oder den angeforderten Vorgang nicht abdeckt. |   2   |
| 12.5.3 | Verifizieren Sie, dass abgelehnte oder zurückgezogene Einwilligungen die Verarbeitungspipelines innerhalb von 24 Stunden stoppen.                                                                                          |   2   |

---

## C12.6 Föderiertes Lernen mit Datenschutzkontrollen

Wenden Sie differentielle Privatsphäre und auf Vergiftungsangriffe resilienter Aggregation auf das föderierte Lernen an, um die individuellen Teilnehmerdaten zu schützen.

|   #    | Beschreibung                                                                                                                     | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 12.6.1 | Überprüfen Sie, dass Client-Updates vor der Aggregation eine lokale Differential-Privacy-Rauschaddition verwenden.               |   1   |
| 12.6.2 | Stellen Sie sicher, dass Trainingsmetriken differenziell privat sind und niemals den Verlust eines einzelnen Clients offenlegen. |   2   |
| 12.6.3 | Überprüfen Sie, ob eine poisoning-resistente Aggregation (z.B. Krum/Gekürzter Mittelwert) aktiviert ist.                         |   2   |
| 12.6.4 | Überprüfen Sie, dass formale Beweise den gesamten ε-Budgetnachweis mit weniger als 5 Nutzungsverlust erbringen.                  |   3   |

---

## References

* [OWASP LLM02:2025 Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/)
* [General Data Protection Regulation (GDPR)](https://gdpr-info.eu/)
* [California Consumer Privacy Act (CCPA)](https://oag.ca.gov/privacy/ccpa)
* [EU Artificial Intelligence Act](https://artificialintelligenceact.eu/)
* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

