# C10 Model Context Protocol (MCP) Sicherheit

## Kontrollziel

Sicherstellen einer sicheren Ermittlung, Authentifizierung, Autorisierung, des Transports und der Verwendung von MCP-basierten Tool- und Ressourcenintegrationen, um Kontextverwechslungen, nicht autorisierte Tool-Aufrufe oder eine Offenlegung von Daten über Mandanten hinweg zu verhindern. Dieses Kapitel behandelt MCP-protokollspezifische Kontrollen.

---

## C10.1 Komponentenintegrität & Supply-Chain-Hygiene

|   #    | Beschreibung                                                                                                                                                                                                                                                               | Ebene |
| :----: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.1.1 | Stellen Sie sicher, dass die MCP-Server- und -Client-Komponenten nur aus vertrauenswürdigen Quellen bezogen und mithilfe von Signaturen, Prüfsummen oder sicheren Paketmetadaten verifiziert werden, wobei manipulierte oder nicht signierte Builds zurückgewiesen werden. |   1   |
| 10.1.2 | Stellen Sie sicher, dass in der Produktion nur allowlistete MCP-Server-Identifikatoren (Name, Version und Registry) zulässig sind und dass die Laufzeit Verbindungen zu nicht gelisteten oder nicht registrierten Servern bereits beim Ladevorgang verwirft.               |   1   |
| 10.1.3 | Verifizieren Sie, dass alle MCP-Tool- und Ressourcenschemata kryptografisch überprüfbare Provenance-Metadaten enthalten — einschließlich Autor, Zeitstempel, Versionshash, Signatur und approved-by-Felder.                                                                |   2   |

---

## C10.2 Authentifizierung & Autorisierung

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                                 | Ebene |
| :-----: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.2.1  | Stellen Sie sicher, dass MCP-Clients für jede Anfrage an MCP-Server ein gültiges Zugriffstoken bereitstellen.                                                                                                                                                                                                                                                                |   1   |
| 10.2.2  | Überprüfen Sie, dass MCP-Server über einen kontrollierten technischen Onboarding-Mechanismus registriert werden, der explizite Angaben zu Eigentümer, Umgebung und Ressourcen erfordert; nicht registrierte oder nicht auffindbare Server dürfen in der Produktion nicht aufrufbar sein.                                                                                     |   1   |
| 10.2.3  | Verifizieren Sie, dass MCP-Sitzungskennungen als Zustand behandelt werden, nicht als Identität: werden mit kryptografisch sicherer Zufallswerte generiert, an den authentifizierten Benutzer gebunden und niemals für Authentifizierungs- oder Autorisierungsentscheidungen herangezogen.                                                                                    |   1   |
| 10.2.4  | Überprüfen Sie, dass MCP-Server die ausgestellten Zugriffs-Token-Ansprüche des ausgestellten Access-Token-Emitters, der Zielgruppe, der Ablaufzeit und der Scope-Claims gemäß OAuth 2.1 validieren.                                                                                                                                                                          |   1   |
| 10.2.5  | Überprüfen Sie, dass MCP-Server, die als OAuth 2.1-Resource-Server fungieren, keine Zugriffstokens oder Benutzeranmeldeinformationen speichern oder persistieren.                                                                                                                                                                                                            |   1   |
| 10.2.6  | Überprüfen Sie, dass MCP`tools/list`und Ressourcen-Erkennungsantworten werden anhand der autorisierten Scopes des Endbenutzers gefiltert, sodass Agenten nur die Tools- und Ressourcen-Definitionen erhalten, die der Benutzer zum Aufrufen berechtigt ist.                                                                                                                  |   2   |
| 10.2.7  | Überprüfen Sie, dass MCP-Server bei jeder Tool-Ausführung Zugriffskontrollen durchsetzen, indem validiert wird, dass das Zugriffstoken des Benutzers sowohl das angeforderte Tool als auch die spezifischen Argumentwerte autorisiert, die angegeben wurden.                                                                                                                 |   2   |
| 10.2.8  | Stellen Sie sicher, dass MCP-Server keine Zugriffstoken, die von Clients empfangen wurden, an nachgelagerte APIs weiterleiten, sondern stattdessen ein separates Token beschaffen, das auf die eigene Identität des Servers beschränkt ist (z. B. über einen On-behalf-of- oder einen Client-Credentials-Flow).                                                              |   2   |
| 10.2.9  | Stellen Sie sicher, dass MCP-Clients nur die für die aktuelle Operation erforderlichen Mindestspeicherberechtigungen anfordern und für höher privilegierte Operationen schrittweise über eine Schritt-für-Schritt-Autorisierung (step-up authorization) eskalieren.                                                                                                          |   2   |
| 10.2.10 | Verifizieren Sie, dass MCP-Server bei Beendigung einer Sitzung, bei der Trennung oder bei einem Timeout die deterministische Sitzungsbeendigung durchsetzen, indem sie zwischengespeicherte Tokens, In-Memory-Zustand, temporären Speicher und Dateihandles zerstören.                                                                                                       |   2   |
| 10.2.11 | Verifizieren Sie, dass autonome Agenten sich mithilfe kryptografisch gebundener Identitätsnachweise (z.B. key-based Proof-of-Possession) authentifizieren und nicht nur mit Bearer-only-Tokens, um sicherzustellen, dass die Agentenidentität nicht übertragen, erneut abgespielt oder durch das Weiterleiten eines gemeinsam genutzten Geheimnisses nachgeahmt werden kann. |   2   |

