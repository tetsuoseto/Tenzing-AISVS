# C11 Adversarial Robustheit & Angriffsresistenz

## Kontrollziel

Stellen Sie sicher, dass KI-Systeme zuverlässig, datenschutzfreundlich und missbrauchsresistent bleiben, wenn sie Umgehungs-, Inferenz-, Extraktions- oder Poisoning-Angriffen ausgesetzt sind. Diese Kontrollen umfassen Tests zur Modell-Ausrichtung, die Stärkung gegen adversariale Angriffe, den Schutz gegen Datenschutzangriffe, Abschreckung gegen Modelldiebstahl und Sicherheitsanpassung für autonome Agenten.

---

## C11.1 Modellabstimmung & Sicherheit

Schützen Sie sich vor schädlichen oder gegen Richtlinien verstoßenden Ausgaben durch systematisches Testen und Schutzmaßnahmen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                             | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.1.1 | Überprüfen Sie, dass die Verweigerungs- und Safe-Completion-Guardrails durchgesetzt werden, um zu verhindern, dass das Modell nicht zulässige Inhaltkategorien generiert.                                                                                                                |   1   |
| 11.1.2 | Verifizieren Sie, dass eine Ausrichtungstest-Suite (Red-Team-Prompts, Jailbreak-Probes, Prüfungen auf unzulässige Inhalte) versionsverwaltet ist und bei jeder Modellaktualisierung oder jeder Veröffentlichung ausgeführt wird.                                                         |   1   |
| 11.1.3 | Überprüfen Sie, dass ein automatisierter Auswerter die Rate von schädlichem Inhalt misst und Regressionen über einen definierten Schwellenwert hinaus kennzeichnet.                                                                                                                      |   2   |
| 11.1.4 | Stellen Sie sicher, dass Ausrichtungs- und Sicherheitsschulungsmaßnahmen (z.B. RLHF, verfassungsbasierte KI oder ein entsprechendes Äquivalent) dokumentiert und nachvollziehbar reproduzierbar sind.                                                                                    |   2   |
| 11.1.5 | Stellen Sie sicher, dass die Ausrichtungsbewertung Bewertungen für die Bewertungsaufmerksamkeit (evaluation awareness) umfasst, bei denen das Modell sich möglicherweise anders verhält, wenn es erkennt, dass es getestet wird, im Vergleich zu dem Verhalten bei einer Bereitstellung. |   3   |

---

## C11.2 Abhärtung gegen Adversarial-Examples

Erhöhen Sie die Robustheit gegenüber manipulierten Eingaben, die darauf ausgelegt sind, Fehlklassifizierungen zu verursachen oder Richtlinien zu umgehen. Adversariales Testing und Robustheitsbenchmarking sind derzeit bewährte Vorgehensweisen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                 | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.2.1 | Stellen Sie sicher, dass Modelle, die Hochrisiko-Funktionen bereitstellen, gegen bekannte Angriffs-Techniken bewertet werden, die für ihre Modalität relevant sind (z. B. Perturbationsangriffe für die Bildverarbeitung, Token-Manipulationsangriffe für Text).             |   1   |
| 11.2.2 | Verifizieren Sie, dass die Erkennung von adversarialen Beispielen Warnmeldungen in Produktions-Pipelines auslöst, mit Blockierungs- oder eingeschränkten-Fähigkeiten-Antworten für Endpunkte oder Anwendungsfälle mit hohem Risiko.                                          |   2   |
| 11.2.3 | Stellen Sie sicher, dass adversariales Training oder äquivalente Härtungstechniken dort angewendet werden, wo dies praktikabel ist, mit dokumentierten Konfigurationen und reproduzierbaren Verfahren.                                                                       |   2   |
| 11.2.4 | Verifizieren Sie, dass Robustheitsevaluierungen adaptive Angriffe verwenden (Angriffe, die speziell dafür entworfen wurden, die bereitgestellten Abwehrmaßnahmen zu umgehen), um zu bestätigen, dass es über Releases hinweg zu keiner messbaren Robustheitsverlusten kommt. |   3   |
| 11.2.5 | Stellen Sie sicher, dass formale Robustheitsverifikationsmethoden (z.B. zertifizierte Schranken, Intervall-Propagation) auf sicherheitskritische Modellkomponenten angewendet werden, bei denen die Modellarchitektur sie unterstützt.                                       |   3   |

