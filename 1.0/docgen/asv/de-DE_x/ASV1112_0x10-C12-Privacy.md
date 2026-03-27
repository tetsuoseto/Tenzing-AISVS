# C12 Datenschutz und Verwaltung personenbezogener Daten

## Kontrollziel

Gewährleisten Sie strenge Datenschutzgarantien über den gesamten KI-Lebenszyklus hinweg – Sammlung, Training, Inferenz und Vorfallreaktion – sodass personenbezogene Daten nur mit klarer Einwilligung, minimal notwendigem Umfang, nachweisbarer Löschung und formellen Datenschutzgarantien verarbeitet werden.

---

## C12.1 Anonymisierung & Datenminimierung

|   #    | Beschreibung                                                                                                                                                      | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 12.1.1 | Überprüfen Sie, dass direkte und Quasi-Identifikatoren entfernt oder gehasht werden.                                                                              |   1   |  D/V  |
| 12.1.2 | Überprüfen Sie, ob automatisierte Prüfungen k-Anonymität/l-Diversität messen und eine Warnung ausgeben, wenn die Schwellenwerte unter die Richtlinie fallen.      |   2   |  D/V  |
| 12.1.3 | Überprüfen Sie, dass die Modell-Feature-Importance-Berichte keine Identifikatoren-Leckage über ε = 0,01 gegenseitige Information hinaus nachweisen.               |   2   |   V   |
| 12.1.4 | Verifizieren Sie, dass formale Beweise oder synthetische Datenzertifizierungen ein Re-Identifizierungsrisiko von ≤ 0,05 auch bei Verknüpfungsangriffen aufweisen. |   3   |   V   |

---

## C12.2 Recht auf Vergessenwerden und Durchsetzung der Löschung

|   #    | Beschreibung                                                                                                                                                                                                          | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 12.2.1 | Überprüfen Sie, dass Löschanfragen bezüglich Datenpersonen innerhalb von Service-Level-Agreements von unter 30 Tagen auf Rohdatensätze, Checkpoints, Einbettungen, Protokolle und Sicherungskopien übertragen werden. |   1   |  D/V  |
| 12.2.2 | Stellen Sie sicher, dass „Machine-Unlearning“-Routinen physisch nachtrainiert werden oder eine angenäherte Entfernung unter Verwendung zertifizierter Unlearning-Algorithmen durchführen.                             |   2   |   D   |
| 12.2.3 | Überprüfen Sie, ob die Bewertung des Schattenmodells beweist, dass vergessene Datensätze weniger als 1 % der Ausgaben nach dem Unlearning beeinflussen.                                                               |   2   |   V   |
| 12.2.4 | Stellen Sie sicher, dass Löschvorgänge unveränderlich protokolliert und für Aufsichtsbehörden prüfbar sind.                                                                                                           |   3   |   V   |

---

## C12.3 Datenschutzmaßnahmen mit Differential Privacy

|   #    | Beschreibung                                                                                                                             | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 12.3.1 | Überprüfen Sie, ob Privacy-Loss-Accounting-Dashboards eine Warnung ausgeben, wenn das kumulative ε die Richtliniengrenzen überschreitet. |   2   |  D/V  |
| 12.3.2 | Überprüfen Sie, ob Black-Box-Datenschutzprüfungen ε̂ innerhalb von 10 % des angegebenen Werts schätzen.                                  |   2   |   V   |
| 12.3.3 | Überprüfen Sie, dass formale Beweise alle Feinabstimmungen und Einbettungen nach dem Training abdecken.                                  |   3   |   V   |

---

## C12.4 Zweckbindung & Schutz vor Umfangsüberschreitung

|   #    | Beschreibung                                                                                                                                                                  | Ebene | Rolle |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 12.4.1 | Verifizieren Sie, dass jeder Datensatz und jeder Modell-Checkpoint mit einem maschinenlesbaren Zweck-Tag versehen ist, das mit der ursprünglichen Einwilligung übereinstimmt. |   1   |   D   |
| 12.4.2 | Überprüfen Sie, ob Laufzeitüberwacher Abfragen erkennen, die mit dem angegebenen Zweck nicht übereinstimmen, und eine sanfte Ablehnung auslösen.                              |   1   |  D/V  |
| 12.4.3 | Überprüfen Sie, ob Richtlinien-als-Code-Barrieren die erneute Bereitstellung von Modellen in neuen Domänen ohne DPIA-Prüfung blockieren.                                      |   3   |   D   |
| 12.4.4 | Überprüfen Sie, dass formale Rückverfolgbarkeitsnachweise zeigen, dass jeder Lebenszyklus personenbezogener Daten innerhalb des genehmigten Umfangs bleibt.                   |   3   |   V   |

---

## C12.5 Einwilligungsverwaltung und rechtmäßige Grundlage der Nachverfolgung

|   #    | Beschreibung                                                                                                                                           | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 12.5.1 | Überprüfen Sie, ob eine Consent-Management-Plattform (CMP) den Opt-in-Status, den Zweck und die Aufbewahrungsdauer pro betroffener Person aufzeichnet. |   1   |  D/V  |
| 12.5.2 | Stellen Sie sicher, dass APIs Zustimmungs-Token bereitstellen; Modelle müssen den Geltungsbereich des Tokens vor der Inferenz validieren.              |   2   |   D   |
| 12.5.3 | Stellen Sie sicher, dass verweigerte oder widerrufene Einwilligungen die Verarbeitungspipelines innerhalb von 24 Stunden stoppen.                      |   2   |  D/V  |

---

## C12.6 Föderiertes Lernen mit Datenschutzkontrollen

|   #    | Beschreibung                                                                                                                   | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------ | :---: | :---: |
| 12.6.1 | Stellen Sie sicher, dass die Client-Updates vor der Aggregation lokale Differential Privacy Rauschzugabe verwenden.            |   1   |   D   |
| 12.6.2 | Verifizieren Sie, dass Trainingsmetriken differenziell privat sind und niemals den Verlust eines einzelnen Clients offenlegen. |   2   |  D/V  |
| 12.6.3 | Überprüfen Sie, dass eine vergiftungsresistente Aggregation (z. B. Krum/Trimmed-Mean) aktiviert ist.                           |   2   |   V   |
| 12.6.4 | Überprüfen Sie, dass formale Beweise das gesamte ε-Budget mit weniger als 5 Nutzungsverlust nachweisen.                        |   3   |   V   |

---

### Literaturverzeichnis