---

## C10.3 Sichere Transport- und Netzwerkgrenzenabsicherung

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                                      | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.3.1 | Verifizieren Sie, dass ein authentifizierter, verschlüsselter streambarer-HTTP als primärer MCP-Transport in Produktionsumgebungen verwendet wird, und dass alternative Transports (z.B. stdio oder SSE) auf lokale oder streng kontrollierte Umgebungen beschränkt sind, jeweils mit expliziter Begründung.                                                      |   1   |
| 10.3.2 | Stellen Sie sicher, dass SSE-basierte MCP-Transporte nur innerhalb privater, authentifizierter interner Kanäle mit TLS, Schema-Validierung, Grenzwerten für die Nutzlastgröße und durchgesetztem Ratenlimit verwendet werden und nicht für das öffentliche Internet freigegeben sind.                                                                             |   2   |
| 10.3.3 | Überprüfen Sie, dass MCP-Server sowohl das `Origin`Überschrift und das`Host`header unabhängig auf allen HTTP-basierten Transporten (einschließlich SSE und streamable-HTTP), um DNS-Rebinding-Angriffe zu verhindern. Anfragen, bei denen entweder der Header fehlt, nicht übereinstimmt oder von einer nicht vertrauenswürdigen Origin stammt, werden abgelehnt. |   2   |
| 10.3.4 | Verifizieren Sie, dass Intermediäre das nicht ändern oder entfernen`Mcp-Protocol-Version`Header auf streamable-HTTP-Transporten, sofern nicht durch die Protokollspezifikation ausdrücklich erforderlich, um eine Protokoll-Downgrade durch Header-Entfernung zu verhindern.                                                                                      |   2   |
| 10.3.5 | Überprüfen Sie, dass MCP-Clients eine minimale akzeptable Protokollversion erzwingen und  ablehnen `initialize`Antworten, die eine Version unter diesem Minimum vorschlagen und so verhindern, dass ein Server oder ein Vermittler die Verwendung einer Protokollversion mit schwächeren Sicherheits-Eigenschaften erzwingt.                                      |   2   |

---

## C10.4 Schema-, Nachrichten- und Eingabevalidierung

