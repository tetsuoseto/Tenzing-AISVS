# C5 Zugriffskontrolle & Identit\u00e4t f\u00fcr KI-Komponenten & Benutzer

## Kontrollziel

KI-Systeme bringen zusätzliche Herausforderungen bei der Zugriffskontrolle mit sich, die über die herkömmliche Anwendungs­sicherheit hinausgehen: Klassifikationslabels müssen Daten durch KI-spezifische Transformationen (Embeddings, Caches, Modell-Ausgaben) hinweg begleiten, Multi-Tenant-Inferenzinfrastrukturen erzeugen neuartige Seitenkanäle, und Retrieval-Augmented-Pipelines müssen die Berechtigungen der Aufrufer in jeder Phase durchsetzen. Dieses Kapitel behandelt KI-spezifische Aspekte der Zugriffskontrolle und Identität, einschließlich der Laufzeit-Isolation des Policy-Decision-Points von der Agentenausführung sowie einer autorisierungsbewussten Ausgabe-Filterung, bei der die Entitlements je Aufrufer variieren.

---

## C5.1 Authentifizierung

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                              | Ebene |
| :---: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.1.1 | Stellen Sie sicher, dass risikoreiche KI-Operationen (Modellbereitstellung, Gewichtsexport, Zugriff auf Trainingsdaten, Änderungen der Produktionskonfiguration) eine Höherstufungs-Authentifizierung mit Sitzungs-Neuverifizierung erfordern.                                                                                                                            |   2   |
| 5.1.2 | Stellen Sie sicher, dass KI-Agenten in föderierten oder Multi-System-Bereitstellungen authentifizieren, indem sie kurzfristige, kryptografisch signierte Tokens verwenden (z. B. signierte JWT-Assertions), wobei der Signaturschlüssel an die Identität des ausstellenden Systems gebunden ist (z. B. über JWKS, x5c oder senderkonstruierte Tokens wie DPoP oder mTLS). |   3   |

---

## C5.2 AI-Ressourcenautorisierung & -klassifizierung

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                                   | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.2.1 | Überprüfen Sie, dass jede KI-Ressource (Datensets, Modelle, Endpunkte, Vektor-Kollektionen, Einbettungsindizes, Compute-Instanzen) Zugriffskontrollen (z.B. RBAC, ABAC) mit expliziten Allow-Lists und Default-Deny-Richtlinien erzwingt.                                                                                                                      |   1   |
| 5.2.2 | Stellen Sie sicher, dass der privilegierte Zugriff auf Modellgewichte, Trainings-Pipelines und die Produktions-AI-Konfiguration auf einer Just-in-time-Basis bereitgestellt wird, mit einer definierten maximalen Sitzungsdauer und automatischem Ablauf, und dass ein permanenter dauerhafter privilegierter Zugriff auf diese Ressourcen nicht zulässig ist. |   2   |
| 5.2.3 | Stellen Sie sicher, dass eine dokumentierte Data-Classification-Taxonomie, die AI-spezifische Datentypen abdeckt (Embeddings, Modellgewichte, Prompt-Templates, RAG-Kontextzusammenstellungen, Fine-Tuning-Datensätze, Agent-Tool-Schemata), definiert ist, und dass AI-Assets gemäß dieser Taxonomie beschriftet sind.                                        |   2   |
| 5.2.4 | Verifizieren Sie, dass Datenklassifizierungskennzeichnungen (PII, PHI, proprietär, usw.) automatisch auf abgeleitete Ressourcen (Embeddings, Prompt-Caches, Modellausgaben) übergeleitet werden.                                                                                                                                                               |   3   |

---

## C5.3 Autorisierung zur Laufzeit der Abfrage

Erzwingen Sie den Autorisierungskontext des Aufrufers über AI-spezifische Abfragepipelines (RAG-Retrieval, Embedding-Nachschlagen, Inferenz-Ketten), damit das KI-System keine Daten zurückgibt, auf die der Aufrufer keinen Zugriff hat.