---

## C11.3 Schutz vor Membership-Inference

Begrenzen Sie die Fähigkeit, festzustellen, ob ein bestimmter Datensatz in den Trainingsdaten enthalten war. Differential Privacy und Output-Kalibrierung sind die wirksamsten bekannten Abwehrmaßnahmen.

|   #    | Beschreibung                                                                                                                                                                                                                                    | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.3.1 | Überprüfen Sie, dass die Modellausgaben kalibriert sind (z. B. über Temperatur-Skalierung oder Ausgabe-Störungen), um übermäßig selbstsichere Vorhersagen zu reduzieren, die Membership-Inference-Angriffe erleichtern.                         |   2   |
| 11.3.2 | Verifizieren Sie, dass das Training auf sensiblen Datensätzen eine differentially-private Optimierung (z.B. DP-SGD) nutzt, mit einem dokumentierten Datenschutzbudget (epsilon).                                                                |   2   |
| 11.3.3 | Verifizieren Sie, dass Membership-Inference-Angriffs-Simulationen (z. B. Shadow-Modell-, Likelihood-Ratio- oder Label-only-Angriffe) zeigen, dass die Angriffsgenauigkeit die Zufallsraten auf gehaltenen Daten nicht wesentlich überschreitet. |   3   |

---

## C11.4 Modell-Inversionsresistenz

Verhindern Sie die Rekonstruktion privater Trainingsdaten oder sensibler Attribute aus den Modell-Ausgaben.

>Hinweis zum Geltungsbereich: Ratenbegrenzung in C11.4 ist spezifisch auf Schutz vor Inversionsangriffen ausgerichtet: das Eindämmen wiederholter adaptiver Anfragen durch dieselbe Identität, um die Kosten für die Rekonstruktion von Trainingsdaten oder sensiblen Attributen zu erhöhen. Sie ist kein Ersatz für allgemeine API-Ratenbegrenzung (siehe ASVS v5 V2.4) oder für Ausführungsbudgets für Orchestrierung (C9.1). Allgemeine Missbrauchsprävention darf nicht doppelt als Schutz vor Inversionen angerechnet werden.

|   #    | Beschreibung                                                                                                                                                                                                                               | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 11.4.1 | Stellen Sie sicher, dass sensible Attribute niemals direkt ausgegeben werden; falls erforderlich, verwenden Ausgaben verallgemeinerte Kategorien (z. B. Bereiche, Buckets) oder einseitige Transformationen.                               |   1   |
| 11.4.2 | Stellen Sie sicher, dass Abfragelimits die wiederholten adaptiven Abfragen desselben Prinzipals drosseln, um die Kosten von Inversionsangriffen zu erhöhen.                                                                                |   1   |
| 11.4.3 | Stellen Sie sicher, dass Modelle, die mit sensiblen Daten umgehen, mit datenschutzfreundlichen Techniken trainiert werden (z. B. Differential Privacy, Gradient Clipping), um das Risiko von Informationslecks über Ausgaben zu begrenzen. |   2   |

---

## C11.5 Model-Extraction-Abwehr

Erkennen und Abschrecken unerlaubter Modellklonierung durch Missbrauch der API. Ratenbegrenzung, Analyse von Abfrage-Mustern und Watermarking werden als empfohlene Abwehrmaßnahmen genannt.

>Hinweis zum Geltungsbereich: Rate Limits in C11.5 werden speziell kalibriert, um eine großangelegte Abfrageerhebung zum Klonen von Modellen unpraktisch zu machen -- sie sind keine universellen API-Throttles (siehe ASVS v5 V2.4). Die Erfüllung von C11.5.1 erfordert den Nachweis, dass die Grenzwerte auf das Extraktionsbedrohungsmodell abgestimmt sind (z. B. Anzahl der Abfragen, die erforderlich sind, um das Modell zu approximieren), und nicht lediglich, dass irgendein Rate Limit vorhanden ist.