|    #    | Beschreibung                                                                                                                                                                                                                                                                                                                                            | Ebene |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.4.1  | Stellen Sie sicher, dass MCP-Tool-Antworten validiert werden, bevor sie in den Modellkontext eingefügt werden, um Prompt Injection, bösartige Tool-Ausgaben oder Kontextmanipulation zu verhindern.                                                                                                                                                     |   1   |
| 10.4.2  | Stellen Sie sicher, dass Fehlerantworten von MCP-Servern keine internen Details (Stacktraces, Dateipfade, Tokens, Implementierungsdetails von Tools) dem Client oder dem Modellkontext offenlegen und dadurch Informationslecks verhindert werden, die über das Modell ausgenutzt werden könnten.                                                       |   1   |
| 10.4.3  | Überprüfen Sie, dass alle MCP-Transporte die Integrität der Nachrichtenrahmung sowie eine strikte Schema-Validierung erzwingen, um Desynchronisierungs- oder Injektionsangriffe zu verhindern.                                                                                                                                                          |   2   |
| 10.4.4  | Überprüfen Sie, dass MCP-Server für alle Funktionsaufrufe eine strikte Eingabevalidierung durchführen, einschließlich Typprüfung, Grenzvalidierung und Durchsetzung von Enumerationen.                                                                                                                                                                  |   2   |
| 10.4.5  | Verifizieren Sie, dass MCP-Clients einen Hash oder einen versionierten Snapshot der Tool-Definitionen beibehalten und dass jede Änderung an einer Tool-Definition (über`notifications/tools/list_changed`(oder zwischen den Sitzungen) löst eine erneute Genehmigung aus, bevor das geänderte Tool aufgerufen werden kann.                              |   2   |
| 10.4.6  | Stellen Sie sicher, dass alle MCP-Transportmechanismen maximale Payload-Größenlimits durchsetzen und fehlerhafte, abgeschnittene oder ineinander verschachtelte Frames zurückweisen.                                                                                                                                                                    |   2   |
| 10.4.7  | Überprüfen Sie, dass MCP-Server nicht erkannte oder übergroße Parameter in Funktionsaufrufen zurückweisen.                                                                                                                                                                                                                                              |   2   |
| 10.4.8  | Überprüfen Sie, dass MCP-Tool- und Ressourcen-Schemata (z.B. JSON-Schemata oder Fähigkeitsdeskriptoren) zusammen mit Schema-Manifests auf Authentizität und Integrität mithilfe von Signaturen validiert werden, um Schema-Manipulation oder bösartige Parameteränderungen zu verhindern.                                                               |   3   |
| 10.4.9  | Überprüfen Sie, dass Intermediäre, die den Nachrichteninhalt bewerten, entweder die von ihnen ausgewertete kanonisierte Darstellung weiterleiten oder Nachrichten ablehnen, bei denen mehrere Byte-Darstellungen unterschiedliche geparste Strukturen erzeugen könnten.                                                                                 |   3   |
| 10.4.10 | Stellen Sie sicher, dass MCP-Server Tool-Antworten mit einem eindeutigen Nonce und einem Zeitstempel innerhalb eines begrenzten Zeitfensters signieren, sodass das aufrufende Agent die Herkunft, Integrität und Aktualität verifizieren kann, um Spoofing, Manipulation und Wiedereinspielen von Tool-Antworten durch Zwischeninstanzen zu verhindern. |   3   |

---

## C10.5 Sicherheit beim ausgehenden Zugriff & bei der Ausführung von Agents

|   #    | Beschreibung                                                                                                                                                                                                            | Ebene |
| :----: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.5.1 | Überprüfen Sie, dass MCP-Server ausgehende Anfragen auf genehmigte interne oder externe Ziele gemäß Least-Privilege-Egress-Richtlinien einschränken, wobei Egress zu allen anderen Zielen standardmäßig blockiert wird. |   2   |

---

## C10.6 Transportbeschränkungen und Kontrollen für Hochrisiko-Grenzen

|   #    | Beschreibung                                                                                                                                                                                                                                                                                                                                            | Ebene |
| :----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| 10.6.1 | Verifizieren Sie, dass MCP-Sicherheitskontrollen Fail-Closed-Semantik erzwingen: Wenn die Validierung des Tool-Schemas, die MCP-Protocol-Version-Aushandlung, die Authentifizierungsprüfung oder die Richtlinienauswertung fehlschlägt oder nicht abgeschlossen werden kann, ist die Standardaktion, die Anfrage zu verweigern, anstatt sie zuzulassen. |   2   |
| 10.6.2 | Stellen Sie sicher, dass MCP-Server nur erlaubte Funktionen und Ressourcen offenlegen und die Funktionsaufrufe auf statisch definierte, vorab genehmigte Namen beschränken, die nicht durch benutzer- oder modellbereitgestellte Eingaben beeinflusst werden können.                                                                                    |   3   |

---

## Referenzen

* [Model Context Protocol (MCP) Specification](https://modelcontextprotocol.io/)
* [OWASP MCP Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/MCP_Security_Cheat_Sheet.html)
* [NIST SP 800-207: Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final)

