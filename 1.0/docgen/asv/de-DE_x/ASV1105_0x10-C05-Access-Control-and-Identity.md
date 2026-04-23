# C5 Zugriffskontrolle & Identität für KI-Komponenten & Nutzer

## Kontrollziel

KI-Systeme bringen Zugriffssteuerungs-Herausforderungen mit sich, die über die traditionelle Anwendungs­sicherheit hinausgehen: Klassifizierungskennzeichnungen müssen den Daten über AI-spezifische Transformationen hinweg folgen (Embeddings, Caches, Modellausgaben), eine Multi-Tenant-Inferenzinfrastruktur schafft neuartige Seitenkanäle, und Retrieval-augmented-Pipelines müssen in jeder Phase die Berechtigungen des Aufrufers durchsetzen.

Dieses Kapitel behandelt nur AI-spezifische Zugriffssteuerungs- und Identitätsbedenken. Allgemeines Identity Management und Authentifizierung (zentraler IdP, Federation, MFA, Step-up-Authentifizierung) werden durch ASVS v5 V6 abgedeckt. Allgemeine Autorisierungsmuster (RBAC/ABAC-Design, ausgelagertes PDP, dynamische Attributauswertung, Policy-Caching), protokollierte Access-Control-Audits und Multi-Tenant-Netzwerkwerke werden durch ASVS v5 V8, V14 und V16 abgedeckt.

Agentenspezifische Autorisierungsrichtlinien und Delegation werden in C9.6 behandelt; die Identität des einzelnen System-Agenten befindet sich in C9.4.1; dieses Kapitel behandelt die Laufzeitisolation des Policy Decision Point von der Agentenausführung (als Ergänzung zu C9.6.4). Durchsetzung des Geltungsbereichs der Vector-Datenbank ist in C8.1 und C8.5 beschrieben. Allgemeines Output-Safety-Filtering (PII-Redaktion, Content-Moderation, Blockierung vertraulicher Daten) ist in C7.3 beschrieben; dieses Kapitel behandelt autorisierungsbewusstes Output-Filtering, bei dem Berechtigungen je nach Aufrufer variieren.

---

## C5.1 Authentifizierung

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                    | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.1.1 | Überprüfen Sie, dass risikoreiche KI-Operationen (Modellbereitstellung, Export von Gewichten, Zugriff auf Trainingsdaten, Änderungen an der Produktionskonfiguration) eine erweiterte Authentifizierung mit Sitzungsneuverifizierung erfordern.                                                                                                 |   2   |
| 5.1.2 | Verifizieren Sie, dass KI-Agenten in föderierten oder Multi-System-Bereitstellungen über kurzlebige, kryptografisch signierte Authentifizierungstokens (z. B. signierte JWT-Assertions) authentifizieren, mit einer maximalen Lebensdauer, die für die Risikostufe angemessen ist, und einschließlich kryptografischen Nachweises der Herkunft. |   3   |

---

## C5.2 AI-Ressourcenautorisierung und -klassifizierung

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.2.1 | Stellen Sie sicher, dass jede AI-Ressource (Datensätze, Modelle, Endpunkte, Vektor-Sammlungen, Embedding-Indizes, Compute-Instanzen) Zugriffskontrollen erzwingt (z.B. RBAC, ABAC) mit expliziten Allow-Listen und Default-Deny-Richtlinien.                                                                                                                |   1   |
| 5.2.2 | Überprüfen Sie, dass ein privilegierter Zugriff auf Modellgewichte, Trainings-Pipelines und die Produktions-KI-Konfiguration nur auf Just-in-time-Basis bereitgestellt wird, mit einer festgelegten maximalen Sitzungsdauer und einem automatischen Ablauf, und dass kein dauerhaft gewährter privilegierter Stehzugriff auf diese Ressourcen zulässig ist. |   2   |
| 5.2.3 | Überprüfen Sie, dass Datenklassifizierungsbezeichnungen (PII, PHI, proprietär usw.) automatisch auf abgeleitete Ressourcen (Embeddings, Prompt-Caches, Modellausgaben) übertragen werden.                                                                                                                                                                   |   3   |
| 5.2.4 | Verifizieren, dass eine dokumentierte Data-Classification-Taxonomie, die AI-spezifische Datentypen (Embeddings, Modellgewichte, Prompt-Templates, RAG-Kontextassemblierungen, Fine-Tuning-Datensätze, Agent-Tool-Schemata) abdeckt, definiert ist, und dass KI-Assets gemäß dieser Taxonomie gekennzeichnet werden.                                         |   2   |

