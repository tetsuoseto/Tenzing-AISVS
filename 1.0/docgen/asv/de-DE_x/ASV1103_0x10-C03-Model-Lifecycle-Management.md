# C3-Modell-Lifecycle-Management und Änderungssteuerung

## Kontrollziel

KI-Systeme müssen Änderungssteuerungsprozesse implementieren, die verhindern, dass nicht autorisierte oder unsichere Modelländerungen die Produktion erreichen. Diese Kontrollen stellen die Modellsicherheit über den gesamten Lebenszyklus hinweg sicher--von der Entwicklung über die Bereitstellung bis zur Außerbetriebnahme--, was eine schnelle Reaktion auf Vorfälle ermöglicht und die Verantwortlichkeit für alle Änderungen aufrechterhält.

Kern-Sicherheitsziel: Nur autorisierte, validierte Modelle gelangen in die Produktion, indem kontrollierte Prozesse eingesetzt werden, die die Integrität, Nachverfolgbarkeit und Wiederherstellbarkeit aufrechterhalten.

---

## C3.1 Modellautorisierung & Integrität

Nur autorisierte Modelle mit verifizierter Integrität erreichen Produktionsumgebungen.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                     | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 3.1.1 | Stellen Sie sicher, dass ein Modell-Registry ein Inventar aller bereitgestellten Modellartefakte führt und eine maschinenlesbare Model/AI Bill of Materials (MBOM/AIBOM) (z. B. SPDX oder CycloneDX) erstellt.                                                                                                                                   |   1   |
| 3.1.2 | Überprüfen Sie, dass alle Modellartefakte (Gewichte, Konfigurationen, Tokenizer, Basismodelle, Feinabstimmungen, Adapter sowie Sicherheits-/Richtlinienmodelle) durch autorisierte Stellen kryptografisch signiert sind.                                                                                                                         |   1   |
| 3.1.3 | Stellen Sie sicher, dass Modellartefakt-Signaturen und Integritäts-Prüfsummen bei der Bereitstellungszulassung und beim Laden überprüft werden, und dass nicht signierte, manipulierte oder nicht übereinstimmende Artefakte abgewiesen werden.                                                                                                  |   1   |
| 3.1.4 | Stellen Sie sicher, dass die Lineage- und Dependency-Tracking-Funktionen ein Abhängigkeitsdiagramm beibehalten, das die Identifizierung aller konsumierenden Services und Agents pro Umgebung (z.B. dev, staging, prod) ermöglicht.                                                                                                              |   3   |
| 3.1.5 | Stellen Sie sicher, dass die Integrität der Modellherkunft und die Trace-Records die Identität einer autorisierenden Einheit, Trainingsdaten-Checksummen, Validierungstest-Ergebnisse mit Pass-/Fail-Status, eine Signatur-Fingerprint-/Zertifikatsketten-ID, einen Erstellungszeitstempel sowie genehmigte Bereitstellungsumgebungen enthalten. |   3   |

---

## C3.2 Modellvalidierung &-testen

Modelle müssen definierte Sicherheits- und Sicherheitsüberprüfungen bestehen, bevor sie bereitgestellt werden.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                               | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.2.1 | Stellen Sie sicher, dass Modelle vor der Bereitstellung automatisierte Eingabevalidierungstests durchlaufen.                                                                                                                                                                                                                                                                                                               |   1   |
| 3.2.2 | Stellen Sie sicher, dass Modelle vor der Bereitstellung automatisierten Tests zur Ausgabe-Sanitisierung unterzogen werden.                                                                                                                                                                                                                                                                                                 |   1   |
| 3.2.3 | Stellen Sie sicher, dass Modelle vor der Bereitstellung Sicherheitsevaluierungen mit festgelegten Bestehen/Nichtbestehen-Schwellenwerten durchlaufen.                                                                                                                                                                                                                                                                      |   1   |
| 3.2.4 | Stellen Sie sicher, dass Sicherheitstests Agent-Workflows, Tool- und MCP-Integrationen, RAG- und Speicherinteraktionen, multimodale Eingaben sowie Guardrails (Sicherheitsmodelle oder Erkennungsdienste) mithilfe eines versionierten Evaluations-Harness abdecken.                                                                                                                                                       |   2   |
| 3.2.5 | Verifizieren Sie, dass alle Modelländerungen (Bereitstellung, Konfiguration, Außerbetriebnahme) unveränderliche Prüfprotokolle erzeugen, die einen Zeitstempel, eine authentifizierte Akteuridentität, einen Änderungs-typ sowie Vor-/Nach-Zustände enthalten, mit Rückverfolgbarkeits-Metadaten (Umgebung und konsumierende Dienste/Agenten) und einer Modellkennung (Version/Digest/Signatur).                           |   2   |
| 3.2.6 | Stellen Sie sicher, dass Validierungsfehler automatisch die Modellbereitstellung blockieren, es sei denn, eine ausdrückliche Genehmigung zur Abweichung durch vorab benannte autorisierte Personen liegt vor, mit dokumentierten geschäftlichen Begründungen.                                                                                                                                                              |   3   |
| 3.2.7 | Stellen Sie sicher, dass Modelle, die einer Post-Training-Quantisierung, -Pruning oder -Distillation unterzogen wurden, vor dem Deployment anhand derselben Sicherheits- und Ausrichtung-Test-Suite auf dem komprimierten Artefakt erneut bewertet werden und dass die Ergebnisse der Bewertung als separate Datensätze aufbewahrt werden, die mit der Version oder dem Digest des komprimierten Artefakts verknüpft sind. |   2   |

