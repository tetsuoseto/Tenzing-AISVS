# C11 Adversarial Robustness & Attack Resistance

## Kontrollziel

Stellen Sie sicher, dass KI-Systeme zuverlässig, datenschutzfreundlich und missbrauchsresistent bleiben, wenn sie Umgehungs-, Inferenz-, Extraktions- oder Poisoning-Angriffen ausgesetzt sind. Diese Kontrollen umfassen Modell-Alignment-Tests, die Härtung gegen Adversarial-Angriffe, Widerstandsfähigkeit gegen Datenschutzangriffe, Abschreckung gegen Modelldiebstahl sowie Sicherheitsanpassung für autonome Agenten.

---

## C11.1 Modell-Ausrichtung & Sicherheit

Schützen Sie vor schädlichen oder gegen Richtlinien verstoßenden Ausgaben durch systematisches Testen und Schutzvorrichtungen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                            | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.1.1 | Überprüfen Sie, dass die Ablehnungs- und die Safe-Completion-Schutzmaßnahmen durchgesetzt werden, um zu verhindern, dass das Modell nicht zulässige Inhaltkategorien generiert.                                                                                                                         |   1   |
| 11.1.2 | Stellen Sie sicher, dass eine Ausrichtungstest-Suite, einschließlich Red-Team-Prompts, Jailbreak-Tests, Prüfungen auf nicht zulässige Inhalte und mehrsprachigen oder Code-Switching-Missbrauchsfällen, versioniert ist und bei jeder Modellaktualisierung oder jeder Veröffentlichung ausgeführt wird. |   1   |
| 11.1.3 | Verifizieren Sie, dass ein automatisierter Evaluator die Rate für schädliche Inhalte misst und Regressionen über einen definierten Schwellenwert hinaus kennzeichnet.                                                                                                                                   |   2   |
| 11.1.4 | Stellen Sie sicher, dass Ausrichtungs- und Sicherheits-Trainingsverfahren (z.B. RLHF, konstitutionelle KI oder entsprechende) dokumentiert und reproduzierbar sind.                                                                                                                                     |   2   |
| 11.1.5 | Stellen Sie sicher, dass die Ausrichtungsbewertung Beurteilungen für Evaluierungsbewusstsein beinhaltet, wobei das Modell möglicherweise anders reagiert, wenn es erkennt, dass es getestet wird, im Vergleich zur Bereitstellung.                                                                      |   3   |

---

## C11.2 Härtung von Adversarial-Examples

