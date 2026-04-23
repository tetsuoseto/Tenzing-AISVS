# C10 Model Context Protocol (MCP) Sicherheit

## Kontrollziel

Sichern Sie die sichere Erkennung, Authentifizierung, Autorisierung, den Transport und die Nutzung von MCP-basierten Tool- und Ressourcen-Integrationen, um Kontextverwechslungen, nicht autorisierte Tool-Aufrufe oder eine Offenlegung von Daten zwischen Mandanten zu verhindern.

---

## C10.1 Komponentenintegrität & Lieferketten-Hygiene

|   #    | Beschreibung                                                                                                                                                                                                                                                                          | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.1.1 | Stellen Sie sicher, dass die Komponenten für den MCP-Server und -Client ausschließlich aus vertrauenswürdigen Quellen bezogen und anhand von Signaturen, Prüfsummen oder sicherer Paketmetadaten verifiziert werden, wobei manipulierte oder nicht signierte Builds abgelehnt werden. |   1   |
| 10.1.2 | Stellen Sie sicher, dass in der Produktion nur erlaubte MCP-Server-Identifikatoren (Name, Version und Registry) zulässig sind und dass die Laufzeit beim Laden Verbindungen zu nicht aufgelisteten oder nicht registrierten Servern abweist.                                          |   1   |

---

## C10.2 Authentifizierung & Autorisierung

>Geltungsbereich: Allgemeine Grundsätze der Bevollmächtigung von Agenten (die Ausgabe des Modells darf keine Zugriffskontrollen außer Kraft setzen, Delegationskontext, kontinuierliche Autorisierung) werden in C9.6 behandelt. Die Kontrollen in diesem Abschnitt adressieren MCP-protokollspezifische Authentifizierungs- und Autorisierungsmechanismen. Weitere Einzelheiten zu OAuth finden sich in ASVSv5 V10.

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                         | Ebene |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 10.2.1  | Verifizieren Sie, dass MCP-Clients und -Server das OAuth 2.1-Authorisierungsframework implementieren: Clients legen bei jeder Anfrage ein gültiges Zugriffstoken vor, und Server validieren die Token-Aussteller-, Zielgruppen-, Ablauf- und Umfangsangaben (scope). Sie fungieren dabei als Ressourcenserver, die keine Tokens oder Benutzerdaten speichern.                        |   1   |
| 10.2.3  | Stellen Sie sicher, dass MCP-Server über einen kontrollierten technischen Onboarding-Mechanismus registriert werden, der explizite Definitionen für Eigentümer, Umgebung und Ressourcen erfordert; nicht registrierte oder nicht auffindbare Server dürfen in der Produktion nicht aufrufbar sein.                                                                                   |   1   |
| 10.2.6  | Überprüfen Sie, dass MCP`tools/list`und die Antworten zur Ressourcenentdeckung werden basierend auf den autorisierten Geltungsbereichen des Endbenutzers gefiltert, sodass Agents nur die Tools- und Ressourcendefinitionen erhalten, die der Benutzer aufrufen darf.                                                                                                                |   2   |
| 10.2.7  | Stellen Sie sicher, dass MCP-Server bei jedem Tool-Aufruf eine Zugriffskontrolle erzwingen, indem überprüft wird, dass der Zugriffstoken des Benutzers sowohl das angeforderte Tool als auch die spezifischen Argumentwerte, die bereitgestellt wurden, autorisiert.                                                                                                                 |   2   |
| 10.2.8  | Stellen Sie sicher, dass MCP-Sitzungskennungen als Zustand behandelt werden, nicht als Identität: Sie werden mithilfe kryptografisch sicherer Zufallswerte erzeugt, an den authentifizierten Benutzer gebunden und niemals für Authentifizierungs- oder Autorisierungsentscheidungen herangezogen.                                                                                   |   1   |
| 10.2.9  | Verifizieren Sie, dass MCP-Server keine von Clients erhaltenen Zugriffstoken an nachgelagerte APIs weitergeben, sondern stattdessen ein separates Token beziehen, das auf die eigene Identität des Servers beschränkt ist (z.B. über einen On-behalf-of- oder einen Client-Credentials-Flow).                                                                                        |   2   |
| 10.2.11 | Verifizieren Sie, dass MCP-Clients nur die Mindestscope anfordern, die für die aktuelle Operation erforderlich sind, und erhöhen Sie schrittweise über Step-up-Authorization für Operationen mit höherer Berechtigung.                                                                                                                                                               |   2   |
| 10.2.12 | Verifizieren Sie, dass MCP-Server bei Beendigung, Trennung oder Ablauf einer Sitzung den deterministischen Sitzungsabbruch erzwingen und dabei zwischengespeicherte Tokens, In-Memory-Status, temporären Speicher und Dateihandles zerstören.                                                                                                                                        |   2   |
| 10.2.13 | Überprüfen Sie, dass autonome Agenten sich mithilfe kryptografisch gebundener Identitätsnachweise (z.B. key-basiertes Proof-of-Possession) authentifizieren und nicht nur mit Bearer-only-Tokens, sodass die Agentenidentität nicht durch Weiterleiten eines gemeinsam genutzten Geheimnisses übertragen, wiedergegeben oder durch Abbilden (Impersonation) missbraucht werden kann. |   2   |

