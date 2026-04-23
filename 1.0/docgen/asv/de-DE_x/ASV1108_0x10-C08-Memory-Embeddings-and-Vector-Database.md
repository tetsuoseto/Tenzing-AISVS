# C8 Speicher, Embeddings & Sicherheit von Vektor-Datenbanken

## Kontrollziel

Einbettungen und Vektor-Speicher fungieren als halb-persistenter und persistenter „Speicher“ für KI-Systeme über Retrieval-Augmented Generation (RAG). Dieser Speicher kann zu einem hochriskanten Daten-Sink und einem Pfad zur Datenexfiltration werden. Diese Kontrollfamilie härtet Speicherpipelines und Vektor-Datenbanken so, dass der Zugriff dem Prinzip der geringsten Rechte folgt, die Daten vor der Vektorisierung bereinigt werden, die Aufbewahrung explizit ist und die Systeme widerstandsfähig gegen Einbettungs-Inversion, Membership Inference und Leakage zwischen Mandanten sind.

>Hinweis zum Geltungsbereich: Allgemeine Autorisierung (RBAC/ABAC, gescoppte Tokens, Cross-Tenant-Kontrollen), Verschlüsselung der Daten im Ruhezustand und Schlüsselmanagement, generische Datenspeicherung und sichere Löschung, generische Eingabevalidierung sowie Sitzungslebenszyklusverwaltung sind nicht Gegenstand dieses Dokuments und werden durch OWASP ASVS v5 Kapitel V8, V11, V13, V14, V2 und V7 abgedeckt. Die Weitergabe des Endbenutzer-Autorisierungskontexts durch RAG-Retrieval ist in AISVS C5.3 abgedeckt. Die Weitergabe von Löschungen personenbezogener Daten über KI-Artefakte (einschließlich Embeddings) ist in AISVS C12.2 abgedeckt. Die Isolierung von Agentenspeicher-Namensräumen in Multi-Agent-Systemen ist in AISVS C9.8.3 abgedeckt. Dieses Kapitel fokussiert auf KI-spezifische Aspekte: Durchsetzung des Geltungsbereichs auf der Ebene des Vector-Engines, KI-spezifische Datenlinie (Embedding-Modellversion, Ingestion-Provenienz), Widerstand gegen Poisoning in der Embedding-Pipeline, Anomalieerkennung zur Retrieval-Zeit, RAG-spezifische Löschweitergabe-Fenster sowie Widerstand gegen Embedding-Inversion / Membership-Inference.

---

## C8.1 Zugriffskontrollen für Speicher- & RAG-Indizes

Erzwinge feingranulare Zugriffskontrollen und eine Durchsetzung der Geltungsbereiche zur Abfragezeit für jede Vektor-Sammlung.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                         | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.1.1 | Stellen Sie sicher, dass Vektor-Insert-, Update-, Delete- und Query-Operationen mit Namespace-/Collection-/Document-Tag-Scope-Steuerungen (z.B. Tenant-ID, Benutzer-ID, Datenklassifizierungslabels) mit Default-Deny erzwungen werden.                                                                                                              |   1   |
| 8.1.2 | Verifizieren Sie, dass jedes ingestete Dokument zur Schreibzeit mit Quelle, Writer-Identität (authentifizierter Benutzer oder System-Principal), Zeitstempel, Batch-ID und Embedding-Modellversion getaggt ist.                                                                                                                                      |   2   |
| 8.1.3 | Überprüfen Sie, dass die bei der Ingestion angewendeten Dokument-Metadaten-Tags nach dem erstmaligen Schreiben unveränderlich sind und nicht von nachfolgenden Pipeline-Stufen oder Benutzeraktionen geändert werden können.                                                                                                                         |   2   |
| 8.1.4 | Überprüfen Sie, dass die Retrieval-Ereignisprotokolle der RAG-Pipeline die ausgegebene Abfrage, die abgerufenen Dokumente oder Chunks, Ähnlichkeitswerte, die Wissensquelle sowie ob der abgerufene Inhalt vor der Einbindung in den Modellkontext das Prompt-Injection-Scanning bestanden hat, erfassen.                                            |   2   |
| 8.1.5 | Verifizieren Sie, dass die Anomalieerkennung bei der Abfrageerfassung Einbettungsdichtigkeits-Ausreißer identifiziert, eine wiederholte Dominanz bestimmter Dokumente in den Ähnlichkeitsergebnissen sowie abrupte Verschiebungen in der Verteilung des Retrieval-Bias erkennen kann, die auf eine Vergiftung der Vektor-Datenbank hindeuten können. |   3   |

---

## C8.2 Einbettungsbereinigung & Validierung