|   #    | Beschreibung                                                                                                                                                                                                        | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.5.1 | Überprüfen Sie, dass Inferenz-Endpunkte pro Principal und globale Rate Limits durchsetzen, die so gestaltet sind, dass groß angelegte Query-Harvesting-Aktivitäten unpraktisch gemacht werden.                      |   1   |
| 11.5.2 | Stellen Sie sicher, dass Extraktions-Alarmereignisse die Metadaten der beanstandeten Abfrage enthalten (z. B. Quell-Principal, Abfragevolumen, Eingabeverteilungsstatistiken), um die Untersuchung zu unterstützen. |   2   |
| 11.5.6 | Verifizieren Sie, dass Extraktion-Alarm-Ereignisse in Incident-Response-Playbooks integriert sind, die Eskalations- und Maßnahmen zur Behebung definieren.                                                          |   2   |
| 11.5.3 | Verifizieren Sie, dass die Analyse von Abfrage-Mustern (z.B. Abfragevielfalt, Anomalien der Eingabeverteilung) einen automatisierten Detektor für Extraktionsversuche speist.                                       |   2   |
| 11.5.4 | Verifizieren Sie, dass Modell-Wasserzeichen- oder Fingerprinting-Techniken angewendet werden, damit nicht autorisierte Kopien identifiziert werden können.                                                          |   3   |
| 11.5.5 | Stellen Sie sicher, dass Wasserzeichen-Überprüfungsschlüssel und Trigger-Sets mit Zugriffskontrollen geschützt sind, die mit denen für andere kritische kryptografische Materialien vergleichbar sind.              |   3   |

---

## C11.6 Erkennung von vergifteten Daten zur Laufzeit der Inferenz

Identifizieren und neutralisieren Sie zur Laufzeit Inferenzzeit zurückverbaute oder vergiftete Eingaben, insbesondere in Systemen, die externe Daten verarbeiten (z. B. RAG-Pipelines, Tool-Ausgaben).

|   #    | Beschreibung                                                                                                                                                                                                                            | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.6.1 | Stellen Sie sicher, dass Eingaben von externen oder nicht vertrauenswürdigen Quellen vor der Modellinferenz eine Anomalieerkennung durchlaufen (z.B. statistische Ausreißererkennung, Konsistenzbewertung).                             |   2   |
| 11.6.2 | Stellen Sie sicher, dass Anomalie-Erkennungs-Schwellenwerte auf repräsentativen sauberen und adversarialen Validierungsdatensätzen abgestimmt werden und dass die Falsch-Positiv-Rate gemessen und dokumentiert wird.                   |   2   |
| 11.6.3 | Überprüfen Sie, dass Eingaben, die als anomali erkannt wurden, entsprechende Gatekeeping-Aktionen auslösen (Blockierung, Fähigkeitsbeeinträchtigung oder menschliche Überprüfung), die dem Risikoniveau angemessen sind.                |   2   |
| 11.6.4 | Verifizieren Sie, dass die Erkennungsmethoden regelmäßig mit aktuellen Angriffstechniken unter Stress getestet werden, einschließlich adaptiver Angriffe, die entwickelt wurden, um die spezifischen verwendeten Detektoren zu umgehen. |   3   |
| 11.6.5 | Überprüfen Sie, dass Nachweiseffizienz-Kennzahlen protokolliert und regelmäßig anhand aktualisierter Bedrohungsinformationen neu bewertet werden.                                                                                       |   3   |

---

## C11.7 Sicherheitsrichtlinien-Anpassung