---

## C10.3 Sichere Übertragung & Netzgrenzen-Schutz

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                      | Ebene |
| :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.3.1 | Überprüfen Sie, dass der authentifizierte, verschlüsselte streamable-HTTP als primärer MCP-Transport in Produktionsumgebungen verwendet wird und dass alternative Transports (z.B. stdio oder SSE) auf lokale oder streng kontrollierte Umgebungen beschränkt sind, mit expliziter Begründung.                                    |   1   |
| 10.3.3 | Stellen Sie sicher, dass SSE-basierte MCP-Transporte nur innerhalb privater, authentifizierter interner Kanäle verwendet werden, mit TLS, Schema-Validierung, Begrenzungen der Payload-Größe und Durchsatzbegrenzung, die erzwungen werden, und dass sie nicht dem öffentlichen Internet ausgesetzt sind.                         |   2   |
| 10.3.4 | Überprüfen Sie, dass MCP-Server die `Origin`und`Host`Header auf allen HTTP-basierten Transports (einschließlich SSE und streamable-HTTP), um DNS-Rebinding-Angriffe zu verhindern, und Anfragen von nicht vertrauenswürdigen, nicht übereinstimmenden oder fehlenden Origins zurückzuweisen.                                      |   2   |
| 10.3.5 | Prüfen Sie, dass Intermediäre die nicht verändern oder entfernen`Mcp-Protocol-Version`Header bei streamable-HTTP-Transporten, sofern nicht ausdrücklich durch die Protokollspezifikation erforderlich, um einen Protokoll- Downgrade durch das Entfernen von Headern zu verhindern.                                               |   2   |
| 10.3.6 | Überprüfen Sie, dass SSE-basierte MCP-Transport-Endpunkte TLS, Authentifizierung, Schema-Validierung, Begrenzungen für die Nutzlastgröße und Ratenbegrenzung erzwingen.                                                                                                                                                           |   2   |
| 10.3.7 | Verifizieren Sie, dass MCP-Clients eine mindestens akzeptable Protokollversion erzwingen und ablehnen, `initialize`Antworten, die eine Version unterhalb dieses Minimums vorschlagen und so verhindern, dass ein Server oder ein Vermittler die Nutzung einer Protokollversion mit schwächeren Sicherheitseigenschaften erzwingt. |   2   |

---