Erhöhen Sie die Resilienz gegenüber manipulierten Eingaben, die darauf ausgelegt sind, Fehlklassifizierungen herbeizuführen oder Richtlinienumgehungen zu ermöglichen. Adversarial Testing und Robustheits-Benchmarking sind derzeit bewährte Best Practices.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                     | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 11.2.1 | Stellen Sie sicher, dass Modelle, die Hochrisiko-Funktionen bereitstellen, gegen bekannte Angriffs-Techniken bewertet werden, die für ihre Modalität relevant sind (z.B. Perturbationsangriffe für die Bildverarbeitung, Token-manipulationsbasierte Angriffe für Text, triggerbasierte oder Instruction-Injection-Backdoors, sofern anwendbar). |   1   |
| 11.2.2 | Überprüfen Sie, dass die Erkennung von Adversarial Examples in Produktions-Pipelines Warnmeldungen auslöst, mit blockierenden oder eingeschränkten-Fähigkeiten-Reaktionen für Endpunkte oder Anwendungsfälle mit hohem Risiko.                                                                                                                   |   2   |
| 11.2.3 | Stellen Sie sicher, dass Modelle, die für risikoreiche Funktionen eingesetzt werden, gegen bösartige Eingaben durch Härtungsmaßnahmen geschützt sind, und zwar mithilfe einer oder mehrerer Techniken wie adversarial Training, Randomized Smoothing, Defensive Distillation oder Input Transformation.                                          |   2   |
| 11.2.4 | Stellen Sie sicher, dass die zertifizierten Robustheitsmetriken (z.B. zertifizierter Radius, verifizierte robuste Genauigkeit bei definierten Störgrenzen) pro Modellversion erfasst und aufgezeichnet werden, und dass eine Verschlechterung über die definierten Schwellenwerte hinaus eine erneute Bewertung vor der Bereitstellung auslöst.  |   2   |
| 11.2.5 | Stellen Sie sicher, dass Abwehr-Härtungskonfigurationen und -verfahren dokumentiert und reproduzierbar sind.                                                                                                                                                                                                                                     |   2   |
| 11.2.6 | Stellen Sie sicher, dass Robustheitsevaluierungen adaptive Angriffe verwenden (Angriffe, die speziell entwickelt wurden, um die bereitgestellten Abwehrmaßnahmen zu umgehen), um zu bestätigen, dass es über die Releases hinweg keinen messbaren Robustheitsverlust gibt.                                                                       |   3   |
| 11.2.7 | Verifizieren Sie, dass formale Robustheitsverifikationsmethoden (z.B. zertifizierte Schranken, Interval-Bound Propagation) auf sicherheitskritische Modellkomponenten angewendet werden, bei denen die Modellarchitektur sie unterstützt.                                                                                                        |   3   |
| 11.2.8 | Stellen Sie sicher, dass Robustheitszertifizierungen oder empirische Robustheitsaudits nach allen Post-Training-Transformationen (Feinabstimmung, Distillation, Quantisierung, Adapter-Merging) wiederholt werden, die dasselbe Basismodell verwenden.                                                                                           |   3   |
| 11.2.9 | Überprüfen Sie, dass Post-Training-Methoden zur Integritätsprüfung des Modells (z.B. Aktivitäts-Clusterbildung, Spektralsignaturanalyse, Neural Cleanse) angewendet werden, um potenzielle Backdoors oder durch Poisoning verursachte Verhaltensanomalien zu erkennen, wobei solche Techniken für die Modellarchitektur verfügbar sind.          |   3   |

---

## C11.3 Schutz vor Membership-Inference

Begrenzen Sie die Fähigkeit, festzustellen, ob ein bestimmter Datensatz in den Trainingsdaten enthalten war. Differential Privacy und Output-Kalibrierung sind die wirksamsten bekannten Abwehrmaßnahmen.

|   #    | Beschreibung                                                                                                                                                                                                                                       | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.3.1 | Überprüfen Sie, dass die Modellausgaben kalibriert sind (z.B. über Temperatur-Skalierung oder Ausgabe-Perturbation), um übermäßig selbstsichere Vorhersagen zu reduzieren, die Membership-Inference-Angriffe erleichtern.                          |   2   |
| 11.3.2 | Stellen Sie sicher, dass das Training auf sensiblen Datensätzen ein differentially-private Optimierung (z.B. DP-SGD) nutzt, mit einem dokumentierten Datenschutzbudget (epsilon).                                                                  |   2   |
| 11.3.3 | Überprüfen Sie, dass Mitgliedschafts-Inferenz-Angriffssimulationen (z.B. Shadow-Modell-, Likelihood-Ratio- oder Label-only-Angriffe) zeigen, dass die Angriffsgenauigkeit auf zurückgehaltenen Daten nicht wesentlich über dem Zufallsraten liegt. |   3   |

---

## C11.4 Modell-Inversionsresistenz

