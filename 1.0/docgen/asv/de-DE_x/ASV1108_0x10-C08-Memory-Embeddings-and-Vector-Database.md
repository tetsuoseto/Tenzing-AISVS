# C8 Memory, Embeddings & Sicherheit von Vektor-Datenbanken

## Kontrollziel

Einbettungen und Vektor-Speicher fungieren als halb-persistentes und persistentes „Gedächtnis“ für KI-Systeme über Retrieval-Augmented Generation (RAG). Dieses Gedächtnis kann zu einem hochriskanten Datenspeicher und zu einem Datenexfiltrationspfad werden. Diese Kontrollfamilie härtet Speicher-Pipelines und Vektor-Datenbanken so aus, dass der Zugriff Least-Privilege ist, die Daten vor der Vektorisierung bereinigt werden, die Aufbewahrung explizit ist und die Systeme widerstandsfähig gegen Einbettungs-Inversion, Member-ship-Inference und das Lecken zwischen Mandanten sind.

---

## C8.1 Zugriffskontrollen für Speicher- und RAG-Indizes

Setzen Sie eine feingranulare Zugriffskontrolle und eine Durchsetzung der Zugriffsbereiche zur Abfragezeit für jede Vektor-Sammlung durch.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.1.1 | Stellen Sie sicher, dass Vektor-Insert-, Update-, Delete- und Query-Operationen mit Namespace-/Collection-/Dokument-Tag-Scope-Kontrollen (z. B. Tenant-ID, User-ID, Datenklassifizierungslabels) erzwungen werden, jeweils mit Default-Deny.                                                                |   1   |
| 8.1.2 | Stellen Sie sicher, dass jedes ingestete Dokument zur Schreibzeit mit Quelle, Autoridentität (authentifizierter Benutzer oder Systemprinzipal), Zeitstempel, Batch-ID und Embedding-Modellversion getaggt wird.                                                                                             |   2   |
| 8.1.3 | Verifizieren Sie, dass die bei der Ingestion angewendeten Dokument-Metadaten-Tags nach dem ersten Schreiben unveränderlich sind und weder durch nachgelagerte Pipeline-Phasen noch durch Benutzeraktionen geändert werden können.                                                                           |   2   |
| 8.1.4 | Überprüfen Sie, dass die Retrieval-Ereignisprotokolle der RAG-Pipeline die ausgegebene Abfrage, die abgerufenen Dokumente oder Chunks, die Ähnlichkeitswerte, die Wissensquelle sowie ob der abgerufene Inhalt vor der Einbindung in den Modellkontext einen Prompt-Injection-Scan bestanden hat, erfassen. |   2   |
| 8.1.5 | Verifizieren Sie, dass eingeschränkte Abrufindizes eindeutig markierte Köderdatensätze (Canary) enthalten, die keinen echten sensiblen Inhalt enthalten, mit Markern, die in Abruf-, Embedding- und Kontext-Assemblierungs-Pipelines überleben.                                                             |   2   |
| 8.1.6 | Stellen Sie sicher, dass eine Security-Alarmmeldung mit hoher Schweregradstufe generiert wird, sobald ein Canary-Datensatz durch Retrieval ausgewählt, durch eine Ähnlichkeitssuche abgeglichen oder als Kontext an das Modell übergeben wird.                                                              |   2   |
| 8.1.7 | Verifizieren Sie, dass die Erkennung von Retrieval-Anomalien Embedding-Dichte-Ausreißer, die wiederholte Dominanz bestimmter Dokumente in den Ähnlichkeitsergebnissen und plötzliche Verschiebungen in der Retrieval-Bias-Verteilung identifiziert, die auf Vector-Database-Poisoning hindeuten können.     |   3   |

---

## C8.2 Einbettungsbereinigung & -validierung

Inhalte vor der Vektorisierung vorab prüfen; behandle Speicherzugriffe als nicht vertrauenswürdige Eingaben; verhindere die Aufnahme unsicherer Nutzlasten.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.2.1 | Stellen Sie sicher, dass regulierte Daten und sensible Felder vor dem Einbetten erkannt und gemäß Richtlinie maskiert, tokenisiert, transformiert oder verworfen werden, wobei zu berücksichtigen ist, dass Daten, sobald sie eingebettet wurden, nicht zuverlässig aus dem resultierenden Index zurückredigiert werden können.                                                                                                                                 |   1   |
| 8.2.2 | Stellen Sie sicher, dass Inhalte, die dazu bestimmt sind, das Retrieval zu vergiften (z.B. Text, der so verfasst wurde, dass er in Nachbarschaften von Einbettungen projiziert wird, die vom Angreifer gewählt wurden, versteckte Anweisungen, die für den Kontext nachgelagerter Modelle vorgesehen sind, oder steganografische Nutzdaten in nicht-textuellen Eingaben), erkannt und abgelehnt oder quarantänisiert werden, bevor eine Vektorisierung erfolgt. |   1   |
| 8.2.3 | Stellen Sie sicher, dass Vektoren, die außerhalb normaler Cluster-Muster liegen, markiert und in Quarantäne gesetzt werden, bevor sie in Produktionsindizes gelangen.                                                                                                                                                                                                                                                                                           |   2   |
| 8.2.4 | Überprüfen Sie, dass Agenten-Ausgaben, Tool-Ausgaben und Orchestrierungs-Ergebnisse nicht automatisch in den vertrauenswürdigen Agenten-Speicher geschrieben werden, ohne explizite Quellenvalidierung (z.B. Inhaltsherkunftsprüfungen oder Schreibautorisierungs-Kontrollen, die die Quelle des Inhalts vor dem Übertragen der Writes verifizieren).                                                                                                           |   2   |
| 8.2.5 | Stellen Sie sicher, dass neuer Inhalt, der in den Speicher geschrieben wird, auf Widersprüche mit dem überprüft wird, was bereits gespeichert ist, und dass Konflikte Warnmeldungen auslösen.                                                                                                                                                                                                                                                                   |   3   |