Echtzeit-Sicherheitsrichtlinien-Updates basierend auf Bedrohungsinformationen und Verhaltensanalytik.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                 | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.7.1 | Stellen Sie sicher, dass Sicherheitsrichtlinien (z. B. Content-Filter, Rate-Limit-Schwellenwerte, Guardrail-Konfigurationen) aktualisiert werden können, ohne dass eine vollständige System-Neu-Bereitstellung erforderlich ist, und dass die Versionen der Richtlinien nachverfolgt werden. |   1   |
| 11.7.2 | Verifizieren Sie, dass Richtlinienaktualisierungen autorisiert sind, integritätsschutzfähig (z. B. kryptografisch signiert) und vor der Anwendung validiert werden.                                                                                                                          |   2   |
| 11.7.3 | Stellen Sie sicher, dass Richtlinienänderungen mit Audit-Trails protokolliert werden, einschließlich Zeitstempel, Autor und Begründung.                                                                                                                                                      |   2   |
| 11.7.5 | Stellen Sie sicher, dass es Rollback-Verfahren für Richtlinienänderungen gibt und dass sie getestet werden, um zu bestätigen, dass sie den vorherigen Richtlinienzustand wiederherstellen.                                                                                                   |   2   |
| 11.7.4 | Stellen Sie sicher, dass die Empfindlichkeit der Bedrohungserkennung anhand des Risikokontexts (z.B. erhöhter Bedrohungsgrad, Incident-Response) mit entsprechender Autorisierung angepasst werden kann.                                                                                     |   3   |

---

## C11.8 Agentensicherheits-Selbstbewertung

Für agentische KI-Systeme validieren, dass die Schlussfolgerungen und Aktionen des Agenten durch sicherheitsorientierte Überprüfungsmechanismen unterliegen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                           | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.8.1 | Stellen Sie sicher, dass agentische Systeme über einen Mechanismus verfügen, um geplante sicherheitskritische Aktionen vor der Ausführung anhand der Sicherheitsrichtlinie zu prüfen (z.B. ein zweites Modell, ein regelbasierter Prüfer oder ein strukturierter Self-Review-Schritt). |   2   |
| 11.8.2 | Stellen Sie sicher, dass Sicherheitsüberprüfungsmechanismen gegen Manipulation durch gegnerische Eingaben geschützt sind (z. B. dass der Überprüfungsschritt nicht durch Prompt Injection überschrieben oder umgangen werden kann).                                                    |   2   |
| 11.8.3 | Stellen Sie sicher, dass Sicherheitsprüfungswarnungen erweiterte Monitoring- oder Human-Intervention-Workflows für die betroffene Sitzung oder Aufgabe auslösen.                                                                                                                       |   3   |

---

## C11.9 Sicherheitsaspekte bei Selbstmodifikation & autonomem Update

Sicherheitskontrollen für Systeme, bei denen die KI ihre eigene Konfiguration, Prompts, den Zugriff auf Tools oder gelernte Verhaltensweisen ändern kann.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.9.1 | Stellen Sie sicher, dass jede Fähigkeit zur Selbstmodifikation (z. B. Prompt-Umschreibung, Änderungen an der Tool-Liste, Aktualisierungen von Parametern) auf explizit ausgewiesene Bereiche beschränkt ist, mit erzwungenen Grenzen.                                                                                                                                                                                                                       |   2   |
| 11.9.2 | Stellen Sie sicher, dass vorgeschlagene Selbständerungen einer Sicherheitsfolgenabschätzung oder einer Richtlinienvalidierung unterzogen werden, bevor sie wirksam werden.                                                                                                                                                                                                                                                                                  |   2   |
| 11.9.3 | Stellen Sie sicher, dass alle Selbstmodifikationen mit ausreichenden Details protokolliert werden, um nachzuvollziehen, was geändert wurde, wann es geändert wurde und unter welcher Autorisierung.                                                                                                                                                                                                                                                         |   2   |
| 11.9.6 | Stellen Sie sicher, dass Selbstmodifikationen reversibel sind und einer Integritätsprüfung unterliegen, sodass ein Rollback auf einen bekannten fehlerfreien Zustand möglich ist und bestätigt werden kann.                                                                                                                                                                                                                                                 |   2   |
| 11.9.4 | Stellen Sie sicher, dass der Bereich der Selbstmodifikation begrenzt ist (z. B. maximale Änderungsstärke, Ratenbegrenzungen für Updates, verbotene Änderungsziele), um ausufernde oder durch Angriffe ausgelöste Änderungen zu verhindern.                                                                                                                                                                                                                  |   3   |
| 11.9.5 | Verifizieren Sie, dass, wenn Sicherheitsverletzungsdaten (blockierte Eingaben, gefilterte Ausgaben, markierte Halluzinationen) als Trainingssignal zur Verbesserung des Modells verwendet werden, die Feedback-Pipeline Integritätsprüfungen, Mechanismen zur Erkennung von Poisoning und Gate-Kontrollen zur menschlichen Überprüfung umfasst, um eine schädliche Beeinflussung des Verbesserungsmechanismus durch Adversarial Manipulation zu verhindern. |   3   |