---

## C3.3 Kontrollierte Bereitstellung & Rollback

Modellbereitstellungen müssen kontrolliert, überwacht und rückgängig gemacht werden können.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                        | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.3.1 | Verifizieren Sie, dass Produktionsbereitstellungen Mechanismen für schrittweise Rollouts implementieren (z. B. Canary- oder Blue-Green-Bereitstellungen) mit automatischen Rollback-Auslösern basierend auf vorher vereinbarten Fehlerquoten, Latenzschwellen, Guardrail-Alarmen oder Ausfallraten von Tools/MCP.                                   |   2   |
| 3.3.2 | Stellen Sie sicher, dass Rollback-Funktionen den vollständigen Modellzustand (Gewichte, Konfigurationen, Abhängigkeiten einschließlich Adapter und Sicherheits-/Richtlinienmodelle) atomar wiederherstellen.                                                                                                                                        |   2   |
| 3.3.3 | Verifizieren Sie, dass die Funktionen zum Notfall-Modellabschalten Modelle nacheinander innerhalb einer vordefinierten Reaktionszeit deaktivieren können.                                                                                                                                                                                           |   3   |
| 3.3.4 | Prüfen Sie, dass der Not-Aus die gesamte Anlage umfasst und in alle Teile des Systems durchgreift, einschließlich z. B. dem Deaktivieren des Agent-Tools und des MCP-Zugriffs, der RAG-Connectoren, der Datenbank- und API-Zugriffsdaten sowie der Speicher-Store-Bindings.                                                                         |   3   |
| 3.3.5 | Stellen Sie sicher, dass Modellversionen, die parallel ausgeführt werden (z.B. A/B-Tests, Canary- und Shadow-Deployments), einen isolierten Laufzeitstatus verwenden, sodass AI-spezifische gemeinsam genutzte Ressourcen (z.B. KV-Caches, Prompt-Caches, Sitzungsstatus, Retrieval-Indices) nicht zwischen Bereitstellungskohorten geteilt werden. |   2   |

---

## C3.4 Sichere Entwicklungspraktiken

Der Modellentwicklungs- und Trainingsprozess muss sichere Praktiken einhalten, um eine Kompromittierung zu verhindern.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                     | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 3.4.1 | Stellen Sie sicher, dass AI-spezifische Laufzeit-Komponenten (Agent-Orchestrierungsdienste, Tool-/MCP-Server, Modell-Registries sowie Prompt-/Policy-Stores) nicht über Umgebungsgrenzen hinweg gemeinsam genutzt werden (z. B. Entwicklung, Staging, Produktion).                                                                               |   1   |
| 3.4.2 | Stellen Sie sicher, dass AI-spezifische Konfigurationsartefakte (Prompt-Vorlagen, Agentenrichtlinien und Routing-Graphen, Tool- oder MCP-Verträge und -Schemata sowie Aktionskataloge oder Capability-Allow-Lists) in der Versionsverwaltung mit Änderungsverlauf gespeichert sind und vor der Bereitstellung eine genehmigte Prüfung erfordern. |   1   |
| 3.4.3 | Stellen Sie sicher, dass Trainings- und Fine-Tuning-Umgebungen von Produktions-Model-Endpoints, Agent-Orchestrierungsdiensten, Tool-/MCP-Servern und Live-RAG-Datenquellen isoliert sind.                                                                                                                                                        |   2   |

