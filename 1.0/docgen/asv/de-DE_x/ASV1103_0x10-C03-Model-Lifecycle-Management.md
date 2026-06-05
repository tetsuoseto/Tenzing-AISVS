# C3-Modell-Lifecycle-Management & Change-Control

## Kontrollziel

KI-Systeme müssen Change-Control-Prozesse implementieren, die verhindern, dass nicht autorisierte oder unsichere Modelländerungen die Produktion erreichen. Diese Kontrollen gewährleisten die Modellintegrität über den gesamten Lebenszyklus hinweg, von der Entwicklung über die Bereitstellung bis zur Außerbetriebnahme, was eine schnelle Incident-Response ermöglicht und die Verantwortlichkeit für alle Änderungen sicherstellt.

Kernziel der Sicherheit: Nur autorisierte, validierte Modelle erreichen die Produktion, indem kontrollierte Prozesse eingesetzt werden, die die Integrität, Nachverfolgbarkeit und Wiederherstellbarkeit aufrechterhalten.

---

## C3.1 Modellautorisierung & Integrität

Nur autorisierte Modelle mit verifizierter Integrität gelangen in Produktionsumgebungen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.1.1 | Überprüfen Sie, dass ein Modell-Registry ein Inventar aller bereitgestellten Modellartefakte verwaltet.                                                                                                                                                                                                                                      |   1   |
| 3.1.2 | Verifizieren Sie, dass alle Modellartefakte (Gewichte, Konfigurationen, Tokenizer, Basismodelle, Fine-tunes, Adapter sowie Sicherheits-/Policy-Modelle) kryptografisch von autorisierten Entitäten signiert sind.                                                                                                                            |   2   |
| 3.1.3 | Überprüfen Sie, dass Modellartefakt-Signaturen und Integritätsprüfsummen bei der Deploy-Admission und beim Laden verifiziert werden, und dass nicht signierte, manipulierte oder nicht übereinstimmende Artefakte abgelehnt werden.                                                                                                          |   2   |
| 3.1.4 | Stellen Sie sicher, dass die Lineage- und Dependency-Tracking-Funktion ein Abhängigkeitsdiagramm beibehält, das die Identifikation sämtlicher konsumierender Services und Agents pro Umgebung ermöglicht (z.B. dev, staging, prod).                                                                                                          |   3   |
| 3.1.5 | Überprüfen Sie, dass die Integrität der Modellherkunft und die Trace-Records die Identität einer autorisierenden Entität, Trainingsdaten-Checksummen, Validierungstest-Ergebnisse mit Pass-/Fail-Status, eine Signatur-Fingerprint-/Zertifikatsketten-ID, einen Erstellungszeitstempel sowie genehmigte Bereitstellungsumgebungen enthalten. |   3   |

---

## C3.2 Modellvalidierung & -tests

Modelle müssen definierte Sicherheits- und Sicherheitsüberprüfungen bestehen, bevor sie bereitgestellt werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.2.1 | Stellen Sie sicher, dass Modelle vor der Bereitstellung automatisierten Eingabevalidierungstests unterzogen werden.                                                                                                                                                                                                                                                                                                                                                          |   1   |
| 3.2.2 | Stellen Sie sicher, dass Modelle vor der Bereitstellung automatisierte Tests zur Ausgabe-Sanitization durchlaufen.                                                                                                                                                                                                                                                                                                                                                           |   1   |
| 3.2.3 | Stellen Sie sicher, dass Modelle vor der Bereitstellung Sicherheitsbewertungen mit festgelegten Bestehen-/Nichtbestehen-Schwellen durchlaufen.                                                                                                                                                                                                                                                                                                                               |   1   |
| 3.2.4 | Stellen Sie sicher, dass die Bereitstellung automatisch blockiert wird, wenn die Ergebnisse der Sicherheitsbewertung die für das bereitgestellte Modell definierten Grenzwerte nicht erfüllen.                                                                                                                                                                                                                                                                               |   1   |
| 3.2.5 | Stellen Sie sicher, dass Sicherheitstests Agent-Workflows, Tool- und MCP-Integrationen, RAG- und Memory-Interaktionen, multimodale Eingaben sowie Guardrails (Safety-Modelle oder Detektionsdienste) mithilfe eines versionierten Evaluations-Harness abdecken. Mindestens zeigen die Tests die Zurückweisung von Prompt-Injection-Probes aus einem gepflegten Korpus sowie die korrekte Bereinigung von Tool-Ausgaben, bevor diese in den Modellkontext aufgenommen werden. |   2   |
| 3.2.6 | Stellen Sie sicher, dass alle Modelländerungen (Deployment, Konfiguration, Außerbetriebnahme) unveränderliche Audit-Records erzeugen, einschließlich eines Zeitstempels, einer authentifizierten Actor-Identität, eines Änderungstyps sowie der Zustände vor/nachher, mit Trace-Metadaten (Umgebung und konsumierende Services/Agents) und einem Modellbezeichner (Version/Digest/Signatur).                                                                                 |   2   |
| 3.2.7 | Stellen Sie sicher, dass Modelle, die einer Post-Training-Quantisierung, -Pruning oder -Distillation unterzogen wurden, anhand derselben Sicherheits- und Ausrichtungs-Test-Suite auf dem komprimierten Artefakt vor der Bereitstellung erneut bewertet werden und dass die Bewertungsergebnisse als getrennte Datensätze gespeichert werden, die mit der Version oder dem Digest des komprimierten Artefakts verknüpft sind.                                                |   2   |