Verhindern Sie die Rekonstruktion privater Trainingsdaten oder sensibler Attribute aus den Modell-Ausgaben.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                              | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.4.1 | Überprüfen Sie, dass modellinferierte sensible Attribute nicht direkt in Ausgaben zurückgegeben werden; wenn solche Attribute offengelegt werden müssen, werden sie als verallgemeinerte Kategorien (z. B. Bereiche, Buckets) oder als Einweg-Transformationen zurückgegeben, um die Rekonstruktion zugrunde liegender Trainingsdatensätze zu begrenzen.                  |   1   |
| 11.4.2 | Überprüfen Sie, dass Query-Rate-Limits wiederholte adaptive Abfragen derselben Identität drosseln, bei Schwellenwerten, die auf das Inversionsbedrohungsmodell abgestimmt sind (z. B. die Anzahl der Abfragen, die erforderlich ist, um Trainingsdaten oder sensible Attribute zu rekonstruieren), und nicht ausschließlich als generelle Anti-Automatisierungssteuerung. |   1   |

---

## C11.5 Modellextraktions-Defense

Erkennen und verhindern Sie unerlaubtes Model-Cloning durch API-Missbrauch. Ratenbegrenzung, Abfrage-Musteranalyse und Watermarking werden als empfohlene Schutzmaßnahmen empfohlen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                   | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 11.5.1 | Überprüfen Sie, dass Inferenz-Endpunkte Durchsatzgrenzen pro Prinzipal und global durchsetzen, die auf das Extraktions- Bedrohungsmodell abgestimmt sind, und nicht nur als generelle API-Drosselung.                                                                                                                          |   1   |
| 11.5.2 | Stellen Sie sicher, dass Extraction-Alert-Ereignisse die auslösenden Abfrage-Metadaten (z.B. Quellprinzipal, Abfrage-Volumen, Eingabeverteilungsstatistiken) enthalten, um eine Untersuchung zu unterstützen.                                                                                                                  |   2   |
| 11.5.3 | Verifizieren Sie, dass die Analyse von Abfrage-Mustern (z.B. Abfragevielfalt, Anomalien in der Eingabeverteilung, Anomalien in der Abdeckung des Ausgabe-Systems) einen automatisierten Detektor für Extraktionsversuche speist.                                                                                               |   2   |
| 11.5.4 | Stellen Sie sicher, dass die Roh-Ausgaben von Modellen (z. B. vollständige Posterior-Verteilungen, Ausgabvektoren) nicht direkt über den Anwendungs-Backend hinaus offengelegt werden, und dass extern sichtbare Antworten die Informationsdichte der Ausgaben in Abhängigkeit von der Höhe des Extraktionsrisikos minimieren. |   2   |
| 11.5.5 | Stellen Sie sicher, dass Modell-Wasserzeichen- oder Fingerprinting-Techniken angewendet werden, sodass nicht autorisierte Kopien identifiziert werden können.                                                                                                                                                                  |   3   |
| 11.5.6 | Verifizieren Sie, dass die Erkennung vermuteter Extraktionsaktivitäten adaptive Reaktionsmaßnahmen auslöst, die proportional zum geschätzten Extraktionsrisiko sind.                                                                                                                                                           |   3   |

---

## C11.6 Erkennung von Laufzeit-Kontextkontamination

Identifizieren und neutralisieren Sie manipulierte, mit Hintertüren versehene oder gegnerische Daten, die zur Laufzeit des Inferenzbetriebs über externe Quellen (z. B. RAG-Abruf, Tool-Ausgaben, MCP-Serverantworten, Grounding-Pipelines) in den Modellkontext gelangen.

|   #    | Beschreibung                                                                                                                                                                                                          | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.6.1 | Stellen Sie sicher, dass Eingaben von externen oder nicht vertrauenswürdigen Quellen vor der Modellinferenz durch eine Anomalieerkennung geleitet werden (z.B. statistische Ausreißererkennung, Konsistenzbewertung). |   2   |
| 11.6.2 | Verifizieren Sie, dass die Anomalie-Erkennungs-Schwellenwerte auf repräsentativen sauberen und adversarialen Validierungsdatensätzen abgestimmt werden.                                                               |   2   |
| 11.6.3 | Verifizieren Sie, dass Eingaben, die als anomali markiert wurden, Gatekeeping-Aktionen auslösen (Blockierung, Fähigkeitsreduzierung oder menschliche Überprüfung).                                                    |   2   |
| 11.6.4 | Stellen Sie sicher, dass die False-Positive-Rate der Anomalieerkennung an repräsentativen Daten gemessen und je Modellversion dokumentiert wird.                                                                      |   2   |