## C10.4 Schema, Nachricht und Eingabevalidierung

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                                               | Ebene |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 10.4.1  | Stellen Sie sicher, dass MCP-Tool-Antworten validiert werden, bevor sie in den Modellkontext eingefügt werden, um Prompt-Injection, bösartige Tool-Ausgaben oder Kontextmanipulation zu verhindern.                                                                                                                                        |   1   |
| 10.4.2  | Verifizieren Sie, dass MCP-Tool- und Resource-Schemata (z.B. JSON-Schemata oder Capability-Deskriptoren) mithilfe von Signaturen auf Authentizität und Integrität validiert werden, um Schema-Manipulation oder bösartige Parameteränderungen zu verhindern.                                                                               |   3   |
| 10.4.3  | Verifizieren Sie, dass alle MCP-Transporte die Integrität der Nachrichtenrahmung, eine strikte Schema-Validierung, maximale Nutzlastgrößen erzwingen und bösartig verformte, abgeschnittene oder ineinander verschachtelte Frames ablehnen, um eine Desynchronisierung oder Injektionsangriffe zu verhindern.                              |   2   |
| 10.4.4  | Überprüfen Sie, dass MCP-Server für alle Funktionsaufrufe eine strikte Eingabevalidierung durchführen, einschließlich Typprüfung, Grenzwertvalidierung, Erzwingung von Enumeration-Werten sowie der Zurückweisung nicht erkannter oder übergroßer Parameter.                                                                               |   2   |
| 10.4.5  | Verifizieren Sie, dass MCP-Clients einen Hash oder einen versionierten Snapshot der Tool-Definitionen beibehalten und dass jede Änderung an einer Tool-Definition (über`notifications/tools/list_changed`oder zwischen Sitzungen) löst eine erneute Genehmigung aus, bevor das geänderte Tool aufgerufen werden kann.                      |   2   |
| 10.4.6  | Stellen Sie sicher, dass Fehlerantworten des MCP-Servers keine internen Details (Stack-Traces, Dateipfade, Tokens, Tool-Implementierung) gegenüber dem Client oder dem Modellkontext offenlegen und damit Informationslecks verhindern, die über das Modell ausgenutzt werden könnten.                                                     |   1   |
| 10.4.8  | Stellen Sie sicher, dass Zwischeninstanzen, die den Nachrichteninhalt auswerten, entweder die kanonische Darstellung weiterleiten, die sie ausgewertet haben, oder Nachrichten ablehnen, bei denen mehrere Byte-Darstellungen zu unterschiedlichen geparsten Strukturen führen könnten.                                                    |   3   |
| 10.4.11 | Stellen Sie sicher, dass MCP-Server Tool-Antworten mit einem eindeutigen Nonce und einem Zeitstempel innerhalb eines begrenzten Zeitfensters signieren, sodass der aufrufende Agent Ursprung, Integrität und Aktualität verifizieren kann und Spoofing, Manipulation und Wiedergabe von Tool-Antworten durch Vermittler verhindert werden. |   3   |

---

## C10.5 Ausgangszugriff & Agenten-Ausführsicherheit

>Scope Hinweis: Ausführungsbudgets, Circuit Breaker und menschliche Genehmigungs-Gates für agenteninitiierte Aktionen (einschließlich MCP-Tool-Aufrufen) werden in C9.1 und C9.2 behandelt. Kontrollen in diesem Abschnitt adressieren MCP-spezifische ausgehende Netzwerk-Einschränkungen.

|   #    | Beschreibung                                                                                                                                                                                                                                                 | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :---: |
| 10.5.1 | Stellen Sie sicher, dass MCP-Server nur nach Least-Privilege-Egress-Richtlinien ausgehende Anfragen an genehmigte interne oder externe Ziele initiieren dürfen und keinen Zugriff auf beliebige Netzwerkziele oder interne Cloud-Metadaten-Dienste erhalten. |   2   |

---

## C10.6 Transportbeschränkungen & Hochrisiko-Grenzkontrollen

>Rahmennotiz: Die Isolation der allgemeinen Agenten-Sandbox wird in C9.3 behandelt. Die Tenant- und Umgebungstrennung für Multi-Agenten-Systeme wird in C9.8 behandelt. Die Kontrollen in diesem Abschnitt adressieren MCP-spezifische Transport- und Dispatch-Einschränkungen.

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                        | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.6.2 | Verifizieren Sie, dass MCP-Server ausschließlich erlaubte Funktionen und Ressourcen bereitstellen und dynamische Dispatching-Mechanismen, reflektive Aufrufe oder die Ausführung von Funktionsnamen, die durch benutzer- oder modelseitig bereitgestellte Eingaben beeinflusst werden, verbieten.                                                                   |   3   |
| 10.6.4 | Überprüfen Sie, dass MCP-Sicherheitskontrollen Fail-Closed-Semantik erzwingen: Wenn die Tool-Schema-Validierung, die MCP-Protocol-Version-Negotiation fehlschlägt, ein Authentifizierungscheck fehlschlägt oder die Policy-Auswertung fehlschlägt bzw. nicht abgeschlossen werden kann, ist die Standardaktion, die Anfrage zu verweigern, anstatt sie zu erlauben. |   2   |

---

## References

* [Model Context Protocol (MCP) Specification](https://modelcontextprotocol.io/)
* [OWASP MCP Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/MCP_Security_Cheat_Sheet.html)
* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/pubs/detail/sp/800-207/final)