---

## C3.3 Geplante Bereitstellung & Rollback

Modellbereitstellungen müssen gesteuert, überwacht und rückgängig gemacht werden können.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                              | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.3.1 | Stellen Sie sicher, dass Produktionsbereitstellungen Mechanismen für schrittweise Rollouts implementieren (z.B. Canary- oder Blue-Green-Bereitstellungen) mit automatisierten Rollback-Auslösern auf Basis zuvor vereinbarter Fehlerquoten, Latenzschwellen, Guardrail-Alarmen oder Ausfallraten von Tools/MCP.                                           |   2   |
| 3.3.2 | Prüfen Sie, dass die Rollback-Fähigkeiten den vollständigen Modellstatus (Gewichte, Konfigurationen, Abhängigkeiten einschließlich Adapter und Sicherheits-/Richtlinienmodelle) atomar wiederherstellen.                                                                                                                                                  |   2   |
| 3.3.3 | Stellen Sie sicher, dass Modellversionen, die parallel ausgeführt werden (z.B. A/B-Tests, Canary- oder Shadow-Deployments), über einen isolierten Laufzeitstatus verfügen, sodass KI-spezifische gemeinsam genutzte Ressourcen (z.B. KV-Caches, Prompt-Caches, Sitzungszustand, Retrieval-Indizes) nicht zwischen Bereitstellungskohorten geteilt werden. |   2   |

---

## C3.4 Sichere Entwicklungspraktiken

Die Prozesse zur Modellentwicklung und zum Modelltraining müssen sicheren Vorgehensweisen folgen, um eine Kompromittierung zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                           | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 3.4.1 | Verifizieren Sie, dass AI-spezifische Laufzeitkomponenten (Agent-Orchestrierungsdienste, Tool-/MCP-Server, Modellregister sowie Prompt-/Policy-Speicher) nicht über Umgebungsgrenzen hinweg gemeinsam genutzt werden (z. B. Entwicklung, Staging, Produktion).                                                                                         |   1   |
| 3.4.2 | Stellen Sie sicher, dass AI-spezifische Konfigurationsartefakte (Prompt-Vorlagen, Agentenrichtlinien und Routing-Graphen, Tool- oder MCP-Verträge und -Schemata sowie Aktionskataloge oder Capability-Allow-Lists) in der Versionsverwaltung mit Änderungsverlauf gespeichert werden und vor der Bereitstellung eine genehmigte Überprüfung erfordern. |   1   |
| 3.4.3 | Stellen Sie sicher, dass Modelltraining und -feinabstimmungsumgebungen von Produktionsmodell-Endpunkten, Agent-Orchestrierungsdiensten, Tool/MCP-Servern und Live-RAG-Datenquellen isoliert sind.                                                                                                                                                      |   2   |

---

## C3.5 Gehostete und vom Anbieter verwaltete Model Controls

Vom Anbieter gehostete und verwaltete Modelle können ihr Verhalten ohne Ankündigung ändern. Diese Kontrollen helfen, die Sichtbarkeit, die erneute Bewertung und den sicheren Betrieb sicherzustellen, wenn die Organisation die Modellgewichte nicht kontrolliert.