Content vorab prüfen, bevor es vektorisiert wird; behandle Speicherzugriffe als nicht vertrauenswürdige Eingaben; verhindere die Aufnahme unsicherer Payloads.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.2.1 | Stellen Sie sicher, dass regulierte Daten und sensible Felder vor dem Einbetten erkannt und gemäß Richtlinien maskiert, tokenisiert, transformiert oder verworfen werden, wobei zu berücksichtigen ist, dass Daten, sobald sie eingebettet wurden, nicht zuverlässig aus dem resultierenden Index zurückredigiert werden können.                                                                                                                    |   1   |
| 8.2.2 | Stellen Sie sicher, dass Inhalte, die dazu bestimmt sind, die Abrufsuche zu vergiften (z.B. Text, der so verfasst wurde, dass er in von dem Angreifer gewählte Embedding-Nachbarschaften projiziert, versteckte Anweisungen, die für den Kontext nachfolgender Modelle vorgesehen sind, oder steganografische Nutzdaten in nicht-textuellen Eingaben), erkannt und abgelehnt oder in Quarantäne versetzt werden, bevor eine Vektorisierung erfolgt. |   1   |
| 8.2.3 | Stellen Sie sicher, dass Vektoren, die außerhalb normaler Clustering-Muster liegen, gekennzeichnet und in Quarantäne überführt werden, bevor sie in Produktionsindizes aufgenommen werden.                                                                                                                                                                                                                                                          |   2   |
| 8.2.4 | Überprüfen Sie, dass die eigenen Ausgaben eines Agenten nicht automatisch in sein vertrauenswürdiges Gedächtnis zurückgeschrieben werden, ohne eine explizite Validierung (z.B. Inhaltsherkunftsprüfungen oder Schreibfreigabesteuerungen, die vor dem Festschreiben der Writes die Quelle des Inhalts verifizieren).                                                                                                                               |   2   |
| 8.2.5 | Stellen Sie sicher, dass neuer Inhalt, der in den Speicher geschrieben wird, auf Widersprüche mit dem bereits gespeicherten Inhalt geprüft wird und dass Konflikte Warnmeldungen auslösen.                                                                                                                                                                                                                                                          |   3   |

---

## C8.3 Speicherablauf, Widerruf und Löschung

Die Aufbewahrung und der Widerruf müssen explizit und durchsetzbar für Speicher- und RAG-Indizes sein, und Löschungen müssen sich innerhalb eines gemessenen Verbreitungsfensters durch abgeleitete Indizes und Caches propagieren.

|   #   | Beschreibung                                                                                                                                                                                                                                | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.3.1 | Stellen Sie sicher, dass abgelaufene Vektoren aus den Abruf-Ergebnissen innerhalb eines gemessenen und überwachten Ausbreitungsfensters ausgeschlossen werden.                                                                              |   2   |
| 8.3.2 | Stellen Sie sicher, dass der Speicher aus Sicherheitsgründen zurückgesetzt werden kann (Quarantäne, selektives Purging, vollständiger Reset) über eine Operation, die separat und unabhängig vom Prozess des Löschens der Aufbewahrung ist. |   2   |
| 8.3.3 | Verifizieren, dass quarantänierter Inhalt für Untersuchungen aufbewahrt wird, aber während der Quarantäne von allen Abruf-Ergebnissen ausgeschlossen ist.                                                                                   |   2   |

---

## C8.4 Verhindern von Embedding-Inversion & -Leckage

Adressinversion, Mitgliedschaftsinferenz und Attributinferenz mit explizitem Bedrohungsmodellierung, Gegenmaßnahmen und Regressionstest-Gates.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                 | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 8.4.1 | Verifizieren Sie, dass Datenschutz-/Nutzungsziele für den Schutz vor Embedding-Leakage definiert und gemessen werden, und dass Änderungen an Embedding-Modellen, Tokenizern, Retrieval-Einstellungen oder Datenschutz-Transformen durch Regressionstests gegen diese Ziele abgesichert sind. |   3   |

---

## C8.5 Durchsetzung von Bereichseinschränkungen für benutzerspezifischen Speicher

Verhindern Sie das Überschreiten von Mandanten- und Benutzergrenzen bei Datenlecks in der Rückgewinnung und beim Zusammenstellen der Prompts.

|   #   | Beschreibung                                                                                                                                                                                                                         | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 8.5.1 | Verifizieren Sie, dass jede Abrufoperation Gültigkeitsbereichseinschränkungen (Tenant/Nutzer/Klassifizierung) in der Vector-Engine-Abfrage erzwingt und diese erneut überprüft, bevor der Prompt zusammengesetzt wird (post-filter). |   1   |
| 8.5.2 | Überprüfen Sie, dass Vektor-Identifikatoren, Namespaces und Metadatenindexierung Cross-Scope-Kollisionen verhindern und die Eindeutigkeit pro Mandant sicherstellen.                                                                 |   1   |
| 8.5.3 | Stellen Sie sicher, dass Suchergebnisse, die die Ähnlichkeitskriterien erfüllen, aber die Bereichsprüfungen nicht bestehen, verworfen werden.                                                                                        |   1   |
| 8.5.4 | Überprüfen, dass Multi-Tenant-Tests feindselige Abrufversuche (promptbasiert und abfragebasiert) simulieren und die vollständige Vermeidung von Dokumenten außerhalb des Geltungsbereichs in Prompts und Ausgaben demonstrieren.     |   2   |

---

## References

* [OWASP LLM08:2025 Vector and Embedding Weaknesses](https://genai.owasp.org/llmrisk/llm082025-vector-and-embedding-weaknesses/)
* [OWASP LLM04:2025 Data and Model Poisoning](https://genai.owasp.org/llmrisk/llm042025-data-and-model-poisoning/)
* [OWASP LLM02:2025 Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/)
* [MITRE ATLAS: RAG Poisoning](https://atlas.mitre.org/techniques/AML.T0070)
* [MITRE ATLAS: False RAG Entry Injection](https://atlas.mitre.org/techniques/AML.T0071)
* [MITRE ATLAS: Infer Training Data Membership](https://atlas.mitre.org/techniques/AML.T0024.000)
* [MITRE ATLAS: Invert AI Model](https://atlas.mitre.org/techniques/AML.T0024.001)

