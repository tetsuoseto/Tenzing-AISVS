# C14 Menschliche Aufsicht, Verantwortlichkeit & Governance

## Kontrollziel

Dieses Kapitel legt Anforderungen fest, um bei KI-Systemen eine menschliche Aufsicht aufrechtzuerhalten und klare Verantwortlichkeitsketten sicherzustellen, und stellt dabei Erklärbarkeit, Transparenz und ethische Verwaltung über den gesamten KI-Lebenszyklus hinweg sicher.

---

## C14.1 Kill-Switch- & Override-Mechanismen

Stellen Sie Abschalt- oder Rollback-Pfade bereit, wenn ein unsicheres Verhalten des KI-Systems beobachtet wird.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.1.1 | Verifizieren Sie, dass ein manueller Kill-Switch-Mechanismus vorhanden ist, um die Inferenz und Ausgaben des KI-Modells unmittelbar zu stoppen.                                                                                                                                                                                                                                                                                                                                                                                                                                 |   1   |
| 14.1.2 | Stellen Sie sicher, dass die Override-Steuerungen nur für autorisiertes Personal zugänglich sind.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |   1   |
| 14.1.3 | Verifizieren Sie, dass Rollback-Verfahren auf vorherige Modellversionen oder Safe-Mode-Vorgänge zurücksetzen können.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |   3   |
| 14.1.4 | Überprüfen Sie, ob Überschreibungsmechanismen regelmäßig getestet werden.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |   3   |
| 14.1.5 | Verifizieren Sie, dass das System in mindestens zwei Zwischen-Zustände des Betriebs zwischen dem Vollbetrieb und der vollständigen Abschaltung versetzt werden kann (z. B. das Deaktivieren bestimmter Tools oder MCP-Server, das Entfernen einer Retrieval-Quelle, das Umschalten auf ein sichereres oder kleineres Modell, das Erzwingen des Nur-Lese-Modus für Agents) und dass jeder Zustand definierte Einstiegsauslöser hat sowie unabhängig verlassen werden kann, ohne dass ein vollständiger Neustart oder eine vollständige Abschaltung des Systems erforderlich ist. |   2   |
| 14.1.6 | Überprüfen Sie, dass Override- und Kill-Switch-Befehle für autonome Agenten über einen Kanal zugestellt und durchgesetzt werden, auf den die Agent-Runtime nicht zugreifen, den sie nicht abfangen oder unterdrücken kann (z.B. Out-of-Band-Infrastrukturkontrollen, Hypervisor-Level-Signale, Netzwerkschicht-Isolation), sodass ein kompromittierter oder manipulierte Agent seine eigene Abschaltung nicht verhindern kann.                                                                                                                                                  |   2   |

---

## C14.2 Human-in-the-Loop-Entscheidungs-Checkpoints

Erfordern Sie menschliche Genehmigungen, wenn die Einsatzhöhe vordefinierte Risikoschwellen überschreitet.

>Hinweis zum Anwendungsbereich: C14.2 regelt die Richtlinie zur menschlichen Aufsicht: Sie definiert, welche KI-Entscheidungen oder -Handlungen als Hochrisiko eingestuft werden, die Kriterien und Schwellenwerte, die Genehmigungsanforderungen auslösen, sowie die Zuständigkeitsstruktur für die Erteilung von Genehmigungen. Der Laufzeit-Mechanismus zur Durchsetzung, der die Ausführung von Agenten blockiert, bis die Genehmigung vorliegt, ist in C9.2 festgelegt. Protokollierung und Auditierung von Genehmigungsentscheidungen sind in C13.7.4 geregelt. Die Einhaltung von C14.2 erfordert den Nachweis, dass eine dokumentierte Richtlinie existiert, nicht lediglich, dass Genehmigungen erteilt werden.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                          | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.2.1 | Stellen Sie sicher, dass eine dokumentierte Richtlinie zur menschlichen Aufsicht festlegt, welche KI-Entscheidungen und Agentenaktionen als Hochrisiko eingestuft werden, welche Kriterien für diese Bestimmung verwendet werden und welche Genehmigungsbefugnis vor der Ausführung erforderlich ist. |   1   |
| 14.2.2 | Stellen Sie sicher, dass Risikoschwellen eindeutig definiert sind und automatisch Workflows zur menschlichen Prüfung auslösen.                                                                                                                                                                        |   1   |
| 14.2.3 | Verifizieren Sie, dass zeitkritische Entscheidungen über Ausfallverfahren verfügen, wenn eine menschliche Genehmigung nicht innerhalb der erforderlichen Zeitrahmen eingeholt werden kann.                                                                                                            |   2   |
| 14.2.4 | Prüfen Sie, dass Eskalationsverfahren bei Bedarf klare Autoritätsstufen für unterschiedliche Entscheidungstypen oder Risikokategorien festlegen.                                                                                                                                                      |   3   |