|   #   | Beschreibung                                                                                                                                                                                                                                                                  | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.5.1 | Stellen Sie sicher, dass die Abhängigkeiten der gehosteten Modelle mit Anbieter, Endpunkt, vom Anbieter offengelegtem Modellbezeichner sowie Versions- oder Freigabeidentifizierer, sofern verfügbar, und mit Fallback- oder Routing-Beziehungen inventarisiert werden.       |   1   |
| 3.5.2 | Stellen Sie sicher, dass Änderungen am Provider-Modell, an der Version oder am Routing eine Sicherheitsneubewertung auslösen, bevor die weitere Nutzung in hochriskanten Workflows erfolgt.                                                                                   |   2   |
| 3.5.3 | Stellen Sie sicher, dass die Protokolle den exakten vom Anbieter zurückgegebenen Identifier des gehosteten Modells erfassen, oder dass explizit vermerkt wird, dass kein solcher Identifier offengelegt wurde.                                                                |   2   |
| 3.5.4 | Überprüfen Sie, dass hochzuverlässige Deployments entweder geschlossen fehlschlagen oder eine explizite Genehmigung erfordern, wenn der Anbieter keine ausreichenden Informationen zur Modellidentität oder zur Änderungsbenachrichtigung für eine Verifikation bereitstellt. |   3   |

---

## C3.6 Feintuning-Pipeline-Autorisierung & Integrität des Belohnungsmodells

Feinabstimmungs-Pipelines sind hochprivilegierte Vorgänge, die das Verhalten bereitgestellter Modelle in großem Maßstab verändern können. Mehrstufige Pipelines verstärken dieses Risiko, da eine Kompromittierung in jeder Zwischenstufe ein subtil verändertes Artefakt erzeugt, das von nachfolgenden Stufen akzeptiert wird. Belohnungsmodelle, die in RLHF verwendet werden, sind ML-Artefakte, die manipulierbar sind, werden jedoch häufig als statische Infrastruktur betrachtet, anstatt als versionierte, validierte Komponenten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                            | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.6.1 | Stellen Sie sicher, dass die in RLHF-Feinabstimmungen verwendeten Belohnungsmodelle versioniert, kryptografisch signiert und vor der Verwendung in einem Trainingslauf auf Integrität verifiziert sind.                                                                                                                                                                 |   2   |
| 3.6.2 | Überprüfen Sie, dass das Starten eines Fine-Tuning- oder Retraining-Laufs eine Autorisierung durch eine Person erfordert, die den Lauf nicht angefordert hat (Aufgabentrennung).                                                                                                                                                                                        |   2   |
| 3.6.3 | Stellen Sie sicher, dass die RLHF-Trainingsphasen eine automatische Erkennung von Reward-Hacking oder eine Überoptimierung des Reward-Modells einschließen (z.B. zurückgehaltene Human-Preference-Probe-Sets, Divergenzschwellen oder Monitoring der KL-Penalty), wobei der Lauf von der Beförderung blockiert wird, wenn die Erkennungsschwellen überschritten werden. |   3   |
| 3.6.4 | Verifizieren Sie, dass in Multi-Stage-Feinabstimmungs-Pipelines die Ausgabe jeder Stufe auf Integrität geprüft wird, bevor die nächste Stufe sie verarbeitet.                                                                                                                                                                                                           |   3   |
| 3.6.5 | Überprüfen Sie, dass Zwischen-Feinabstimmungs-Checkpoint als eigenständige Artefakte mit Versions- oder Digest-Kennungen registriert werden, sodass ein Rollback pro Phase möglich ist.                                                                                                                                                                                 |   3   |

---

## Referenzen

* [MITRE ATLAS](https://atlas.mitre.org/)
* [OWASP AI Testing Guide](https://owasp.org/www-project-ai-testing-guide/)
* [MLOps Principles](https://ml-ops.org/content/mlops-principles)
* [Reinforcement fine-tuning](https://platform.openai.com/docs/guides/reinforcement-fine-tuning)
* [What is AI adversarial robustness?: IBM Research](https://research.ibm.com/blog/securing-ai-workflows-with-adversarial-robustness)

