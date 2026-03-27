# C14 Menschliche Aufsicht, Verantwortlichkeit & Governance

## Kontrollziel

Dieses Kapitel enthält Anforderungen für die Aufrechterhaltung der menschlichen Aufsicht und klarer Verantwortlichkeitsketten in KI-Systemen, um Erklärbarkeit, Transparenz und ethische Leitung während des gesamten KI-Lebenszyklus sicherzustellen.

---

## C14.1 Not-Aus-Schalter & Übersteuerungsmechanismen

Stellen Sie Abschalt- oder Rückfallwege bereit, wenn ein unsicheres Verhalten des KI-Systems beobachtet wird.

|   #    | Beschreibung                                                                                                                      | Ebene | Rolle |
| :----: | --------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.1.1 | Überprüfen Sie, ob ein manueller Not-Aus-Mechanismus vorhanden ist, um die Inferenz und Ausgabe des KI-Modells sofort zu stoppen. |   1   |  D/V  |
| 14.1.2 | Stellen Sie sicher, dass die Übersteuerungskontrollen nur für autorisiertes Personal zugänglich sind.                             |   1   |   D   |
| 14.1.3 | Überprüfen Sie, ob Rollback-Verfahren auf vorherige Modellversionen oder sichere Betriebsmodi zurücksetzen können.                |   3   |  D/V  |
| 14.1.4 | Stellen Sie sicher, dass Übersteuerungsmechanismen regelmäßig getestet werden.                                                    |   3   |   V   |

---

## C14.2 Mensch-in-der-Schleife Entscheidungsprüfpunkte

Menschliche Genehmigungen erforderlich, wenn die Einsätze vordefinierte Risikoschwellen überschreiten.

|   #    | Beschreibung                                                                                                                                                                                   | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.2.1 | Stellen Sie sicher, dass hochriskante KI-Entscheidungen vor der Ausführung eine ausdrückliche menschliche Genehmigung erfordern.                                                               |   1   |  D/V  |
| 14.2.2 | Stellen Sie sicher, dass Risikoschwellenwerte klar definiert sind und automatisch Überprüfungsabläufe durch Menschen auslösen.                                                                 |   1   |   D   |
| 14.2.3 | Stellen Sie sicher, dass zeitkritische Entscheidungen über Fallback-Verfahren verfügen, wenn eine menschliche Genehmigung nicht innerhalb der erforderlichen Zeitrahmen eingeholt werden kann. |   2   |   D   |
| 14.2.4 | Stellen Sie sicher, dass Eskalationsverfahren klare Befugnisstufen für verschiedene Entscheidungstypen oder Risikokategorien definieren, falls zutreffend.                                     |   3   |  D/V  |

---

## C14.3 Verantwortlichkeitskette & Prüfbarkeit

Protokollieren Sie Operatoraktionen und Modellentscheidungen.

|   #    | Beschreibung                                                                                                                                                                     | Ebene | Rolle |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.3.1 | Stellen Sie sicher, dass alle Entscheidungen des KI-Systems und menschlichen Eingriffe mit Zeitstempeln, Benutzeridentitäten und Entscheidungsbegründungen protokolliert werden. |   1   |  D/V  |
| 14.3.2 | Überprüfen Sie, dass Prüfprotokolle nicht manipuliert werden können und Integritätsprüfmechanismen enthalten.                                                                    |   2   |   D   |

---

## C14.4 Erklärbare-KI-Techniken

|   #    | Beschreibung                                                                                                                                                                                | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.4.1 | Überprüfen Sie, ob KI-Systeme grundlegende Erklärungen für ihre Entscheidungen in einem für Menschen lesbaren Format liefern.                                                               |   1   |  D/V  |
| 14.4.2 | Stellen Sie sicher, dass die Qualität der Erklärungen durch menschliche Evaluationsstudien und Metriken validiert wird.                                                                     |   2   |   V   |
| 14.4.3 | Stellen Sie sicher, dass Merkmalswichtigkeitswerte oder Attributionsmethoden (SHAP, LIME usw.) für kritische Entscheidungen verfügbar sind.                                                 |   3   |  D/V  |
| 14.4.4 | Überprüfen Sie, ob kontrafaktische Erklärungen aufzeigen, wie Eingaben verändert werden könnten, um Ergebnisse zu ändern, sofern dies für den Anwendungsfall und die Domäne zutreffend ist. |   3   |   V   |

---

## C14.5 Modellkarten & Nutzungsangaben

Führen Sie Modellkarten für den beabsichtigten Einsatz, Leistungskennzahlen und ethische Überlegungen.

|   #    | Beschreibung                                                                                                                                                                                                           | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.5.1 | Überprüfen Sie, ob Modelkarten die beabsichtigten Anwendungsfälle, Einschränkungen und bekannten Ausfallmodi dokumentieren.                                                                                            |   1   |   D   |
| 14.5.2 | Stellen Sie sicher, dass Leistungskennzahlen für verschiedene anwendbare Anwendungsfälle offengelegt werden.                                                                                                           |   1   |  D/V  |
| 14.5.3 | Stellen Sie sicher, dass ethische Überlegungen, Bias-Bewertungen, Fairness-Evaluierungen, Merkmale der Trainingsdaten und bekannte Einschränkungen der Trainingsdaten dokumentiert und regelmäßig aktualisiert werden. |   2   |   D   |
| 14.5.4 | Stellen Sie sicher, dass Modellkarten versionskontrolliert sind und während des gesamten Modelllebenszyklus mit Änderungsverfolgung gepflegt werden.                                                                   |   2   |  D/V  |

---

## C14.6 Unsicherheitsquantifizierung

Verbreiten Sie Konfidenzwerte oder Entropie-Maße in den Antworten.

|   #    | Beschreibung                                                                                                                    | Ebene | Rolle |
| :----: | ------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.6.1 | Stellen Sie sicher, dass KI-Systeme Vertrauenswerte oder Unsicherheitsmaße mit ihren Ergebnissen bereitstellen.                 |   1   |   D   |
| 14.6.2 | Überprüfen Sie, ob Unsicherheitsschwellen eine zusätzliche menschliche Überprüfung oder alternative Entscheidungswege auslösen. |   2   |  D/V  |
| 14.6.3 | Überprüfen Sie, ob Unsicherheitsquantifizierungsmethoden kalibriert sind und anhand von tatsächlichen Daten validiert wurden.   |   2   |   V   |
| 14.6.4 | Stellen Sie sicher, dass die Unsicherheitsfortpflanzung in mehrstufigen KI-Arbeitsabläufen aufrechterhalten wird.               |   3   |  D/V  |

---

## C14.7 Benutzerorientierte Transparenzberichte

Geben Sie regelmäßige Berichte über Vorfälle, Drift und Datennutzung.

|   #    | Beschreibung                                                                                                                                         | Ebene | Rolle |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------- | :---: | :---: |
| 14.7.1 | Stellen Sie sicher, dass Datenschutzrichtlinien und Praktiken zur Verwaltung der Nutzerzustimmung klar an die Interessengruppen kommuniziert werden. |   1   |  D/V  |
| 14.7.2 | Überprüfen Sie, ob AI-Auswirkungsbewertungen durchgeführt werden und die Ergebnisse in die Berichterstattung aufgenommen sind.                       |   2   |  D/V  |
| 14.7.3 | Überprüfen Sie, ob regelmäßig veröffentlichte Transparenzberichte KI-Vorfälle und betriebliche Kennzahlen in angemessenem Detail offenlegen.         |   2   |  D/V  |

### Literaturverzeichnis