---

## C3.5 Gehostete und durch den Anbieter verwaltete Modellkontrollen

Vom Gastgeber und vom Anbieter verwaltete Modelle können sich ohne vorherige Ankündigung im Verhalten ändern. Diese Kontrollen tragen dazu bei, Sichtbarkeit, Neubewertung und einen sicheren Betrieb sicherzustellen, wenn die Organisation die Modellgewichte nicht kontrolliert.

|   #   | Beschreibung                                                                                                                                                                                                                                                           | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.5.1 | Verifizieren Sie, dass die gehosteten Modellabhängigkeiten mit Anbieter, Endpoint, vom Anbieter offengelegter Modellkennung, Version oder Release-Kennung (wenn verfügbar) sowie Fallback- oder Routing-Beziehungen inventarisiert werden.                             |   1   |
| 3.5.2 | Überprüfen Sie, dass Anbieter-Model-, Versions- oder Routing-Änderungen eine Sicherheitsneubewertung auslösen, bevor die weitere Nutzung in risikoreichen Workflows erfolgt.                                                                                           |   2   |
| 3.5.3 | Stellen Sie sicher, dass die Protokolle den exakten gehosteten Modellbezeichner erfassen, der vom Anbieter zurückgegeben wurde, oder dass explizit aufgezeichnet wird, dass kein solcher Bezeichner offengelegt wurde.                                                 |   2   |
| 3.5.4 | Verifizieren, dass High-Assurance-Deployments entweder geschlossen ausfallen oder eine explizite Genehmigung erfordern, wenn der Anbieter keine ausreichenden Informationen zur Modellidentität oder zur Änderungsbenachrichtigung für die Verifizierung bereitstellt. |   3   |

---

## C3.6 Feintuning-Pipeline: Autorisierung & Integrität des Belohnungsmodells

Feinabstimmungs-Pipelines sind hochprivilegierte Vorgänge, die das Verhalten bereitgestellter Modelle in großem Maßstab verändern können. Mehrstufige Pipelines erhöhen dieses Risiko, weil ein Kompromittieren in jeder Zwischenstufe ein subtil verändertes Artefakt erzeugt, das nachfolgende Stufen akzeptieren. Belohnungsmodelle, die in RLHF verwendet werden, sind ML-Artefakte, die dem Manipulieren ausgesetzt sind, jedoch häufig als statische Infrastruktur behandelt werden, anstatt als versionierte, validierte Komponenten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                            | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 3.6.1 | Prüfen, dass das Initiieren eines Fine-Tuning- oder Retraining-Laufs eine Autorisierung durch eine Person erfordert, die den Lauf nicht angefordert hat (Trennung der Aufgaben).                                                                                                                                                                                        |   3   |
| 3.6.2 | Verifizieren Sie, dass Reward-Modelle, die beim RLHF-Feintuning verwendet werden, versioniert, kryptografisch signiert und vor der Verwendung in einem Trainingslauf auf Integrität überprüft sind.                                                                                                                                                                     |   2   |
| 3.6.3 | Stellen Sie sicher, dass die RLHF-Training-Phasen eine automatisierte Erkennung von Reward Hacking oder einer Überoptimierung des Reward Models umfassen (z.B. gehaltene menschliche Präferenz-Probe-Sets, Divergenzschwellen oder Überwachung der KL-Strafe). Das Ausführen ist von der Beförderung auszuschließen, wenn die Erkennungsschwellen überschritten werden. |   3   |
| 3.6.4 | Verifizieren Sie, dass in Multi-Stage-Feinabstimmungs-Pipelines die Ausgabe jeder Stufe auf Integrität geprüft wird, bevor sie von der nächsten Stufe übernommen wird, und dass Zwischen-Checkpoints als eigenständige Artefakte registriert werden, die ein Rollback pro Stufe ermöglichen.                                                                            |   3   |

---

## References

* [MITRE ATLAS](https://atlas.mitre.org/)
* [MLOps Principles](https://ml-ops.org/content/mlops-principles)
* [Reinforcement fine-tuning](https://platform.openai.com/docs/guides/reinforcement-fine-tuning)
* [What is AI adversarial robustness?: IBM Research](https://research.ibm.com/blog/securing-ai-workflows-with-adversarial-robustness)