---

## C11.7 Sicherheitsrichtlinien-Anpassung

Behalten Sie die Fähigkeit bei, AI-Sicherheits- und Guardrail-Richtlinien schnell zu aktualisieren, um auf Bedrohungsinformationen und Verhaltensanalysen zu reagieren.

|   #    | Beschreibung                                                                                                                                                                                                                                                                 | Ebene |
| :----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.7.1 | Überprüfen, dass Sicherheitsrichtlinien (z.B. Content-Filter, Rate-Limit-Schwellenwerte, Guardrail-Konfigurationen) aktualisiert werden können, ohne dass eine vollständige Systemneubereitstellung erforderlich ist, und dass die Richtlinienversionen nachverfolgt werden. |   1   |
| 11.7.2 | Stellen Sie sicher, dass Richtlinienaktualisierungen autorisiert, integritätsschutzgesichert (z.B. kryptografisch signiert) und vor der Anwendung validiert werden.                                                                                                          |   2   |
| 11.7.3 | Stellen Sie sicher, dass es Rollback-Verfahren für Richtlinienänderungen gibt und dass sie getestet werden, um zu bestätigen, dass sie den vorherigen Richtlinienstatus wiederherstellen.                                                                                    |   2   |
| 11.7.4 | Stellen Sie sicher, dass die Empfindlichkeit der Bedrohungserkennung anhand des Risikokontexts angepasst werden kann (z. B. erhöhtes Bedrohungsniveau, Incident Response).                                                                                                   |   3   |

---

## C11.8 Agentensicherheits- Selbstbewertung

Für agentische KI-Systeme ergänzen Sie deterministische Richtlinien-Gates (C9.2, C9.7) durch eine KI-gestützte Überprüfung vorgeschlagener Aktionen und schützen Sie diesen Überprüfungsmechanismus vor dem umgehenden Einfluss durch Adversarial-Angriffe.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                     | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 11.8.1 | Verifizieren Sie, dass agentische Systeme eine durch KI unterstützte Überprüfung geplanter Hochrisiko-Aktionen vor der Ausführung enthalten (z. B. ein sekundäres Modell, ein strukturierter Self-Review-Schritt oder eine Ensemble-of-Judges-Prüfung), die zusätzlich und nicht anstelle des deterministischen Policy-Gates in C9.7.1 arbeitet. |   2   |
| 11.8.2 | Überprüfen Sie, dass der KI-gestützte Überprüfungsmechanismus in 11.8.1 gegen Manipulation durch adversariale Eingaben geschützt ist, sodass der Überprüfungsschritt nicht durch Prompt-Injection oder Instruction-Smuggling im Agentenkontext außer Kraft gesetzt oder umgangen werden kann.                                                    |   2   |

---

## C11.9 Sicherheitsaspekte der Selbstmodifikation & der autonomen Aktualisierung