---

## C5.3 Berechtigungsprüfung zur Laufzeit der Abfrage

Setzen Sie den Autorisierungskontext des Aufrufers durch AI-spezifische Abfragepipelines (RAG-Abruf, Einbettungs-Lookups, Inferenz-Chain) durch, sodass das KI-System keine Daten zurückgibt, auf die der Aufrufer keinen Zugriff hat.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                  | Ebene |
| :---: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.3.1 | Stellen Sie sicher, dass KI-Inferenz- und Retrieval-Pipelines (z.B. RAG-Abfragen, Embedding-Suchen) in jeder Retrieval- und Assemblierungsphase den Autorisierungskontext des Endbenutzers durchsetzen, anstatt sich ausschließlich auf die Berechtigungen des Service-Accounts zu verlassen. |   1   |

---

## C5.4 Erzwingung der Berechtigungszuweisung bei der Ausgabe

Stellen Sie sicher, dass KI-generierte Ausgaben, einschließlich Zitate und Quellenangaben, die Datenberechtigungen des Aufrufers respektieren.

|   #   | Beschreibung                                                                                                                                                                                                            | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.4.1 | Stellen Sie sicher, dass Mechanismen zur Filterung nach der Inferenz verhindern, dass Antworten klassifizierte Informationen oder proprietäre Daten enthalten, die der Antragsteller nicht autorisiert ist zu erhalten. |   1   |
| 5.4.2 | Verifizieren Sie, dass Zitierungen, Referenzen und Quellenangaben in Modellausgaben gegen die Benutzerberechtigungen des Aufrufers geprüft und entfernt werden, wenn ein nicht autorisierter Zugriff festgestellt wird. |   2   |

---

## C5.5 Policy-Entscheidungspunkt-Isolation

Stellen Sie sicher, dass die Autorisierungsentscheidungsinfrastruktur für KI-Agenten vor Kompromittierung und Manipulation durch die Agenten geschützt ist, die sie verwalten.

|   #   | Beschreibung                                                                                                                                                                                                                  | Ebene |
| :---: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.5.1 | Verifizieren Sie, dass das Policy-Decision-Point für die Agentenautorisierung vom Ausführungsumfeld des Agents isoliert ist, sodass eine kompromittierte Agenten-Laufzeit die Bewertung weder beeinflussen noch umgehen kann. |   3   |
| 5.5.2 | Stellen Sie sicher, dass der Policy-Decision-Point strukturierte Aktionsbeschreibungen (z.B. Aktionstyp, Zielressource, Parameter) erhält, statt den unformatierten Begründungskontext des Agenten.                           |   3   |

---

## C5.6 Mandantenfähige Isolation

Verhindern Sie das Aufdecken von Informationen zwischen Mandanten durch AI-spezifische freigegebene Infrastrukturkomponenten wie Inferenz-Caches und freigegebenen Modellstatus.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                     | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 5.6.1 | Verifizieren Sie, dass Inferenzzeit-KV-Cache-Einträge nach einer authentifizierten Sitzungs- oder Mandantenidentität partitioniert werden und dass automatisches Prefix-Caching keine gecachten Präfixe zwischen unterschiedlichen Sicherheitshauptkonten teilt, um timingbasierte Prompt-Rekonstruktionsangriffe zu verhindern.                 |   2   |
| 5.6.2 | Stellen Sie sicher, dass die gemeinsame Modell-Serving-Infrastruktur verhindert, dass Feintuning-, Inferenz- oder Einbettungsoperationen eines Mandanten einen Einfluss auf die Operationen eines anderen Mandanten nehmen oder diese beobachten können, und zwar über gemeinsam genutzten Modellstatus, Adapter-Gewichte oder Rechenressourcen. |   2   |

---

## References

* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/pubs/detail/sp/800-207/final)
* [NIST SP 800-63-3: Digital Identity Guidelines](https://csrc.nist.gov/pubs/sp/800/63/3/final)
* [I Know What You Asked: Prompt Leakage via KV-Cache Sharing in Multi-Tenant LLM Serving (NDSS 2025)](https://www.ndss-symposium.org/ndss-paper/i-know-what-you-asked-prompt-leakage-via-kv-cache-sharing-in-multi-tenant-llm-serving/)