---

## C14.3 Verantwortlichkeitskette & Nachvollziehbarkeit

Protokollieren Sie Operatoraktionen und Modellentscheidungen.

|   #    | Beschreibung                                                                                                                                                                           | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.3.1 | Stellen Sie sicher, dass alle Entscheidungen von KI-Systemen und alle menschlichen Eingriffe mit Zeitstempeln, Benutzeridentitäten und Entscheidungsbegründungen protokolliert werden. |   1   |

---

## C14.4 Techniken für Explainable-AI

|   #    | Beschreibung                                                                                                                                                                                                                        | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.4.1 | Stellen Sie sicher, dass KI-Systeme grundlegende Erklärungen für ihre Entscheidungen in menschenlesbarem Format bereitstellen.                                                                                                      |   1   |
| 14.4.2 | Verifizieren Sie, dass die Erklärungsqualität durch Human-Evaluierungsstudien und Metriken validiert wird.                                                                                                                          |   2   |
| 14.4.3 | Stellen Sie sicher, dass Feature-Importance-Scores oder Attributionsmethoden (SHAP, LIME, etc.) für kritische Entscheidungen verfügbar sind.                                                                                        |   3   |
| 14.4.4 | Überprüfen Sie, dass Gegenfaktenerklärungen (Counterfactual Explanations) zeigen, wie Eingaben so geändert werden könnten, dass sich Ergebnisse ändern, sofern dies für den Anwendungsfall und den jeweiligen Fachbereich zutrifft. |   3   |

---

## C14.5 Modellkarten & Offenlegungen zur Verwendung

Pflegen Sie Modellkarten für den vorgesehenen Einsatz, Leistungsmetriken und ethische Aspekte.

|   #    | Beschreibung                                                                                                                                                                                                      | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.5.1 | Überprüfen Sie, dass Modellkarten die beabsichtigten Anwendungsfälle, Einschränkungen und bekannten Ausfallmodi dokumentieren.                                                                                    |   1   |
| 14.5.2 | Stellen Sie sicher, dass Leistungskennzahlen für verschiedene anwendbare Anwendungsfälle offengelegt werden.                                                                                                      |   1   |
| 14.5.3 | Stellen Sie sicher, dass ethische Erwägungen, Bias-Analysen, Fairness-Bewertungen, Merkmale der Trainingsdaten sowie bekannte Einschränkungen der Trainingsdaten dokumentiert und regelmäßig aktualisiert werden. |   2   |
| 14.5.4 | Stellen Sie sicher, dass Modellkarten versionsgeführt werden und während des gesamten Modelllebenszyklus mit Änderungsverfolgung gepflegt werden.                                                                 |   2   |

---

## C14.6 Unsicherheitsquantifizierung

Verbreiten Sie Konfidenzwerte oder Entropiemaße in den Antworten.

|   #    | Beschreibung                                                                                                                      | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.6.1 | Stellen Sie sicher, dass KI-Systeme Vertrauenswerten oder Unsicherheitsmaße zusammen mit ihren Ausgaben bereitstellen.            |   1   |
| 14.6.2 | Überprüfen Sie, dass Unsicherheits-Schwellenwerte zusätzliche menschliche Prüfung oder alternative Entscheidungsabläufe auslösen. |   2   |
| 14.6.3 | Verifizieren Sie, dass Methoden zur Quantifizierung von Unsicherheit gegen Ground-Truth-Daten kalibriert und validiert werden.    |   2   |
| 14.6.4 | Verifizieren Sie, dass die Unsicherheitsfortpflanzung durch mehrstufige KI-Workflows beibehalten wird.                            |   3   |

---

## C14.7 Transparenzberichte mit Nutzerfokus

Geben Sie periodische Offenlegungen zu Vorfällen, Drift und Datenverwendung an.

|   #    | Beschreibung                                                                                                                                                                  | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 14.7.1 | Stellen Sie sicher, dass Richtlinien zur Datenverwendung und Praktiken zum Management der Einwilligung der Nutzer den Stakeholdern klar kommuniziert werden.                  |   1   |
| 14.7.2 | Stellen Sie sicher, dass KI-Wirkungsabschätzungen durchgeführt werden und die Ergebnisse in die Berichterstattung einbezogen werden.                                          |   2   |
| 14.7.3 | Stellen Sie sicher, dass Transparenzberichte regelmäßig veröffentlicht werden und KI-Vorfälle einschließlich ihrer Art, Auswirkung und Behebung offenlegen.                   |   2   |
| 14.7.4 | Überprüfen Sie, dass Transparenzberichte betriebliche Kennzahlen (z. B. Nutzungsvolumina, Sicherheitsfilterraten, Fehlerraten) in angemessenem Detaillierungsgrad offenlegen. |   2   |

## References