Sicherheitskontrollen für Systeme, bei denen die KI ihre eigene Konfiguration, Prompts, den Zugriff auf Tools oder erlernte Verhaltensweisen ändern kann.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                       | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.9.1 | Verifizieren Sie, dass jede Selbstmodifikationsfähigkeit (z.B. Prompt-Umschreibung, Änderungen an der Tool-Liste, Aktualisierungen von Parametern) auf ausdrücklich ausgewiesene Bereiche beschränkt ist, mit durchgesetzten Grenzen.                                                                                                                                                              |   2   |
| 11.9.2 | Stellen Sie sicher, dass die vorgeschlagenen Selbstmodifikationen vor ihrem Wirksamwerden einer Sicherheitsfolgenabschätzung oder einer Richtlinienvalidierung unterzogen werden.                                                                                                                                                                                                                  |   2   |
| 11.9.3 | Stellen Sie sicher, dass Selbstmodifikationen explizit als sicherheitsrelevante Ereignisse klassifiziert und mit ausreichenden Details protokolliert werden, um rekonstruieren zu können, was sich geändert hat, wann, durch welchen Agenten oder Prinzipal und unter welcher Autorisierung, unabhängig davon, ob Selbstmodifikation anderweitig als geloggtes Ereignis dokumentiert ist.          |   2   |
| 11.9.4 | Stellen Sie sicher, dass Selbstmodifikationen reversibel sind und einer Integritätsprüfung unterliegen, sodass ein Rollback auf einen bekannten funktionsfähigen Zustand möglich ist und bestätigt werden kann.                                                                                                                                                                                    |   2   |
| 11.9.5 | Stellen Sie sicher, dass der Umfang der Selbstmodifikation begrenzt ist (z.B. maximale Änderungsgröße, Grenzwerte für Aktualisierungsraten, verbotene Modifikationsziele), um riskante oder durch böswillige Eingaben verursachte Änderungen zu verhindern.                                                                                                                                        |   3   |
| 11.9.6 | Verifizieren Sie, dass, wenn Sicherheitsverletzungsdaten (blockierte Eingaben, gefilterte Ausgaben, gemeldete Halluzinationen) als Trainingssignal zur Modellverbesserung verwendet werden, die Feedback-Pipeline Integritätsprüfungen, Poisoning-Erkennung und menschliche Überprüfungs-Gates umfasst, um eine adversarial manipulative Beeinflussung des Verbesserungsmechanismus zu verhindern. |   3   |

## C11.10 Abwehr von Ausnutzung durch adversariellen Bias

Schützen Sie sicherheitsrelevante Klassifikatoren vor Gegnern, die systematisch nach ausnutzbaren Verzerrungsmustern suchen und die entdeckten Unterschiede als einen Umgehungsvektor zweckentfremden.

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 11.10.1 | Überprüfen Sie, dass Adversarial-Robustheitsbewertungen für sicherheitsrelevante Klassifikatoren nach aussagekräftigen Eingabe-Untergruppen stratifiziert sind (z.B. Register der Sprache, Inhaltskategorie), wobei die pro Untergruppe unter adversarialen Bedingungen gemessenen False-Negative-Rates erfasst und als fehlerhaft markiert werden, wenn sie von den aggregierten Raten über einem definierten Schwellenwert abweichen.                                         |   2   |
| 11.10.2 | Stellen Sie sicher, dass Inferenz-Endpunkte für sicherheitsrelevante Klassifizierer (z.B. Missbrauchserkennung, Betrugsbewertung) eine Überwachung enthalten, die Abfrage-Muster berücksichtigt, welche auf Bias-Probing hindeuten, etwa eine systematische Variation entlang einer einzelnen Eingabedimension (z.B. demografisch, sprachlich, stilistisch), während andere Dimensionen konstant bleiben, und dass ein Alarm ausgelöst wird, wenn solche Muster erkannt werden. |   3   |
| 11.10.3 | Verifizieren Sie, dass, wo eine umgehungsbasierte Verzerrung als wesentliche Bedrohung erkannt wird, gehärtete Gegenmaßnahmen gegen Angriffe (z.B. adversarial training mit per-Subgroup Loss-Constraints, Ensemble-Diversität über Trainingsverteilungen hinweg) explizite Anforderungen an die Robustheit je Subgruppe einbeziehen, und dass überprüft wird, dass per-Subgroup-Robustheitsmetriken über Modellveröffentlichungen hinweg nicht zurückgehen.                    |   3   |

---

## Referenzen

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