## C11.10 Abwehr von Ausnutzung adversarialer Verzerrungen

Schützen Sie sicherheitsrelevante Klassifikatoren vor Angreifern, die systematisch nach ausnutzbaren Verzerrungsmustern suchen und die entdeckten Unterschiede als Umgehungsvektor zweckentfremden.

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Ebene |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 11.10.1 | Verifizieren Sie, dass Inferenz-Endpunkte für sicherheitsrelevante Klassifizierer (z.B. Missbrauchserkennung, Fraud-Scoring) Überwachung enthalten, die Abfrage-Muster berücksichtigt, welche auf Bias-Probing hindeuten, wie etwa eine systematische Variation entlang einer einzelnen Eingabedimension (z.B. demografisch, sprachlich, stilistisch), während andere Dimensionen konstant bleiben, und dass ein Alarm ausgelöst wird, wenn solche Muster erkannt werden.                                                |   3   |
| 11.10.2 | Überprüfen Sie, dass die Bewertungen der adversarialen Robustheit für sicherheitsrelevante Klassifikatoren nach sinnvollen Eingabe-Untergruppen geschichtet sind (z.B. Sprachregister, Inhaltskategorie). Messen und kennzeichnen Sie dabei die pro Untergruppe ermittelten False-Negative-Raten unter adversarialen Bedingungen, wenn sie von den aggregierten Raten abweichen, über eine definierte Schwelle hinaus.                                                                                                   |   2   |
| 11.10.3 | Verifizieren Sie, dass dort, wo Bias-basierte Umgehung als wesentliche Bedrohung identifiziert wird, die adversarial Hardening-Maßnahmen (z.B. adversariales Training mit Nebenbedingungen für die Verlustfunktion pro Untergruppe, Ensemble-Diversität über Trainingsverteilungen hinweg) explizite Anforderungen an die Robustheit der jeweiligen Untergruppen einbeziehen und dass die pro-Untergruppe-Robustheitsmetriken so überprüft werden, dass sie sich zwischen Modellveröffentlichungen nicht verschlechtern. |   3   |

---

## References

* [OWASP LLM02:2025 Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/)
* [OWASP LLM04:2025 Data and Model Poisoning](https://genai.owasp.org/llmrisk/llm042025-data-and-model-poisoning/)
* [OWASP LLM10:2025 Unbounded Consumption](https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/)
* [MITRE ATLAS: Infer Training Data Membership](https://atlas.mitre.org/techniques/AML.T0024.000)
* [MITRE ATLAS: Invert ML Model](https://atlas.mitre.org/techniques/AML.T0024.001)
* [MITRE ATLAS: Extract ML Model](https://atlas.mitre.org/techniques/AML.T0024.002)
* [MITRE ATLAS: Backdoor ML Model](https://atlas.mitre.org/techniques/AML.T0018)
* [NIST AI 100-2e2023 Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations](https://csrc.nist.gov/pubs/ai/100/2/e2023/final)
* [MITRE ATLAS: Active Scanning (AML.T0006)](https://atlas.mitre.org/techniques/AML.T0006)
* [MITRE ATLAS: Evade ML Model (AML.T0015)](https://atlas.mitre.org/techniques/AML.T0015)
* [MITRE ATLAS Case Study: Bypass Cylance's AI Malware Detection (AML.CS0003)](https://atlas.mitre.org/studies/AML.CS0003)