---

## C8.3 Speicherablauf, Widerruf & Löschung

Die Aufbewahrung und der Widerruf müssen für Speicher- und RAG-Indizes explizit und durchsetzbar sein, und Löschungen müssen sich innerhalb eines gemessenen Propagationsfensters durch derivative Indizes und Caches fortpflanzen.

|   #   | Beschreibung                                                                                                                                                                                                                                          | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.3.1 | Überprüfen Sie, dass abgelaufene Vektoren aus den Abruf-Ergebnissen innerhalb eines gemessenen und überwachten Propagationszeitfensters ausgeschlossen werden.                                                                                        |   2   |
| 8.3.2 | Stellen Sie sicher, dass der Speicher aus Sicherheitsgründen zurückgesetzt werden kann (Quarantäne, selektive Löschung, vollständiges Zurücksetzen) über eine Operation, die getrennt und unabhängig von dem Prozess der Aufbewahrungs- Löschung ist. |   2   |
| 8.3.3 | Stellen Sie sicher, dass unter Quarantäne gestellter Inhalt für Untersuchungen aufbewahrt wird, jedoch während der Quarantäne von allen Abruf-Ergebnissen ausgeschlossen ist.                                                                         |   2   |

---

## C8.4 Verhindern von Embedding-Inversion & -Leckage

Adressumkehr, Membership Inference und Attributinferenz mit explizitem Threat Modeling, Gegenmaßnahmen und Regression-Testing-Gates.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                          | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.4.1 | Stellen Sie sicher, dass Datenschutz-/Nützlichkeitsziele für die Widerstandsfähigkeit gegen Embedding-Leakage definiert und gemessen werden und dass Änderungen an Embedding-Modellen, Tokenizern, Retrieval-Einstellungen oder Privacy-Transformationen durch Regressionstests gegen diese Ziele abgesichert werden. |   3   |

---

## C8.5 Durchsetzung von Zugriffsbeschränkungen für benutzerspezifischen Speicher

Verhindern Sie Cross-Tenant- und Cross-User-Leakage bei der Suche (Retrieval) und beim Zusammenstellen der Prompts.

|   #   | Beschreibung                                                                                                                                                                                                                      | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.5.1 | Überprüfen Sie, dass jede Abrufoperation die Bereichsbeschränkungen (Mandant/Benutzer/Klassifizierung) in der Vektor-Engine-Abfrage durchsetzt und diese erneut überprüft, bevor der Prompt zusammengesetzt wird (Post-Filter).   |   1   |
| 8.5.2 | Stellen Sie sicher, dass Vektorbezeichner, Namespaces und Metadatenindizierung Cross-Scope-Kollisionen verhindern und die Eindeutigkeit pro Mandant erzwingen.                                                                    |   1   |
| 8.5.3 | Stellen Sie sicher, dass Retrieval-Ergebnisse, die Übereinstimmungskriterien erfüllen, aber die Scope-Prüfungen nicht bestehen, verworfen werden.                                                                                 |   1   |
| 8.5.4 | Verifizieren Sie, dass Multi-Tenant-Tests adversariellen Abrufversuchen (promptbasiert und anfragebasiert) simulieren und eine Null-Aufnahme von Dokumenten außerhalb des Geltungsbereichs in Prompts und Ausgaben demonstrieren. |   2   |

---

## Referenzen

* [OWASP LLM08:2025 Vector and Embedding Weaknesses](https://genai.owasp.org/llmrisk/llm082025-vector-and-embedding-weaknesses/)
* [OWASP LLM04:2025 Data and Model Poisoning](https://genai.owasp.org/llmrisk/llm042025-data-and-model-poisoning/)
* [OWASP LLM02:2025 Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/)
* [MITRE ATLAS: RAG Poisoning](https://atlas.mitre.org/techniques/AML.T0070)
* [MITRE ATLAS: False RAG Entry Injection](https://atlas.mitre.org/techniques/AML.T0071)
* [MITRE ATLAS: Infer Training Data Membership](https://atlas.mitre.org/techniques/AML.T0024.000)
* [MITRE ATLAS: Invert AI Model](https://atlas.mitre.org/techniques/AML.T0024.001)