|   #   | Beschreibung                                                                                                                                                                                                                                                                       | Ebene |
| :---: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.3.1 | Stellen Sie sicher, dass KI-Inferenz- und Retrieval-Pipelines (z. B. RAG-Abfragen, Embedding-Lookups) den Autorisierungskontext des Endbenutzers in jeder Retrieval- und Montagephase durchsetzen, statt sich ausschließlich auf die Berechtigungen des Dienstkontos zu verlassen. |   1   |

---

## C5.4 Ausgabeberechtigungsdurchsetzung

Stellen Sie sicher, dass von KI generierte Ausgaben, einschließlich Zitaten und Quellenangaben, die Daten-Entitlements des Aufrufers respektieren.

|   #   | Beschreibung                                                                                                                                                                                                               | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.4.1 | Stellen Sie sicher, dass nachgelagerte Filtermechanismen nach der Inferenz verhindern, dass Antworten klassifizierte Informationen oder proprietäre Daten enthalten, die der Anforderer nicht autorisiert ist zu erhalten. |   1   |
| 5.4.2 | Überprüfen Sie, dass Zitate, Referenzen und Quellenangaben in Modell-Ausgaben gegen die Berechtigungen des Aufrufers validiert werden und entfernt werden, wenn ein nicht autorisierter Zugriff erkannt wird.              |   2   |

---

## C5.5 Isolierung des Policy-Entscheidungspunkts

Stellen Sie sicher, dass die Autorisierungsentscheidung-Infrastruktur für KI-Agenten vor Kompromittierung und Manipulation durch die von ihr gesteuerten Agenten geschützt ist.

|   #   | Beschreibung                                                                                                                                                                                                                     | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.5.1 | Überprüfen Sie, dass der Policy-Entscheidungspunkt für die Agentenautorisierung von der Ausführungsumgebung des Agents isoliert ist, sodass eine kompromittierte Agentenlaufzeit keine Bewertung beeinflussen oder umgehen kann. |   3   |
| 5.5.2 | Stellen Sie sicher, dass der Policy-Entscheidungspunkt strukturierte Aktionsbeschreibungen (z.B. Aktionstyp, Zielressource, Parameter) erhält und nicht den Roh-Reasoning-Kontext des Agents.                                    |   3   |

---

## C5.6 Multi-Mandanten-Isolation

Verhindern Sie das Cross-Tenant-Information-Leakage durch AI-spezifische gemeinsam genutzte Infrastrukturbestandteile wie Inferenz-Caches und gemeinsam genutzten Modellstatus.

|   #   | Beschreibung                                                                                                                                                                                                                                                                                                                                       | Ebene |
| :---: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 5.6.1 | Verifizieren Sie, dass Inferenzzeit-KV-Cache-Einträge nach einer authentifizierten Sitzungs- oder Mandantenidentität partitioniert werden und dass automatisches Prefix-Caching keine zwischengespeicherten Präfixe zwischen verschiedenen Sicherheitsprinzipalen gemeinsam nutzt, um timingbasierte Prompt-Rekonstruktionsangriffe zu verhindern. |   2   |
| 5.6.2 | Stellen Sie sicher, dass die gemeinsam genutzte Modell-Serving-Infrastruktur verhindert, dass Fine-Tuning-, Inferenz- oder Einbettungsoperationen eines Mandanten die Operationen eines anderen Mandanten beeinflussen oder sie beobachten können, und zwar über gemeinsam genutzten Modellstatus, Adapter-Gewichte oder Rechenressourcen.         |   2   |

---

## Referenzen

* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final)
* [NIST SP 800-63-3: Digital Identity Guidelines](https://csrc.nist.gov/pubs/sp/800/63/3/final)
* [I Know What You Asked: Prompt Leakage via KV-Cache Sharing in Multi-Tenant LLM Serving (NDSS 2025)](https://www.ndss-symposium.org/ndss-paper/i-know-what-you-asked-prompt-leakage-via-kv-cache-sharing-in-multi-tenant-llm-serving/)

